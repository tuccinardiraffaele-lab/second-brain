---
tipo: loss
creato: 2026-04-20
aggiornato: 2026-04-20
stato: chiusa
progetto: "[[Football Trading]]"
pillar: Quality
livello: 2
failure-mode: return silenzioso in branch di eccezione lascia stato fantasma non più sorvegliato
classificazione-chiusura: A
tags:
  - loss/execution
  - loss/retry-path
area: prodotto
---

## Fenomeno

Close walker su `OVER_UNDER_65` (PSG vs Lyon 2026-04-19): fill parziale 9.58 su 135 richiesti, 20 iterazioni stalled → `close_walker_incomplete`. Il branch dedicato persisteva una `green` PARTIAL + alert critical + `return`. Da quel momento la posizione restava aperta su Betfair ma scompariva dal tracking di `ExitAgent` finché il market non passava `CLOSED` (orphan sweep a fine partita). 3 occorrenze su 6 del 19/04 chiusero in perdita (−135 € netti) senza alcun intervento di stop loss.

## Causa base

Il contract del walker (fix 2026-04-17 `4e8bf9e`) assumeva *"exit must always complete entro 20 iterazioni"*. Il branch di fallimento ne era la safety net teorica: scriveva log + alert + `return` puro, **senza comunicare il fallimento a `ExitAgent`** e **senza re-enqueue del residuo in `pending_greens`**. Risultato: nessun meccanismo riprendeva la posizione. Il reconciler era esplicitamente bloccato da `_exited_signals` (aggiunto da `_trigger_exit` *prima* di sapere l'esito del walker).

Root cause non è "il walker non riprova abbastanza" ma "l'architettura accetta uno stato fantasma" — una posizione può esistere su Betfair senza essere tracciata da nessuno.

## Strumento applicato

**UPS** (`.brain/debug/close-walker-incomplete-position-abandoned.md`) per identificare le 5 condizioni necessarie. Poi **Quality Pillar** per dichiarare 18 acceptance criteria che formalizzassero *"una posizione aperta è sempre sorvegliata"* come invariante osservabile. Piano implementativo in 6 fasi con persistenza B (una sola green row) + marker Redis + colonna `position_status` come doppia rappresentazione dello stato intermedio.

## Classificazione di chiusura

**A** — violazione di AC esistente. *"Il bot gestisce il rischio di una posizione aperta"* era un AC implicito del sistema di trading (è la ragione di esistere di `ExitAgent`). Il branch abbandono violava l'AC producendo posizioni esposte senza stop. Difetto promosso nell'implementazione (commit `d5dadc5`): il branch partial-fill ora cade nel retry/escalate path, il force_flush completa deterministicamente, la posizione non viene mai rimossa dal tracking senza conferma di chiusura.

## Lezione riusabile

**Ogni branch che fa `return` in un codice di retry è un sospetto.** Se quel `return` rappresenta un *fallimento non fatale* (niente exception, niente propagation), deve **comunicare esplicitamente il fallimento a qualcuno** — altrimenti lo stato che dipendeva da quel codice resta in limbo.

Due test operativi riutilizzabili:
1. Ogni `return` in un path di chiusura/rollback va letto chiedendosi *"chi si ricorda che questa cosa non è finita?"*. Se la risposta è "nessuno", è un bug.
2. Ogni stato "transient" in memoria (qui `_exited_signals`) **deve** avere una fonte durable equivalente (qui il marker Redis con TTL). L'in-memory si perde ai restart; il durable è l'unica verità a distanza di tempo.

Applicazione diretta al progetto: l'entry walker (`_open_via_ladder_walk`) ha lo stesso pattern di abbandono documentato in `.brain/debug/walker-no-fill-ever-abandons-signal.md` — va rivalutato con la stessa lente in una prossima sessione.

## Sorgente brain locale

Sorgente: `.brain/debug/close-walker-incomplete-position-abandoned.md` (fix-committato `d5dadc5`).
Piano master: `.brain/planning/2026-04-20-exit-lifecycle-robust-redesign.md` (completato).
