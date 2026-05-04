---
tipo: architettura
creato: 2026-04-28
aggiornato: 2026-04-28
stato: attivo
tags:
  - architettura/eventing
  - architettura/correlation
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
---

# Chiave evento = chiave UNIQUE persistita

> [!info] In una frase
> Ogni chiave veicolata in un payload evento (per join cross-consumer) deve coincidere con una chiave UNIQUE già persistita nello schema del producer — mai un UUID generato al volo nel route e mai scritto in tabella.

## Contesto

Lo Sprint Apprendimento (Phase 11) ha emesso `feedback.free_text.received` con un campo `feedback_event_id` generato dal route HRS (`uuid4()` in `review_views.py`). Quel valore non veniva mai persistito: `FeedbackWriter` (consumer di `human.review.completed`) creava la riga in `learning.feedback_events` con un `feedback_event_id` proprio (`default_factory=uuid4`). L'apply consumer downstream cercava la riga per il primo ID — che non esisteva. **Pipeline AI no-op silenzioso**: evento parte, agent risponde, apply non aggiorna mai nulla, zero errori.

## Pattern

**Regola**: in una catena evento `producer → consumer_A → consumer_B`, la chiave veicolata fra `consumer_A` e `consumer_B` per fare lookup deve essere **una chiave già scritta dal producer in tabella con vincolo UNIQUE**.

In AIOS Studio le chiavi candidate sono:
- `decision_id` su `learning.feedback_events` (UNIQUE) → join HRS apply
- `workflow_id` su `workflow.workflow_instances` (PK) → join cross-service workflow
- `practice_id` su `practice.practices` (PK) → join SEC-003 isolation
- `pattern_signature` su `learning.override_rules` (UNIQUE) → join detection

**Anti-pattern**: il route genera un nuovo UUID per "comodità di tracciamento" e lo mette nel payload senza scriverlo da nessuna parte. Funziona finché c'è solo un consumer; rompe al primo lookup downstream.

## Verifica progettuale (checklist)

Quando si introduce un nuovo evento:
- [ ] La chiave di join nel payload è una colonna UNIQUE della tabella che il producer scrive nella stessa transazione dell'`OutboxWriter`?
- [ ] Esiste un test E2E reale (non composition) che esercita il consumer downstream e fallisce se il lookup non matcha?
- [ ] L'addendum contracts dichiara la chiave come "UNIQUE join key shared across consumers"?

## Sorgente brain locale

Sorgente: review post-merge Sprint Apprendimento Sessione 2+3, finding B1 (commit `3c0839c`, 2026-04-28). Trade-off `feedback_event_id` orfano vs pivot su `decision_id` documentato in `docs/contracts-addendum-phase11-feedback-interpretation-events.md` (NFR-004).

## Note collegate

- [[Arch-Service-Returns-Emitted-Envelope]] — companion pattern (chi emette restituisce envelope)
- [[2026-04-28-test-e2e-composition-non-esercita-route]] — la loss che ha fatto emergere questo pattern
- [[Sistema-Agentico-Studio]]
