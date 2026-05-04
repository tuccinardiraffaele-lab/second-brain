---
tipo: architettura
creato: 2026-04-28
aggiornato: 2026-04-28
stato: attivo
tags:
  - architettura/test
  - architettura/eventing
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
---

# Test reset — cleanup outbox-aware

## Contesto
In sistemi event-driven con OutboxWriter (vedi Invariante #3 di AIOS), ogni emit di evento crea una entry in `<schema>.outbox_entries` con un `idempotency_key` UNIQUE. Il consumer dedup-pa basandosi su quella chiave. Cancellare le entità di dominio (es. `learning.override_rules`, `learning.promotion_proposals`) **senza** cancellare le entries dell'outbox lascia la chiave occupata: il prossimo emit con stesso fingerprint semantico esplode con `OutboxWriteError: duplicate idempotency_key`, che propaga come HTTP 500 al frontend (sintomo: "il button non funziona").

## Pattern
Ogni script o procedura di reset di stato per test E2E deve enumerare:

1. Tutte le tabelle di dominio toccate dal flusso testato.
2. **Le `outbox_entries` di tutti gli schemi event-emitter coinvolti** (`governance.outbox_entries`, `learning.outbox_entries`, `validation.outbox_entries`, `gb.outbox_entries`...).
3. Idempotency processing markers in Redis se vengono ricostruiti ogni volta (di solito: no, hanno TTL).

Esempio:
```sql
DELETE FROM learning.outbox_entries
 WHERE idempotency_key LIKE 'learning-override-promoted-%';
DELETE FROM learning.knowledge_capture_queue;
DELETE FROM learning.override_rules;
DELETE FROM learning.promotion_proposals WHERE proposal_id = $1;
```

## Detection
Quando si scrive un nuovo cleanup script: per ogni route POST/PATCH che il test esercita, identificare l'outbox emit che produce. Quasi tutti i POST in AIOS che modificano stato emettono un evento — lista delle eccezioni più corta della lista delle regole.

## Trade-off
Cleanup più verboso, ma elimina una classe di falso-bug "il button rotto" che in realtà è cleanup incompleto. La diagnosi del falso-bug costa molto più della verbosità del cleanup.

## Note collegate
- [[Pattern-Outbox-Writer]] (brain locale)
- Sorgente brain locale: `.brain/60-Pattern/Pattern-Test-Reset-Outbox-Aware.md`
- Sessione di emersione: AIOS Studio Phase 10 UI sprint, 2026-04-28.
