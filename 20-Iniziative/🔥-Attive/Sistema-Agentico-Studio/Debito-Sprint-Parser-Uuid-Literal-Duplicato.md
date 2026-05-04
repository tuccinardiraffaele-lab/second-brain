---
tipo: debito-tecnico
creato: 2026-05-01
aggiornato: 2026-05-01
stato: attivo
tags:
  - debito/data-modeling
  - debito/sprint-parser
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
gravità: bassa
costo-stimato: 1-2 ore (refactor con costante condivisa via package)
---

# UUID null literal duplicato tra migration e codice runtime

## Contesto

Il partial unique index su `practice.client_field_extractions` (migration 056) usa `COALESCE(document_id, '00000000-0000-0000-0000-000000000000'::uuid)` per gestire il caso `document_id IS NULL` (manual_override non ha documento sorgente). L'`ON CONFLICT` in `_insert_field_extraction_audit` deve usare lo stesso literal per inferire l'index.

## Forma del debito

Il literal `'00000000-0000-0000-0000-000000000000'::uuid` compare in due posti:
- `data/migrations/versions/056_client_field_extractions_audit_unique.py:38`
- `services/practice-context-service/app/domain/profile_enrichment.py:_FIELD_EXTRACTIONS_NULL_UUID`

Mitigazione attuale: costante nel modulo applicativo + commento esplicito di sync con la migration.

## Perché è debito

Se qualcuno cambia uno dei due (es. usa un UUID diverso per leggibilità) e non l'altro, l'`ON CONFLICT` non infera più l'index → tornano i duplicati silenziosi che la migration 056 doveva eliminare. Il sync è solo testuale (commento), non runtime-enforced.

## Costo accettato

La migration è frozen storico (rule `migrations.md`), non si può importarla dal codice runtime. Le opzioni di refactor pulito (costante condivisa in package neutro, generazione SQL da template) costano più della mitigazione attuale dato il rischio basso (chi tocca uno dei due dovrebbe accorgersi del commento in review PR).

## Quando promuovere a fix

- Se il literal viene cambiato e si scopre il sync rotto in produzione (segnale: duplicati ricompaiono).
- Se serve estendere il pattern partial-unique-with-null-default ad altre tabelle (allora vale il refactor a costante condivisa).

## Sorgente brain locale

Sorgente: `.brain/30-Decisioni/Trade-Off-Log-Sprint-Parser-Estensione.md` TO-1
