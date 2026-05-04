---
tipo: architettura
creato: 2026-04-28
aggiornato: 2026-04-28
stato: attivo
tags:
  - architettura/automation
  - architettura/knowledge-management
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
---

# Idempotent generated artifact with preservation markers

> [!info] In una frase
> Quando uno script genera artefatti (note, doc, config) che il founder può poi annotare a mano, **il blocco rigenerabile vive dentro marker espliciti** (`<!-- aios:auto:start --> ... <!-- aios:auto:end -->`): il re-run sostituisce solo quel blocco e preserva tutto il resto, con un controllo hash che evita scritture inutili.

## Quando applicare

- Esiste uno script automatico che produce contenuto strutturato (frontmatter + body) a partire da dati canonici (DB, API).
- L'output convive con annotazioni umane successive: il founder legge la nota, aggiunge contesto, esempi, riflessioni — e si aspetta che alla prossima generazione **non venga sovrascritto**.
- Il re-run dello script deve essere sicuro: nessuna duplicazione, nessuna perdita, nessun side effect su contenuto già allineato.

## Forma del pattern

```
file.md (esistente):
  ---
  <frontmatter umano + automatico>
  ---

  <!-- aios:auto:start -->
  <sezione rigenerata ad ogni run>
  <!-- aios:auto:end -->

  <annotazioni umane libere — preservate>
```

Algoritmo di upsert:

1. **Frontmatter**: sostituito interamente a ogni run (campi canonici come `override_rule_id`, `pattern_signature`, `promoted_at` sono autoritativi dal DB).
2. **Auto-block**: regex `<!-- aios:auto:start -->.*?<!-- aios:auto:end -->` (DOTALL) → sostituzione 1:1 del blocco. Se i marker sono assenti (caso file appena creato), il blocco viene appended in testa al body.
3. **Resto del body**: invariato. Tutto ciò che vive **fuori** dai marker è patrimonio umano.
4. **Hash gate**: prima di scrivere, calcolo `sha256` del contenuto risultante; se uguale a quello attuale, no-op (skip print). Evita rumore in `git diff` per re-run identici.

## Invarianti vincolanti

1. **Marker stabili nel tempo**. Cambiare il loro testo letterale è una breaking change: tutti i file esistenti perdono protezione. Versionare i marker (`<!-- aios:auto:v1:start -->`) solo se davvero serve evolverli.
2. **Mai scrivere fuori dai marker**. Lo script *non* può creare sezioni umane "consigliate". Le annotazioni nascono dall'utente, non dallo script.
3. **Frontmatter autoritativo dal data source**. Il founder non deve modificare a mano i campi che lo script rigenera; se un campo è "umano", non deve stare nel frontmatter generato dallo script.
4. **Hash check su contenuto finale, non su body**. Include frontmatter rigenerato. Garantisce no-op solo quando *tutto* è identico.
5. **Atomicità di scrittura**. Read → compute → write in unico step. Niente write parziale: se lo script crasha a metà, la nota resta consistente con la run precedente.
6. **Output umano-leggibile dell'esecuzione**. Per ogni file: `WROTE` / `SKIP` / `MARKED` (status DB) — il founder vede subito cosa è cambiato prima di `git add`.

## Quando NON applicare

- L'artefatto è 100% generato e non riceverà mai annotazioni umane → semplifica: rigenera tutto il file ogni run, niente marker.
- Più producer concorrenti scrivono nello stesso file → serve locking esterno o un solo writer canonico, i marker non sono sufficienti.
- L'artefatto è schema-strict (es. `package.json`) → strumento dedicato (`json-canvas`, `obsidian-bases`), non text-merge a marker.

## Conseguenze

- **Positive**: il founder può annotare le note senza paura di perderle al re-run; lo script è davvero idempotente; il `git diff` resta pulito su run identici; nessun lock/state esterno serve per gestire la concorrenza con l'editing umano.
- **Negative**: lo script deve fare un parse minimo del file esistente prima di scriverlo (cost trascurabile per file <1MB); marker visibili nel sorgente (cosmetica accettabile per `.md`, scomoda per file binari).
- **Da monitorare**: drift della forma frontmatter — se il founder edita un campo "autoritativo" pensando che resti, lo script lo sovrascrive al prossimo run. Mitigazione: documentare in runbook ([[Runbook-Knowledge-Capture-Writer]] equivalente) che cosa è auto e cosa è umano.

## Implementazione AIOS Studio

Sprint Apprendimento Sessione 3 (T11): `scripts/knowledge_capture_writer.py`.

- Marker: `<!-- aios:auto:start -->` / `<!-- aios:auto:end -->` (vedi costanti `MARKER_START`, `MARKER_END`).
- Funzioni: `upsert_note_content(existing, frontmatter, auto_body)` per il merge, `write_note_idempotent(path, frontmatter, auto_body)` per il dispatch I/O con hash check.
- Test unit: `tests/test_knowledge_capture_writer.py` copre creazione, replace, preservazione testo umano, no-op su contenuto identico.
- Runbook operativo: `.brain/50-Operativo/Runbook-Knowledge-Capture-Writer.md`.

## Sorgente brain locale

Sorgente: pattern emerso durante Sprint Apprendimento Sessione 3 T11, vedi `.brain/30-Decisioni/ADR-008-Phase11-Sprint-Apprendimento.md` (sezione "Eccezione esplicita su skill `obsidian-markdown`") e `.brain/50-Operativo/Runbook-Knowledge-Capture-Writer.md`.

## Note collegate

- [[Sistema-Agentico-Studio]]
- [[Arch-Hybrid-Sync-Async-LLM-Enrichment]]
