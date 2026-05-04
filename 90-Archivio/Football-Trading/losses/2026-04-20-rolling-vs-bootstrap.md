---
tipo: loss
creato: 2026-04-20
aggiornato: 2026-04-20
stato: chiusa
progetto: "[[Football-Trading]]"
pillar: Quality
livello: 2
failure-mode: algoritmo rolling live applicato at-bootstrap senza riprogettare
classificazione-chiusura: A
tags:
  - loss/algoritmi
  - loss/calibration
area: prodotto
---

## Fenomeno

Il primo draft di `_rebuild_pattern_stats_90d` calcolava il disable at-bootstrap usando `tail = recent[-drawdown_window:]` — ultima coda di 20 trade — invece che sull'intera serie del cluster in finestra 90gg. Un cluster con 80 trade iniziali a -€500 e 20 trade finali positivi risultava **attivo** — il recupero recente dominava il giudizio iniziale, e il "dazio di ri-verifica" che il piano voleva eliminare tornava parzialmente in scena.

## Causa base

Logica copiata 1:1 dallo script `backfill_cluster_ids.py::rebuild_pattern_stats`, che a sua volta replicava il comportamento rolling di `PatternMonitor._check_exhaustion` live. Quel comportamento ha senso **live** (reazione rapida a un momento sfavorevole recente, con la storia precedente già incorporata nelle stats accumulate) ma è sbagliato **at-bootstrap**, dove l'intent è giudizio cumulativo onesto sull'intera storia del cluster nella finestra.

## Strumento applicato

AM equivalent (defect register `.brain/autonomous-maintenance/defects/closed/FT-pattern-monitor-disable-rolling-vs-cumulativo-2026-04-20.md`) con violazione di AC-04/AC-05. Fix: sostituzione `tail[-drawdown_window:]` con `series` intera sia per drawdown (sum) sia per accuracy (wins/total). Gate statistico `len(series) >= min_trades` mantenuto per evitare falsi positivi su cluster con pochi trade. `recent_pnl` jsonb stored resta la tail 20 per compatibilità col behavior live post-bootstrap.

## Classificazione di chiusura

**A — violazione di AC esistente**. AC-04 diceva "drawdown cumulativo" e AC-05 "peso uniforme 1.0 su tutti i trade del cluster". L'implementazione rolling violava entrambi sul piano cumulativo.

## Lezione riusabile

Un algoritmo di decisione ha un comportamento diverso a seconda della fase temporale in cui viene applicato:

- **Live / streaming**: reagisce al presente. La storia è già incorporata in stato accumulato (contatori, deque, rolling aggregates). L'algoritmo guarda solo ciò che arriva fresco.
- **Bootstrap / retrofit**: giudica il passato. Non c'è stato accumulato, c'è solo una serie di eventi storici. L'algoritmo deve aggregare tutto per formulare un verdetto iniziale.

**Errore tipico**: applicare l'algoritmo live tale-quale al bootstrap. Funziona sintatticamente ma cambia semantica — il verdetto diventa "reagisce al momento più recente" invece di "giudica la storia complessiva".

Segnali che indicano che stai cadendo nel trap:

- Il piano parla di "giudizio onesto sui soldi veri persi" — è un segnale forte che serve cumulativo.
- Il piano parla di "disabilitare cluster strutturalmente perdenti" — strutturale ≠ recente.
- Stai copiando una funzione live in un contesto di rebuild/retrofit — fermati e riprogetta.

Tipico punto di verifica: scrivi esplicitamente cosa vuoi che succeda a un'entità con 80 trade perdenti seguita da 20 positivi. Se la risposta "deve nascere disabilitata" ≠ quello che il codice fa → hai applicato la logica sbagliata.

## Sorgente brain locale

Sorgente: `.brain/autonomous-maintenance/defects/closed/FT-pattern-monitor-disable-rolling-vs-cumulativo-2026-04-20.md`

Piano di riferimento: `.brain/planning/2026-04-20-pattern-monitor-relabel-retrain.md`
