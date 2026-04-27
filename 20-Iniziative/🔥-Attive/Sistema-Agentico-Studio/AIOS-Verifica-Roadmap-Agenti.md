---
tipo: progetto
creato: 2026-04-13
aggiornato: 2026-04-27
stato: attivo
tags:
  - progetto/sistema-agentico
  - azione-aperta
  - verifica-repo
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
prossima_azione: "Chiudere R6 (firma cliente) + R2 (lettura GB) + R7 (API deadlines) prima di Phase 10"
blocco: ""
---

# Verifica roadmap agenti AIOS

> [!success] Verifica codice eseguita 2026-04-27
> I 7 requisiti sono stati verificati nel codice tramite Explore mirato. Esito: **R1 OK / R3 e R7 PARZIALE / R2, R4, R5, R6 ASSENTE**. Bloccanti per go-live 2026-05-10: **R2, R6, R7**. Dettaglio per requisito (citazioni `file:line`) in `~/projects/AIOS Studio/.brain/00-Bridge/Phase-10-Guardrail-Architettura.md`. Questa nota mantiene il **perché** (intuizioni e gap originali); lo stato di implementazione vive nel guardrail.

## Esito sintetico per requisito

| ID | Requisito | Stato | Bloccante go-live |
|---|---|---|---|
| R1 | DB clienti context-dependent (forma giuridica, attività, regime) | **OK** — migration 041 | — |
| R2 | Lettura fatture GB (flusso B / SDI diretto) | **ASSENTE** — `gb-integration-service` vuoto | **SÌ** se >50% volume |
| R3 | Strato 1 vault baseline | **PARZIALE** — domain+routes ok, no auto-update normativo | NO (sì per pitch B2C/B2B) |
| R4 | Override + retrofeedback umano | **ASSENTE** — no tabelle feedback | NO (decidere policy ora) |
| R5 | Retraining threshold (Optuna) | **ASSENTE** — soglia hardcoded 0.85 | NO (post-MVP esplicito) |
| R6 | Validation gate firma cliente | **ASSENTE** — FSM senza stati attesa firma | **SÌ** per dichiarativi/bilanci |
| R7 | Alert engine scadenze | **PARZIALE** — DeadlineScanner ok, no API + no auto-sync | **SÌ** (soglia pilot #3) |

> [!info] Sorpresa positiva
> R1 (DB clienti) era dato per "non verificato" e si temeva fosse il primo gap bloccante. **È OK**: la migration `041_client_complete_profiles` espone `natura_giuridica`, `codice_ateco_primario` + `secondari[]`, `regime_contabile` enum. Resta solo la domanda di popolamento per i 10 pilot, da chiudere alla 2ª intervista padre.

---

## Punti originali (verificati e non) — conservati per traccia storica

### 1. Agente finanziario / advisory

**Intuizione originale del founder**: agente che, sulla base dei risultati dell'AccountingAgent, suggerisce al cliente finale leve fiscali e insight per migliorare la sua situazione finanziaria.

**Stato attuale dichiarato**: accorpato in parte in FiscalAgent e in parte in AccountingAgent.

**Da verificare**:

- È davvero accorpato (e come), o è stato droppato e dimenticato?
- Ha senso rifarlo come agente a sé post-MVP?
- Il nome "finanziario" è quello giusto? Advisory? Tax-planning?

**Quando**: deep dive post-MVP, al primo giro di consolidamento.

### 2. Agente consulenza del lavoro

**Intuizione del founder**: esiste un altro agente pensato per la gestione della consulenza lavorativa (busta paga, F24, dichiarazioni, adempimenti lavoristici).

**Stato attuale nel brain**: cercando `lavoro`, `labor`, `payroll`, `consulen.*lavor` nel `.brain/` → **nessuna menzione**. Il progetto nella sua descrizione ufficiale include "consulenza lavoro" come bounded context, ma non c'è un agente dedicato né nei file `agents/` né nel roadmap tracciato (Next-Steps.md fino a Phase 13+).

**Da verificare**:

- Esiste davvero in un documento che ho perso? Dove?
- Oppure è un agente pensato ma mai scritto nel brain?
- Se non c'è, va aggiunto formalmente alla roadmap.

### 3. "Roadmap ristrutturata" indicata dal founder

**Cosa è stato detto in intervista**: esiste una roadmap ristrutturata nel repo, "verso metà-fine file" di qualche documento.

**Cosa ho cercato**: `.brain/02-project/Next-Steps.md` (fine file = carryover Phase 10), `.brain/02-project/Overview.md`, `.brain/02-project/Current-State.md`, README, AGENTS.md, CLAUDE.md.

**Cosa ho trovato**: il Next-Steps elenca Phase 10..13+ ma nella parte alta; la parte media-finale è dedicata alle task Phase 9. Nessuna sezione chiamata "roadmap ristrutturata". *Da rivisitare dopo redesign brain locale del 2026-04-27 (la struttura `.brain/` è cambiata).*

### 4. Copertura del flusso B — fatture via SDI direttamente in GBSoftware → R2

**Verificato 2026-04-27**: ASSENTE. `services/gb-integration-service/app/main.py:6` ha TODO esplicito; routes vuote. Vedi guardrail Phase 10.

### 5. Struttura del DB clienti — campi necessari per classificazione context-dependent → R1

**Verificato 2026-04-27**: OK. Migration `data/migrations/versions/041_client_complete_profiles.py:32-50` espone i 3 campi. Resta da verificare popolamento per i 10 pilot.

### 6. Retraining automatico del threshold di confidenza → R5

**Verificato 2026-04-27**: ASSENTE. Nessun Optuna in `pyproject.toml`, soglia hardcoded `0.85` in `agents/validation_agent.py:28`. Da esplicitare post-MVP nella roadmap.

## Domande aperte (da chiudere alla 2ª intervista padre, 2026-05-03)

Da [[AIOS-Intervista-Padre-Follow-Up]] e dalla verifica codice:

- **R1**: regime contabile dei 10 pilot — chi popola e quando?
- **R2**: % volume fatture via flusso B vs flusso A sui 10 pilot?
- **R4**: override generalizza tra clienti simili o resta per-cliente?
- **R6**: per quali tipi di output (oltre dichiarativi e bilanci) è obbligatoria la firma cliente?
- Quadratura trimestrale: passi operativi (Lean mapping)
- Bus-factor persona-per-persona

## Azioni concrete prossime 48h

In ordine di blocco al go-live 2026-05-10:

- [ ] **R6** — Aggiungere stati `PENDING_CLIENT_SIGNATURE` / `PENDING_CLIENT_APPROVAL` in FSM (`packages/workflow-sdk/aios_workflow/transitions.py`) + gate in `workflow-governance-service` + evento firma in `human-review-service`
- [ ] **R2** — Stub route `GET /invoices/inbound` in `gb-integration-service` + consumer per `gb.invoice.received`
- [ ] **R7** — Endpoint `GET /practices/{practice_id}/deadlines/upcoming` + `POST /deadlines/reminders/emit` + scheduler mensile per `sync-ade-calendar.py` in `lifespan.py`

## Collegamenti

- [[Sistema-Agentico-Studio]] — MOC prodotto
- [[Prodotto-Vault-Substrato-Di-Prodotto]] — architettura a 3 strati
- [[AIOS-Brainstorm-Knowledge-Map-Padre]] — fonte dei gap 4, 5, 6
- [[AIOS-Intervista-Padre-Domande-KB]] — pain e soglie originali
- [[AIOS-Intervista-Padre-Follow-Up]] — 2ª intervista 2026-05-03
- [[KR1.1 — Phase 10 GBSoftware completata]]
- [[KR1.2 — Metriche pilot fissate con padre]]
