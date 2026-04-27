---
tipo: architettura
creato: 2026-04-27
aggiornato: 2026-04-27
stato: attivo
tags:
  - progetto/sistema-agentico
  - architettura/servizi
  - prodotto/inventario
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari: []
forma_aggancio: asset
sistema_owner: "[[Sistema-Agentico-Studio]]"
---

# AIOS — Inventario servizi

> [!info] In una frase
> AIOS è composto da **12 servizi** (11 MVP + 1 Phase 10 post-MVP), ciascuno con porta dedicata, contratto API documentato e stato di costruzione tracciato. Inventario verificato il 2026-04-27 contro `~/projects/AIOS Studio/.brain/20-Architettura/Servizi/` e codice in `services/`.

> [!warning] Fonte autoritativa
> La specifica completa di ciascun servizio (eventi, comandi, payload) vive nel `.brain/` locale (`.brain/20-Architettura/Servizi/<nome>.md`). Questa nota è il riassunto navigabile per la conversazione strategica/commerciale.

## Servizi MVP (Phase 4-9, congelati)

| # | Servizio | Porta | Phase intro | Scope |
|---|---|---|---|---|
| 1 | **Event Intake Service** | 8001 | 4 | Normalizzazione intake documenti + Outbox writer |
| 2 | **Orchestration Service** | 8002 | 4 | FSM supervisor, routing task cross-service. Ospita `AIOSSupervisor` (Phase 8, flag `USE_SUPERVISOR=false` di default — vedi ADR-004) |
| 3 | **Document Processing Service** | 8003 | 7 | Estrazione, classificazione, deduplica documenti (chiama `DocumentAgent`) |
| 4 | **Practice Context Service** | 8004 | 4 | Registry cliente/pratica/checklist/contesto. **Espone DB clienti context-dependent** (forma giuridica, ATECO, regime contabile — migration 041_client_complete_profiles) |
| 5 | **Accounting Service** | 8005 | 5 | GL rules, anomaly detection, dataset (chiama `AccountingAgent` con Claude Sonnet 4) |
| 6 | **Workflow Governance Service** | 8006 | 5 | FSM task lifecycle, deadlines, reminders. **Ospita `DeadlineScanner` + `DeadlineEnforcementService`** (alert engine — vedi R7 di [[AIOS-Verifica-Roadmap-Agenti]]) |
| 7 | **Validation Service** | 8007 | 8 | Cross-agent validation, risk scoring, gate decision (chiama `ValidationAgent` con LLM separato VER-002) |
| 8 | **Knowledge Reference Service** | 8008 | (Future) | KB fiscale read-only. Stato: domain + routes + tests presenti, **no auto-update normativo** (vedi R3 di [[AIOS-Verifica-Roadmap-Agenti]]) |
| 9 | **Audit Service** | 8009 | 4 | Append-only logical trail, trace reconstruction |
| 10 | **Human Review Service** | 8010 | 6 | Review task management, approval/override (chiama `ReviewAgent`) |
| 11 | **Tax Compliance Service** | 8012 | 6 | Compliance fiscale, draft, pre-F24, readiness (integrabile con Anthropic) |

## Servizio Phase 10 (post-MVP, gate go-live)

| # | Servizio | Porta | Phase intro | Stato |
|---|---|---|---|---|
| 12 | **GB Integration Service** | 8011 | 10 | Anti-corruption layer file-based verso GBSoftware. **Stato 2026-04-27: scaffolding vuoto** (`services/gb-integration-service/app/main.py:6` ha TODO esplicito, routes vuote) |

## Vincolo architetturale chiave

> [!danger] Anti-corruption layer unico
> **Nessun servizio MVP dipende direttamente da GBSoftware.** L'unico ponte è GB Integration Service (invariante #7 dei contratti). Accounting, Tax Compliance ed Event Intake instradano verso GB Integration in staging/dispatch/receipt/import — **mai scrittura diretta su DB GB, mai dipendenza da API GB non documentate** (Service-API-Contracts-Common.md, ll. 63-64 nel `.brain/`).

## Mappa flussi cross-servizio

- **Intake → classificazione → pratica**: `event-intake → document-processing → practice-context`
- **Accounting flow**: `practice-context → accounting → validation → human-review` (con eventuale `gb-integration` come destinazione finale)
- **Compliance flow**: `practice-context → tax-compliance → validation → human-review` (con vincolo firma cliente — vedi R6 di [[AIOS-Verifica-Roadmap-Agenti]])
- **Deadline flow**: `workflow-governance/DeadlineScanner → orchestration → human-review` (alert proattivi)

## Servizi PARZIALI o ASSENTI da chiudere prima di Phase 10

Da [[AIOS-Verifica-Roadmap-Agenti]]:

- **GB Integration** (R2) — endpoint lettura fatture flusso B
- **Workflow Governance** (R7) — esposizione API deadlines + auto-sync ADE
- **Workflow Governance + Human Review** (R6) — stati `PENDING_CLIENT_SIGNATURE` / `PENDING_CLIENT_APPROVAL`

## Note collegate

- [[Sistema-Agentico-Studio]] — MOC prodotto
- [[AIOS-Architettura-Agenti]] — gli agenti che girano dentro questi servizi
- [[AIOS-Stack-Tecnico]] — stack tecnologico sotto i servizi
- [[AIOS-Verifica-Roadmap-Agenti]] — esito verifica R1-R7
- [[AIOS-MVP-Confine-Operativo]] — scope MVP
- [[Prodotto-Pillar-Delivery-Piloti]] — pillar di appartenenza
