---
tipo: loss
creato: 2026-04-20
aggiornato: 2026-04-20
stato: chiusa
progetto: "[[Football-Trading]]"
pillar: Quality
livello: 2
failure-mode: reset legacy operante su stato che il nuovo flusso considera autoritativo
classificazione-chiusura: A
tags:
  - loss/pipeline
  - loss/refactor
area: prodotto
---

## Fenomeno

Nel `monthly_full_retrain`, `pattern_monitor.reset_after_retrain()` veniva invocato nell'ordine storico — DOPO il retrain XGBoost ma PRIMA del nuovo `_retrain_cluster_model()`. Il reset legacy faceva `DELETE FROM pattern_stats` per purgare i vecchi `pattern_id` (hash delle foglie XGBoost). Tra quella DELETE e il rebuild del ClusterModel passavano 3-5 minuti (Optuna 50 trial + INSERT cluster_models + re-labeling). Durante quella finestra `pattern_stats` era vuota, `AnalyticsAgent` poteva hot-reloadare il nuovo `cluster_models` (ogni 5 min), `SignalAgent` emetteva segnali e il check `is_pattern_active()` ritornava True per default (pattern mai visti) → **il circuit breaker era bypassato sul nuovo modello prima ancora che le sue stats fossero ricostruite**.

## Causa base

Ordine delle operazioni copiato dal flusso legacy (reset PRIMA del retrain del modello successivo, logica pensata per il vecchio `pattern_id` basato su foglie XGBoost) senza adattarlo al nuovo flusso dove `_retrain_cluster_model` internamente ricostruisce `pattern_stats`. Il reset legacy operava su uno stato che il nuovo flusso aveva appena ridisegnato come autoritativo: il cleanup faceva danno invece di beneficio.

## Strumento applicato

AM equivalent (defect register `.brain/autonomous-maintenance/defects/closed/FT-pattern-monitor-finestra-incoerenza-reset-2026-04-20.md`) con violazione di AC-13 (finestra di incoerenza ≤5 min, nessun bypass del circuit breaker). Fix a tre livelli:

1. `reset_after_retrain` spostato DOPO `_retrain_cluster_model` → la sync del monitor avviene su `pattern_stats` già ricostruita.
2. `reset_after_retrain` riscritto: non fa più DELETE su pattern_stats (già ricostruita dal trainer), esegue clear in-memory + `load_from_storage` + purga `exploration:cluster:*` keys stale.
3. `monthly_full_retrain` schedulato alle 02:00 UTC → nessuna partita live, SignalAgent inattivo. Anche se la finestra di incoerenza ci fosse, il rischio di bypass è nullo perché non ci sono segnali in volo.

## Classificazione di chiusura

**A — violazione di AC esistente**. AC-13 limitava esplicitamente la finestra di incoerenza a ~5 min accettabili; il draft iniziale la produceva sistematicamente insieme a un AnalyticsAgent allineato al nuovo modello.

## Lezione riusabile

Quando estendi una pipeline di retrain esistente aggiungendo un nuovo step integrato che "rebuilda" parte dello stato condiviso, gli step di reset pre-esistenti a monte o a valle vanno rivisti esplicitamente. Non è un refactor cosmetico, è una domanda di semantica:

- Il mio nuovo step ricostruisce stato che prima veniva azzerato altrove? Se sì → devo rimuovere/spostare quel reset, non lasciarlo nell'ordine storico.
- Il mio nuovo step persiste in storage nuovo che altri componenti hot-reloadano? Se sì → devo garantire che il mio rebuild chiuda PRIMA che il hot-reload diventi visibile ai consumer (o usare scheduling che elimini i consumer — es. retrain notturno).

Principio: **l'aggiunta di uno step che riscrive X rende obsoleti tutti i cleanup legacy che operavano su X sotto l'ipotesi "lo ricostruisco al prossimo trigger"**. Il nuovo step È il trigger di ricostruzione; lo step legacy stava solo azzerando uno stato che il nuovo flusso ritiene autoritativo.

Come si intercetta in pratica: in code review, cerca ogni `DELETE/TRUNCATE/RESET` nella pipeline e chiediti "chi riempie questo stato adesso?". Se la risposta non è "il successivo step" ma "il successivo retrain fra un mese", quel reset è in posizione sbagliata.

Mitigazione addizionale: scheduling notturno per tutti i retrain pesanti (quando non c'è traffico live) riduce il blast radius di qualsiasi finestra di incoerenza transitoria, indipendentemente dalla sua origine.

## Sorgente brain locale

Sorgente: `.brain/autonomous-maintenance/defects/closed/FT-pattern-monitor-finestra-incoerenza-reset-2026-04-20.md`

Piano di riferimento: `.brain/planning/2026-04-20-pattern-monitor-relabel-retrain.md`
