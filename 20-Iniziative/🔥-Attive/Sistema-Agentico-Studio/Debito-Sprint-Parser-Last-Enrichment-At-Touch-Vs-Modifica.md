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
costo-stimato: 2-4 ore (aggiungere colonna `last_value_change_at` + migration + UPSERT condizionale)
---

# `last_enrichment_at` semantica "ultimo touch" vs "ultima vera modifica"

## Contesto

`ProfileFieldMergeConsumer._apply_to_profile` esegue UPSERT su `client_complete_profiles` con `ON CONFLICT DO UPDATE SET {campo} = EXCLUDED.{campo}, last_enrichment_at = now(), updated_at = now()`. Il timestamp `last_enrichment_at` viene aggiornato anche quando il valore del campo NON cambia (riapplica lo stesso valore).

## Forma del debito

Semantica attuale: **ultimo touch enrichment** = "qualcuno ha confermato/applicato un valore per questo profilo, anche se identico al precedente".

Ipotetica semantica futura: **ultima vera modifica** = "il valore di una colonna è davvero cambiato".

Le due semantiche divergono su: ricomputo di una proposta che riconferma il valore esistente; replay idempotente di un evento già processato.

## Perché è debito

Oggi non sappiamo quale semantica servirà alla UI / report del padre. La UX del pilot potrebbe rivelare che:
- "Ultimo aggiornamento = oggi" su profilo che non cambia da settimane è rumoroso e fuorviante.
- Oppure è quello che il padre vuole ("oggi qualcuno ha guardato questo cliente", segnale di attività).

## Costo accettato

Lasciamo "ultimo touch" come semantica iniziale. Se servirà la seconda, introdurre colonna `last_value_change_at` con UPDATE condizionale `SET last_value_change_at = CASE WHEN {campo} IS DISTINCT FROM EXCLUDED.{campo} THEN now() ELSE last_value_change_at END`.

## Quando promuovere a fix

- Feedback pilot: "perché il profilo dice aggiornato oggi quando non è cambiato niente?"
- Implementazione UI tracciabilità (Sprint successivo, fuori scope MVP) che ha bisogno di distinguere i due timestamp.

## Sorgente brain locale

Sorgente: `.brain/30-Decisioni/Trade-Off-Log-Sprint-Parser-Estensione.md` TO-2
