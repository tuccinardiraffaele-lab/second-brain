---
tipo: architettura
creato: 2026-04-28
aggiornato: 2026-04-28
stato: attivo
tags:
  - architettura/eventing
  - architettura/llm
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
---

# Hybrid sync/async LLM enrichment

> [!info] In una frase
> Quando il prodotto deve arricchire un evento utente con un'inferenza LLM, **la chiamata LLM non vive nella request HTTP del titolare**: il boundary persiste l'intent in modo strutturato e sincrono, poi un agente specializzato consuma l'evento, chiama il modello, ed emette un secondo evento che un *apply consumer* applica come enrichment idempotente sul record originario.

## Quando applicare

- Una superficie utente (form HTTP, API call) deve restituire una risposta deterministica e veloce, **ma** il prodotto vuole anche una lettura semantica del contenuto inserito (free-text, motivazione libera, descrizione).
- Il valore aggiunto LLM è "signal", non autorità: la decisione utente resta vincolante (HITL), l'inferenza LLM solo arricchisce.
- L'inferenza può essere lenta, parzialmente affidabile (soglia confidence), e non bloccare in nessun caso il flusso principale.

## Forma del pattern

```
[1] HTTP boundary
    ├─ valida payload strutturato (CorrectionPayload o equivalente)
    ├─ persiste record canonico (feedback_event)
    └─ emette evento "raw" via OutboxWriter, stessa TX
                    ↓ (event broker)
[2] Agente LLM (orchestration-service / pari)
    ├─ consuma "raw"
    ├─ redige PII (solo verso LLM, mai sul DB)
    ├─ chiama il modello con prompt strutturato + schema JSON
    ├─ valida output (es. confidence ≥ soglia → OK / FAILED)
    └─ emette evento "interpreted" via OutboxWriter
                    ↓ (event broker)
[3] Apply consumer (sul servizio owner del record)
    ├─ consuma "interpreted"
    ├─ UPDATE idempotente di un sotto-campo dedicato
    │  (es. corrections_payload.ai_interpreted)
    └─ MAI sovrascrive l'intent esplicito dell'utente (HITL)
```

Tre eventi, tre consumer, una transazione per ciascun stage.

## Invarianti vincolanti

1. **Boundary HTTP non chiama LLM**. Mai. Il timeout HTTP non deve essere influenzato dalla latenza del modello.
2. **Persist before emit**. Il record canonico è scritto prima dell'evento "raw" — `OutboxWriter` nella stessa TX della scrittura DB.
3. **Idempotency esplicita**. Sia il consumer LLM (`interp-{record_id}`) sia l'apply consumer (`apply-{record_id}`) hanno chiavi deterministiche derivate dall'id del record, non dall'event_id.
4. **PII redaction asimmetrica**. Regex CF/PIVA/IBAN si applicano *solo* sul prompt verso il modello. Il payload persistito mantiene il testo grezzo per audit.
5. **Confidence gate al consumatore LLM**. Sotto soglia → status `FAILED` con `reasoning` esplicito; mai best-effort silenzioso.
6. **HITL preservato dall'apply consumer**. L'UPDATE tocca SOLO il sotto-campo dedicato all'AI (`ai_interpreted`). La decisione utente nel record canonico resta intoccabile.
7. **Lineage propagato**. `EnvelopeBuilder.propagate()` su entrambi gli eventi: la chain è "raw → interpreted" dentro la stessa correlazione del record originario.

## Quando NON applicare

- L'inferenza LLM è bloccante per la decisione utente → serve un agente sincrono dentro la request, non questo pattern.
- Il modello deve agire (write, dispatch, tool use) e non solo arricchire → si entra nel territorio supervisor-led con FSM guard, fuori scope qui.
- Volumi triviali (poche unità/giorno) e nessuna richiesta latenza percepita → KISS: chiama l'LLM in foreground, niente eventing.

## Conseguenze

- **Positive**: latenza percepita utente costante (no LLM nel critical path); resilienza a downtime modello (gli eventi `raw` si accumulano, l'agente recupera al rientro); osservabilità separata dei tre stage; possibilità di disabilitare l'enrichment senza toccare il flusso principale.
- **Negative**: tre transazioni anziché una; possibile scrittura iniziale del record con sotto-campo AI in stato `PENDING` visibile in UI prima del completamento.
- **Da monitorare**: ratio di eventi `raw` consumati vs interpreted con `OK` (proxy della qualità del modello su questa surface); latenza p95 `raw → apply` (se cresce, la surface diventa "stale" agli occhi utente).

## Implementazione AIOS Studio

Sprint Apprendimento Sessione 2 (T8-T10):

- Boundary: `services/human-review-service/app/api/routes/review_views.py`, route `POST /reviews/{id}/decide` — persiste `validation.review_decisions` + `learning.feedback_events`, emette `feedback.free_text.received` quando `free_text_motivation` presente.
- Agente: `agents/feedback_interpreter_agent.py` (Claude Sonnet 4.6, soglia 0.7) + `services/orchestration-service/app/consumers/feedback_interpretation_consumer.py` — emette `feedback.free_text.interpreted`.
- Apply: `services/human-review-service/app/consumers/feedback_interpretation_consumer.py` — UPDATE idempotente (`jsonb_set`) di `learning.feedback_events.corrections_payload.ai_interpreted`.

Schemi e contratti: `packages/contracts/events/payload-schemas/feedback.free_text.received.v1.schema.json`, `feedback.free_text.interpreted.v1.schema.json`, namespace `feedback` nel catalog. Documento di riferimento runtime: `docs/contracts-addendum-phase11-feedback-interpretation-events.md`.

## Sorgente brain locale

Sorgente: pattern emerso durante Sprint Apprendimento Sessioni 2-3, vedi `.brain/90-Sessioni/Session-Summary-Latest.md` (sezione "Sprint chiuso") e `.brain/30-Decisioni/ADR-008-Phase11-Sprint-Apprendimento.md`.

## Note collegate

- [[Sistema-Agentico-Studio]]
