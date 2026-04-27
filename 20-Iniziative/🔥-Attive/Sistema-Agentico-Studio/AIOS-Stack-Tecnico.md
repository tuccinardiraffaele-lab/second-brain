---
tipo: architettura
creato: 2026-04-27
aggiornato: 2026-04-27
stato: attivo
tags:
  - progetto/sistema-agentico
  - architettura/stack
  - prodotto/tecnologia
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari: []
forma_aggancio: asset
sistema_owner: "[[Sistema-Agentico-Studio]]"
---

# AIOS — Stack tecnico

> [!info] In una frase
> Stack Python event-driven con eventing Redis Streams + Outbox pattern + DLQ partizionato, persistenza PostgreSQL + MinIO per documenti, LLM **Anthropic-only** (Sonnet 4 + Haiku 4.5), orchestrazione FSM-driven con Supervisor LLM-overlay opzionale (default OFF). Verificato il 2026-04-27 contro `~/projects/AIOS Studio/`.

> [!warning] Perché serve nel vault
> Il pitch di AIOS verso il padre, eventuali partner, futura conversazione B2B/B2C, deve poggiare su una descrizione tecnica accurata. Una nota che dice "5 agenti rule-based" mentre il codice ha 5 agenti LLM-based brucia credibilità al primo confronto serio.

## Linguaggi e framework

- **Python 3.11**
- **FastAPI** per API HTTP per servizio
- **asyncpg** per accesso async a PostgreSQL
- **Pydantic** per schema/DTO

## Persistenza

| Storage | Versione | Uso |
|---|---|---|
| **PostgreSQL** | 16 | Stato applicativo, ledger, FSM, registry pratiche/clienti, audit trail |
| **Redis** | 7 | Streams (eventing), consumer groups, idempotency middleware, cache |
| **MinIO** | RELEASE.2025-01-20 | Object storage per documenti (bucket `aios-documents`) — S3-compatible |

## Eventing pattern

- **Redis Streams** con prefisso `aios.*` (stream prefix configurabile via `RedisSettings`)
- **Outbox Writer pattern**: nessun `XADD` diretto — emissione eventi via `OutboxWriter(schema=...)` (ADR-001)
- **DLQ partizionato per service** con fallback `aios.dlq` (ADR-002)
- **Consumer Idempotency Middleware**: dedup su retry safety
- **Outbox Relay**: running in lifespan dei servizi (`accounting-service`, `orchestration-service`, `workflow-governance-service`)

## LLM

> [!tip] Anthropic-only
> Nessun provider alternativo cablato. Modelli specifici per agente:

| Servizio / agente | Modello |
|---|---|
| `accounting-service` (AccountingAgent) | `claude-sonnet-4-20250514` |
| `orchestration-service` (`AIOSSupervisor`) | `claude-haiku-4-5-20251001` |
| `validation-service` (ValidationAgent) | Anthropic supportato |
| `tax-compliance-service` | AsyncAnthropic integrabile |

Dipendenza dichiarata: `anthropic>=0.39,<1.0` (`pyproject.toml`).

**Vincolo NFR-001**: nessun framework di orchestrazione esterno (no LangGraph/CrewAI/AutoGen) — chiamate dirette ad `AsyncAnthropic`.

## Pattern di orchestrazione

- **FSM service-layer** (Phase 0-7, modalità default): `WorkflowDispatchConsumer` → lookup PostgreSQL → route a 12 handler hardcoded → emit via OutboxWriter
- **Supervisor LLM overlay** (Phase 8+, opt-in): LLM propone azione, FSM valida, escalation se invalido. **Flag `USE_SUPERVISOR=false` di default** (ADR-004) — il Supervisor NON è il coordinatore principale di produzione, è un overlay A/B
- **Reasoning Trace Repository**: cablato in `orchestration-service` per storia decisioni

## Variabili d'ambiente principali

```
# LLM
ANTHROPIC_API_KEY                # accounting + orchestration (Supervisor)
ANTHROPIC_MODEL                  # default=claude-sonnet-4-20250514
ANTHROPIC_ENABLED                # boolean flag

# DB
DATABASE__HOST / PORT / NAME / USER / PASSWORD

# Redis
REDIS__HOST / PORT / PASSWORD / DB

# MinIO
MINIO__ENDPOINT / ACCESS_KEY / SECRET_KEY / BUCKET

# Supervisor (Phase 8+)
USE_SUPERVISOR                   # default false
SUPERVISOR_DRY_RUN
SUPERVISOR_MODEL
```

## Red flag pre-go-live (verificati 2026-04-27)

> [!warning]
> 1. **`ANTHROPIC_API_KEY` con fallback silenzioso** (default `""` in `accounting-service/app/config.py:14` e `document-processing-service/app/config.py:13`) — il sistema non urla se manca
> 2. **Strategia migrazioni Alembic non documentata** — schema DB non versionato in modo riproducibile (vedi [[AIOS-Rischi-Pilot]] dopo sanitizzazione)
> 3. **GB Integration Service** = scaffolding vuoto (vedi [[AIOS-Servizi-Inventario]]) — bloccante Phase 10

## Note collegate

- [[Sistema-Agentico-Studio]] — MOC prodotto
- [[AIOS-Servizi-Inventario]] — i servizi che usano questo stack
- [[AIOS-Architettura-Agenti]] — gli agenti che chiamano l'LLM
- [[AIOS-Architettura-Tre-Strati]] — strato 3 (agenti) si appoggia su questo stack
- [[AIOS-Verifica-Roadmap-Agenti]] — esito verifica R1-R7
- [[Prodotto-Pillar-Delivery-Piloti]] — pillar di appartenenza
