---
tipo: architettura
creato: 2026-05-01
aggiornato: 2026-05-01
stato: attivo
tags:
  - architettura/eventing
  - architettura/data-merge
  - architettura/sprint-parser
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
---

# Field priority policy framework — merge multi-fonte deterministico

> [!info] In una frase
> Il `ProfileFieldMergeConsumer` decide il vincitore di ogni `(client_id, campo)` ricomputando lo stato globale su tutte le proposte attive secondo policy dichiarative, anziché applicare last-write-wins. Lo stato finale dipende dall'**insieme** dei documenti caricati, non dall'**ordine** di arrivo degli eventi.

## Contesto

Il flusso Sprint Parser produce proposte di campo profilo da fonti multiple (XBRL CCIAA, bilancio gestionale, libro cespiti, profile_enrichment Phase 10, manual_override UI). Ogni proposta è una riga in `practice.client_field_extractions`, emessa dai PFE come evento `practice.field_proposed`.

Tre problemi della prima implementazione (gating inline nei PFE):
- **Caricamento massivo**: Redis Streams non garantisce ordine; proposte concorrenti per stesso `(client, campo)` venivano applicate non-deterministicamente.
- **Race condition**: `pg_advisory_xact_lock` mitigava ma non risolveva la semantica "ultimo arrivato" se gli eventi venivano processati in ordine inverso al caricamento.
- **Scope cross-fonte**: aggiungere una nuova fonte (es. visura) richiedeva di toccare tutti i PFE per il gating mutuale → matrice combinatoria difficile da mantenere.

## Pattern

```
┌──────────────────┐
│ FIELD_POLICIES   │  dict[campo → FieldPolicy]
│  - rankings      │  tuple[SourceRanking(agente, priority)]
│  - threshold     │  float (auto-apply ≥ 0.85)
│  - conditional?  │  Callable opzionale per logica context-aware
└────────┬─────────┘
         │ caricato a init time
         ▼
┌──────────────────────────────────────┐
│ ProfileFieldMergeConsumer.handle()   │
│  1. acquire pg_advisory_xact_lock    │
│  2. load TUTTE proposte attive       │
│     (PROPOSTA + APPLICATA)           │
│  3. decide_winner(policy, proposals) │
│  4. winner → APPLICATA + UPSERT      │
│     losers → RIFIUTATA               │
│     motivo: policy_override:{winner} │
│  5. emit practice.field_merged       │
│     (audit downstream)               │
└──────────────────────────────────────┘
```

Decision algorithm (deterministico):
1. Filtra proposte attive (escluse RIFIUTATA).
2. Filtra confidenza ≥ threshold.
3. Se policy ha `conditional` → invocala (riceve `current_year` da `envelope.produced_at` per replay-safety).
4. Altrimenti ordina per `(priority ASC, confidenza DESC, extraction_id DESC)`. Tie-break su `extraction_id` mantiene determinismo: la più recente vince a parità di rank.

## Decisioni chiave

| Decisione | Razionale |
|---|---|
| **Policy come codice Python**, non config YAML | Type-safe, immutabile, testabile via unit test puri. P&G "data is config, behavior is code". |
| **`current_year` esplicito al conditional** | Replay-safety: un evento riprocessato a mesi di distanza produce lo stesso vincitore. `datetime.now()` solo come fallback. |
| **`manual_override` priority 0 in tutte le policy** | L'override umano è autoritativo per definizione (Sprint R1 T-R1-11). Non sovrascrivibile da extractor automatici. |
| **Loser → RIFIUTATA con `policy_override:{vincitore}`**, non DELETE | History-shape preservata: l'API `GET /profile/{campo}/source` ricostruisce la catena di decisioni per audit. |
| **`pg_advisory_xact_lock` con namespace versionato** | Serializza merge concorrenti su stessa coppia `(client, campo)` evitando collisioni cross-flow. |

## Riusabilità

Il pattern è applicabile fuori da AIOS Studio ovunque serva merge deterministico cross-fonte:
- Anagrafica clienti consolidata da CRM + visura + libro soci.
- Pricing engines con quote da provider multipli.
- Configurazione device IoT con override locale + remoto.

Vincoli per riuso:
- Modello dati history-shaped (proposte non si cancellano, si declassano).
- Lock cooperativo per coppia di chiavi (advisory lock o DB-specific equivalente).
- Outbox pattern per audit downstream.

## Riferimenti

- Decisione: [[Sistema-Agentico-Studio]] → ADR-012 in `.brain/30-Decisioni/ADR-012-Field-Priority-Policy-Framework.md`
- Loss correlate: [[2026-05-01-sprint-parser-manual-override-perde-policy]]
- Codice: `services/practice-context-service/app/domain/field_priority_policy.py` + `app/consumers/profile_field_merge_consumer.py`
