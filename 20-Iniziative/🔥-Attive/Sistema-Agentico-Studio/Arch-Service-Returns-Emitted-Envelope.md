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

# Service che emette evento restituisce l'envelope emesso

> [!info] In una frase
> Quando un domain service emette un evento via `OutboxWriter` come parte della sua azione, deve restituire la coppia `(record, envelope)` — non solo il record — affinché i caller downstream possano propagare la lineage via `EnvelopeBuilder.propagate(parent=envelope)` invece di costruire envelope shaped come root in violazione del catalog.

## Contesto

`ReviewService.submit_decision()` in HRS emetteva `human.review.completed` ma restituiva solo il `ReviewDecisionRecord`. Il route handler che voleva emettere `feedback.free_text.received` nello stesso flusso non aveva accesso all'envelope appena prodotto: l'unica strada era `EnvelopeBuilder.build(correlation_id=uuid4(), lineage_root_id=uuid4())` che però (a) creava una thread di correlation nuova disconnessa dalla review, (b) violava `root_expectation: non_root_only` dichiarato nel `event-types-catalog.yaml`.

## Pattern

Domain service che emette eventi → firma `def metodo(...) -> tuple[Record, EventEnvelope]`.

Caller downstream:
```python
record, parent_envelope = await service.do_thing(...)
follow_up = EnvelopeBuilder.propagate(
    parent=parent_envelope,
    new_event_type="follow.up.event",
    ...
)
```

**Vincolo correlato (root-creation matrix)**: solo gli event_type elencati in `docs/correlation-lineage-spec.md` possono aprire una nuova thread (`causation_id=null`, `parent_event_id=null`). Tutti gli altri devono essere `propagate()` da un parent. Restituire l'envelope è il meccanismo che rende la regola applicabile in pratica.

## Quando NON applicare

- Se il service è puramente CRUD senza emit → ritorna solo il record.
- Se il service emette N eventi e nessuno è il "principale" → ritorna `tuple[Record, list[EventEnvelope]]` o introduci un wrapper. Caso non ancora visto in AIOS.

## Verifica progettuale

- Test che asserisce `parent_envelope.correlation.correlation_id == follow_up.correlation.correlation_id`
- Test che asserisce `follow_up.correlation.causation_id == parent_envelope.event_id`

## Sorgente brain locale

Sorgente: review post-merge Sprint Apprendimento Sessione 2+3, finding B2 (commit `3c0839c`, 2026-04-28). Modifica firma `submit_decision` in `services/human-review-service/app/domain/review_service.py`; addendum `docs/contracts-addendum-phase11-feedback-interpretation-events.md` aggiornato per riflettere il pattern.

## Note collegate

- [[Arch-Event-Key-Persisted-Unique]] — companion pattern (chiave evento = UNIQUE persistita)
- [[Sistema-Agentico-Studio]]
