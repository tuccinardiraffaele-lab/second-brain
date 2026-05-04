---
tipo: loss
creato: 2026-04-29
aggiornato: 2026-04-29
stato: chiusa
progetto: "[[Sistema-Agentico-Studio]]"
pillar: quality
livello: 1
failure-mode: "trigger manuale via UI apre root envelope su event_type non root-capable, rompendo invariante #5 (correlation explicit) e silenziando il consumer downstream"
classificazione-chiusura: A
tags:
  - loss/correlation
  - loss/contracts
area: prodotto
---

# R1 — Envelope root non root-capable per override manuale

## Fenomeno

Al primo override manuale via UI, il route `clienti_profile.correct_profile_field` apriva un envelope root con `event_type="client.profile.signal_applied"` e `causation_id=None`. Lo schema frozen `event-envelope.schema.json:43-52` enumera 6 root-capable types e `client.profile.*` non è tra questi: l'envelope falliva la validazione, l'outbox relay rifiutava l'evento, il `ObligationRecalculatorConsumer` (T-R1-12) non si attivava. L'intero Blocco D dello sprint sarebbe morto al primo uso del pilot.

## Causa base

Costruzione manuale dell'envelope con `EnvelopeBuilder.build()` su un event_type di dominio (`client.*`), trascurando la regola esplicita di `docs/correlation-lineage-spec.md:63-78` "regola generale per trigger manuali": un'azione manuale non crea un nuovo root solo perché è manuale; va materializzata via uno dei 6 root-capable types (qui `intake.event_received` con `source_type="human"`) e il dominio è derivato via `propagate()`.

## Strumento applicato

UPS — `Phenomenon → Physical → Conditions → 5-Why → Root Cause` su evidenza diretta (codice + schema frozen + matrix doc). Niente azione su supposizione: prima letto schema, poi spec, poi codice esistente di altri trigger manuali per confermare la convenzione (es. `gb.package.received`).

## Classificazione di chiusura

**A — violazione di AC esistente** (invariante #5 + matrice root-creation freezed). Non gap di AC: la regola esisteva da Phase 5, era documentata. È stata semplicemente mancata in fase di scrittura del nuovo route. Defect promosso e chiuso con fix coerente alla spec.

## Lezione riusabile

I trigger manuali del prodotto (UI override, comandi admin, replay tools) **non sono root domain**. Vivono dentro la matrice root-creation come `intake.event_received` con `source_type="human"`. Quando aggiungo un nuovo punto di azione manuale, il template è: (1) materializza l'azione come root `intake.event_received`, (2) deriva il dominio via `propagate()`, (3) entrambi nello stesso commit outbox. Il "tipo di evento di dominio non è mai root-capable" vale anche se il trigger è umano, anzi specialmente.

## Sorgente brain locale

Sorgente: `.brain/autonomous-maintenance/defects/closed/AIOS-Studio-R1-Envelope-Root-Non-Capable-Inv5-2026-04-29.md`
Addendum contracts: `docs/contracts-addendum-r1-manual-correction-root.md`

## Note collegate

- [[Sistema-Agentico-Studio]]
- [[2026-04-28-test-e2e-composition-non-esercita-route]] — altra loss A che dimostra come "test verde" non significhi "comportamento del prodotto verificato": qui il quality loop ha intercettato il bug, lì lo aveva mancato.
