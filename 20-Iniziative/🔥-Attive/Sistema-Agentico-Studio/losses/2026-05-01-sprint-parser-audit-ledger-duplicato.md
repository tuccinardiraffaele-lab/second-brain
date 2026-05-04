---
tipo: loss
creato: 2026-05-01
aggiornato: 2026-05-01
stato: chiusa
progetto: "[[Sistema-Agentico-Studio]]"
pillar: quality
livello: 1
failure-mode: "tabella history-shaped (no UNIQUE applicativo) scritta da producer che non gestisce dedup → replay duplica righe → consumer policy-driven ricomputa cross-fonte e auto-elimina i propri duplicati con motivo policy_override:{stesso_agente}"
classificazione-chiusura: A
tags:
  - loss/idempotency
  - loss/data-modeling
  - loss/sprint-parser-estensione
area: prodotto
---

# Sprint Parser Estensione — Audit ledger duplicato senza dedup

## Fenomeno

Step 5 dello sprint ha aggiunto `_insert_field_extraction_audit` in `ProfileEnrichmentService` per chiudere il gap D-5 (tracciabilità fonte Phase 10). Il method esegue `INSERT INTO practice.client_field_extractions (...)` senza `ON CONFLICT` né dedup applicativo. Ad ogni replay (DLQ replay manuale, retry HTTP su `apply_manual_correction`) si scrivono righe duplicate per stesso `(client_id, campo, document_id, agente)`. Il `ProfileFieldMergeConsumer` policy-driven le carica come N proposte concorrenti dello stesso agente, le ordina per tie-break su `extraction_id`, applica la più recente e declassa le altre N-1 a RIFIUTATA con motivo `policy_override:profile_enrichment_consumer` — auto-override di se stesso.

## Causa base

Modello dati `client_field_extractions` (migration 050) è **history-shaped**: le proposte storiche RIFIUTATA restano per audit, indici NON-unique su `(client_id, campo)`. Implica che chi scrive deve gestire idempotency applicativo. Lo Step 5 ha trattato `_insert_field_extraction_audit` come "side effect tracciabilità" gemello di `client_profile_signals` (che invece ha `UNIQUE (client_id, signal_key, source_document_id)` con `ON CONFLICT DO UPDATE`), assumendo simmetria che il modello dati non garantisce.

## Strumento applicato

UPS livello 1 durante review giro 1. Fix in due livelli:
- **Modello dati**: nuova migration `056_client_field_extractions_audit_unique.py` con partial unique index `(client_id, campo, COALESCE(document_id, '00000000-...'::uuid), agente) WHERE stato='APPLICATA'`. Le proposte RIFIUTATA history restano consentite.
- **Codice applicativo**: `_insert_field_extraction_audit` ora usa `ON CONFLICT (...) WHERE stato='APPLICATA' DO NOTHING` inferendo l'index della migration. Costante condivisa `_FIELD_EXTRACTIONS_NULL_UUID` con commento di sync.

## Classificazione di chiusura

**A** — violazione AC D-5 (ogni campo profilo riconducibile a UNA fonte univoca). Defect chiuso con fix applicato in giro 1.

## Lezione riusabile

> *Quando un modello dati è "history-shaped" (audit log, ledger eventi), il vincolo di unicità per riga "corrente" è responsabilità di chi scrive, non emerge dallo schema. Replay-safety richiede o partial unique index (DB) + ON CONFLICT (codice), o dedup applicativo SELECT-prima-di-INSERT (più fragile).*

Pattern: prima di aggiungere un INSERT nuovo a una tabella esistente, verificare la **gerarchia di idempotency**: c'è già un vincolo unique che protegge il replay? Se no, il producer è da solo. Una nuova fonte di proposte è un cambio di modello, non solo di codice.

## Sorgente brain locale

Sorgente: `.brain/autonomous-maintenance/defects/closed/AIOS-Studio-Sprint-Parser-Estensione-Audit-Ledger-Duplicato-2026-05-01.md`
