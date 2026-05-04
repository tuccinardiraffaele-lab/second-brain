---
tipo: loss
creato: 2026-04-29
aggiornato: 2026-04-29
stato: chiusa
progetto: "[[Sistema-Agentico-Studio]]"
pillar: quality
livello: 1
failure-mode: "str() come serializer universale: produce letterali Python irrecuperabili per collezioni (TEXT[], JSONB), rompendo audit trail e rollback dell'override manuale"
classificazione-chiusura: A
tags:
  - loss/audit
  - loss/serialization
area: prodotto
---

# R1 — `previous_value` registrato come `str(<collezione>)` non recuperabile

## Fenomeno

Il ledger `client_profile_signals.previous_value` registrava il valore precedente via `str(previous)`. Per scalari (TEXT, BOOLEAN, DATE) funzionava. Per colonne collezione — `servizi_attivati` (TEXT[]) e futuri JSONB — `str()` produce letterali Python (`"['CONTABILITA','IVA']"`), non riconvertibili a oggetto. Conseguenza: l'audit trail della prima correzione manuale su un array sarebbe stato inutilizzabile per review umana o per rollback.

## Causa base

`apply_manual_correction()` è stato scritto pensando solo a campi scalari (caso dominante MVP). Il salto a `str()` come serializer "universale" è il bug latente classico: funziona finché qualcuno non gli passa un tipo composito.

## Strumento applicato

Reviewer del giro 1 ha sollevato il caso. Fix con helper `_serialize_previous(value)` che applica `json.dumps(ensure_ascii=False)` ai non-primitivi. **Standardize cross-codebase**: applicato in 3 punti di `profile_enrichment.py` (apply_manual_correction ledger, return per evento, `_insert_signal` automatico) — non solo dove la review aveva pizzicato.

## Classificazione di chiusura

**A — violazione di AC esistente** (audit trail completo come precondizione di review umana). Non gap.

## Lezione riusabile

`str()` è un serializer **per primitivi**, non universale. Quando un valore può essere non-primitivo, usa `json.dumps`. Domanda da porsi prima di chiudere il task: *"questo campo può ricevere list/tuple/dict, oggi o in futuro?"*. Se sì, switch a JSON. Vale per: ledger di audit, payload di evento, log strutturati, cache, persistenza JSONB.

Vale come regola anche durante l'aggiunta di una nuova colonna: se la colonna è array/JSONB, mappa il serializer prima di scrivere il primo INSERT.

## Sorgente brain locale

Sorgente: `.brain/autonomous-maintenance/defects/closed/AIOS-Studio-R1-Previous-Value-Collezioni-Audit-2026-04-29.md`

## Note collegate

- [[Sistema-Agentico-Studio]]
