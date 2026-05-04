---
tipo: loss
creato: 2026-04-20
aggiornato: 2026-04-20
stato: chiusa
progetto: "[[Football-Trading]]"
pillar: Quality
livello: 2
failure-mode: rebuild non atomico portato da script one-shot a componente live
classificazione-chiusura: A
tags:
  - loss/atomicita
  - loss/concurrency
area: prodotto
---

## Fenomeno

Nel primo draft di `_rebuild_pattern_stats_90d` dentro il `monthly_full_retrain`, la sequenza `TRUNCATE TABLE pattern_stats` seguita da N `INSERT` girava in transazioni asyncpg autonome (autocommit implicito). Fra TRUNCATE e il primo INSERT, e fra qualsiasi INSERT intermedio, la tabella era vuota o parzialmente popolata e visibile a `PatternMonitor._persist` concorrenti, alla dashboard, alle query ad-hoc. Un crash a metà loop avrebbe lasciato stato permanentemente inconsistente senza rollback.

## Causa base

Logica riutilizzata dallo script one-shot `backfill_cluster_ids.py` (asyncpg.Connection con autocommit implicito), senza riconoscere che il contesto live-system richiede atomicità e lock di breve durata — requisiti nuovi rispetto al contesto one-shot dove nessun altro scrive in parallelo.

## Strumento applicato

AM equivalent (defect register `.brain/autonomous-maintenance/defects/closed/FT-pattern-monitor-rebuild-non-atomico-2026-04-20.md`) con violazione di AC-03 (intent: rebuild atomico). Fix in due step:

- Step 1: avvolgere l'intero blocco (SELECT + loop Python + executemany) in `async with conn.transaction()`. Atomico ma con lock ACCESS EXCLUSIVE su `pattern_stats` per secondi, bloccando scrittori concorrenti.
- Step 2 (dopo seconda review): SELECT + classificazione Python fuori transazione, dentro TX solo TRUNCATE + executemany. Lock ridotto a ~ms.

## Classificazione di chiusura

**A — violazione di AC esistente**. Il piano 2026-04-20 esplicitava il rebuild come operazione atomica nel contesto live; il codice non rispettava l'intent. Defect promosso retroattivamente, chiuso con commit `51147a3` e second-pass fix `51147a3` (iterate giro 2).

## Lezione riusabile

Quando porti logica di scrittura bulk da uno script one-shot a un componente che gira in un sistema live, due requisiti che in one-shot erano impliciti diventano espliciti:

1. **Atomicità**: la scrittura deve essere rollback-able su crash. Non bastano N transazioni autonome.
2. **Durata del lock**: la transazione deve essere il più corta possibile. Lavoro Python pesante (loop di classificazione, trasformazioni, validazioni) sta FUORI dalla transazione. Dentro solo I/O.

Anti-pattern da riconoscere nel port:

- "Copio la funzione dallo script al trainer e cambio solo la signature" — serve riprogettare la sequenza di lock, non copiare.
- "Uso `async with conn.transaction()` e metto tutto dentro" — atomico ma bloccante. Secondo step sempre: restringere la transazione alle sole operazioni I/O.

## Sorgente brain locale

Sorgente: `.brain/autonomous-maintenance/defects/closed/FT-pattern-monitor-rebuild-non-atomico-2026-04-20.md`

Piano di riferimento: `.brain/planning/2026-04-20-pattern-monitor-relabel-retrain.md`
