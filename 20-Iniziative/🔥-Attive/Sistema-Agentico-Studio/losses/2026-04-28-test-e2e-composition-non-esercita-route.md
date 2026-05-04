---
tipo: loss
creato: 2026-04-28
aggiornato: 2026-04-28
stato: chiusa
progetto: "[[Sistema-Agentico-Studio]]"
pillar: Quality
livello: 2
failure-mode: Test dichiarati "E2E" che mockano repo + agent senza chiamare il route reale lasciano passare bug critici nel route stesso (qui: pipeline AI no-op silenzioso)
classificazione-chiusura: A
tags:
  - loss/test-strategy
  - loss/quality-pillar
area: prodotto
---

## Fenomeno

Lo Sprint Apprendimento Sessione 3 ha consegnato `test_sprint_apprendimento_e2e.py` (9 test) presentato come copertura E2E di AC #4-#6 #10. Review post-merge ha rivelato che AC #6 ("interpreted event turns ai_interpreted.status to OK") era violato in produzione da un bug di chain (`feedback_event_id` orfano fra route → FeedbackWriter → apply consumer): nessun test l'ha intercettato.

I 9 test "E2E" facevano:
- Asserzioni su `payload.free_text_present()` (unit method)
- Mock di `LearningRepository.update_feedback_ai_interpreted` (skipping il join reale)
- Asserzioni su `to_corrections_dict()` (model method)

**Nessuno chiamava `POST /reviews/{id}/decide`**. Il bug B1 viveva esattamente dentro il body del route handler, non rilevabile da nessun mock-based composition test.

## Causa base

Ambiguità tassonomica: "E2E" usato come sinonimo di "composition" o "integration mock". Il file di test era unit-camuffato:
1. Stessi mock e stub dei test unit
2. Nessun client HTTP reale (no `httpx.AsyncClient` o equivalent)
3. Nessuna invocazione della stessa funzione che gira in produzione

Conseguenza: copertura percepita > copertura reale. Il defect register e la chiusura del Quality Pillar Sprint Apprendimento hanno calcolato similarità AC ≥99% basandosi su test che non erano test del comportamento dichiarato.

## Strumento applicato

UPS — fenomeno: "AC #6 rotto in produzione, nessun test fallisce". 5-Why su condizione "i test passano ma la pipeline non funziona":
1. Perché passano? Mockano i collaboratori dove il bug vive.
2. Perché mockano? Convenienza: niente DB, niente Redis, niente HTTP.
3. Perché chiamarli "E2E"? Coprivano la "composizione di tutti i moduli" — etichetta auto-attribuita.
4. Perché nessuno l'ha contestato? Il defect register Quality Pillar non ha un check su "il test esercita davvero la stessa funzione di produzione?".
5. **Causa modificabile**: regola di processo mancante: un test che NON chiama almeno una funzione presente nello stack di produzione (route handler, consumer.handle, scheduled job entry) **non è E2E**, è composition.

## Classificazione di chiusura

**A — violazione AC esistente.** AC #6 era dichiarato e violato. Fix-committato in `3c0839c` con:
- Pivot `decision_id` lungo la catena evento (root cause B1)
- `submit_decision` ritorna envelope per propagation (B2)
- Apply consumer raise on no-row-matched (B3)
- Nuovo `test_decide_route_e2e.py` che chiama davvero `submit_decision_form` con `OutboxWriter` spy

Defect non aperto formalmente in `.brain/autonomous-maintenance/defects/closed/` perché la review ha applicato fix + test in un unico ciclo UPS senza materializzare ticket intermedio. Tracciato qui come storico.

## Lezione riusabile

**Definizione operativa**: un test è E2E **solo se** invoca almeno una funzione che è anche entry point di produzione (route handler FastAPI, `EventConsumerBase.handle`, CLI entry, scheduled job tick). Tutto il resto è composition o integration shallow.

**Check da aggiungere al Quality Pillar Gate 3**: per ogni AC numerato, identificare il **punto di entrata in produzione** che lo realizza, e verificare che almeno un test lo invochi direttamente. Se non esiste, il Gate 3 non passa.

**Anti-pattern di naming**: file `*_e2e.py` con import di `unittest.mock.AsyncMock` per il collaboratore principale è un red flag — quasi certamente è composition, non E2E.

## Sorgente brain locale

Sorgente: review post-merge Sprint Apprendimento Sessione 2+3 (commit `3c0839c`, 2026-04-28). Finding H2 nel report del reviewer subagent. Fix in `services/human-review-service/tests/test_decide_route_e2e.py` (nuovo file, 2 test che esercitano `submit_decision_form` direttamente con `OutboxWriter` spy).

## Note collegate

- [[Arch-Event-Key-Persisted-Unique]] — root cause architetturale che il test E2E vero avrebbe trovato
- [[Arch-Service-Returns-Emitted-Envelope]] — fix di propagation conseguente
- [[Sistema-Agentico-Studio]]
