---
tipo: progetto
creato: 2026-04-13
aggiornato: 2026-05-03
stato: attivo
tags:
  - progetto/sistema-agentico
  - prodotto/ai
  - strategia/bet-principale
area: prodotto
prossima_azione: "Aprire Phase 10 GBSoftware (KR1.1, deadline interna 2026-05-03). R6/R2/R7 e sanitizzazione vault chiusi 2026-04-27."
blocco: ""
repo_path: ~/projects/AIOS Studio
brain_path: ~/projects/AIOS Studio/.brain
---

# Sistema Agentico Studio

> [!info] In una frase
> Sistema multi-agente per **studi commercialisti + consulenza del lavoro medio-piccoli** che automatizza il lavoro manuale a valore nullo (contabilizzazione, classificazione documenti, scadenziario) portando dentro lo studio **ordine lean + AI insieme**. È il **bet strategico principale** della transizione corporate → consulenza (vedi [[Strategia-Attuale]]).

## Cosa fa concretamente

Cinque agenti AI **LLM-based** (Anthropic Sonnet 4 / Haiku 4.5), con un **AIOSSupervisor opzionale** (`USE_SUPERVISOR=false` di default — coordinamento via contratti espliciti event bus / workflow-sdk). Eseguono i lavori time-consuming tipici di uno studio commerciale: contabilizzazione fatture (con classificazione SP/CE), generazione bilanci, classificazione documenti in ingresso (FatturaPA, CU, bilanci), organizzazione scadenziario, sollecito clienti, review package per il commercialista. Verità di prodotto verificata sul codice il 2026-04-27 — vedi [[AIOS-Sanitizzazione-Note-Vault]].

## Indice navigabile

> [!tip] Hub di accesso al progetto
> Le sezioni di dettaglio vivono in note atomiche. Questa MOC mantiene solo: hub navigabile, stato vivo del progetto, log sessioni, debito/azioni aperte.

**Prodotto**
- [[AIOS-ICP-Studi-Medio-Piccoli]] — chi è il cliente target + studio del padre come cliente zero
- [[AIOS-Value-Prop-Pain-E-Relazione]] — pain risolti + principio "AI libera tempo per relazione"
- [[AIOS-MVP-Confine-Operativo]] — confine MVP (contabilizzazione + GBSoftware) + ripriorizzazione post-MVP
- [[AIOS-Modello-Business]] — B2C / B2B + vincolo reputazionale

**Architettura**
- [[AIOS-Architettura-Tre-Strati]] — vault Obsidian + processi lean + agenti AI
- [[AIOS-Architettura-Agenti]] — i 5 agenti + invarianti (no coupling, separazione exec/val, firma cliente)
- [[AIOS-Servizi-Inventario]] — 12 servizi (11 MVP + GB Integration Phase 10) con porte e fasi
- [[AIOS-Stack-Tecnico]] — Python/FastAPI + Postgres/Redis/MinIO + Anthropic-only (Sonnet 4 / Haiku 4.5)
- [[AIOS-Audit-Primitive-Agentiche]] — primitive agentiche (~12)

**Pilot**
- [[AIOS-Timeline-Pilot]] — go-live ~10 maggio 2026 + metriche al 30 giugno
- [[AIOS-Rischi-Pilot]] — rischi specifici del pilot
- [[Decisione-Soglie-Pilot-AIOS]] — soglie chiuse il 2026-04-19

**Knowledge studio del padre (intervista 2026-05-03)**
- [[AIOS-Bus-Factor-Studio]] — mappa persona→impatto sulle 4 posizioni dello studio (titolare, contabile società, contabile privati, segreteria)
- [[AIOS-Cliente-Fuori-Standard]] — 3 archetipi (edilizia, notaio, farmacia) tutti dentro pilot al go-live
- [[AIOS-Processo-Quadratura-Trimestrale]] — 8 passi end-to-end + colli di bottiglia (passo 5 banca, passo 7 verifica)
- [[AIOS-Firma-Deleghe-Procure-Cliente]] — 17 atti cablati + delega unica AdE + 6 zone grigie risolte + antiriciclaggio cablato fin dal go-live
- [[AIOS-Gate-GBSoftware-Dossier]] — dossier preparatorio Gate A→B (workflow 4 writer, config GB cloud, ranking priorità Visura→VarIVA→F24→FatturaPA)


**Pattern frontend (sprint 2026-04-28)**
- [[Arch-HTMX-Refresh-Inline-Script]] — refresh post-submit deterministico, immune a cache
- [[Arch-Dashboard-No-Cache-Headers]] — middleware no-cache su tutte le response dinamiche
- [[Arch-Test-Reset-Outbox-Aware]] — cleanup E2E con outbox

**Pattern eventing/automation (Sprint Apprendimento 2026-04-28)**
- [[Arch-Hybrid-Sync-Async-LLM-Enrichment]] — emit sincrono in TX al boundary HTTP + agent LLM + apply consumer asincroni; mai LLM nella request utente
- [[Arch-Idempotent-Generated-Artifact-Markers]] — marker `<!-- aios:auto:start/end -->` per artefatti generati che convivono con annotazioni umane
- [[Arch-Event-Key-Persisted-Unique]] — chiave veicolata in evento = colonna UNIQUE persistita; mai UUID effimeri da route
- [[Arch-Service-Returns-Emitted-Envelope]] — domain service che fa emit ritorna `(record, envelope)` per consentire `propagate()` ai caller

**Pattern data-merge (Sprint Parser Estensione 2026-05-01)**
- [[Arch-Field-Priority-Policy-Framework]] — merge multi-fonte deterministico via policy dichiarative + ricomputo globale per (client, campo); stato finale dipende dall'insieme delle proposte, non dall'ordine

**Debito tecnico aperto (Sprint Parser Estensione 2026-05-01)**
- [[Debito-Sprint-Parser-Uuid-Literal-Duplicato]] — UUID null literal duplicato tra migration 056 e codice runtime, sync solo testuale (gravità bassa)
- [[Debito-Sprint-Parser-Last-Enrichment-At-Touch-Vs-Modifica]] — `last_enrichment_at` semantica "ultimo touch", da rivedere se UI pilot richiede "ultima vera modifica" (gravità bassa)

## Loss chiuse

- [[2026-04-28-test-e2e-composition-non-esercita-route]] — pipeline AI no-op silenzioso passata oltre review perché 9 test "E2E" mockavano repo+agent senza chiamare il route. Classificazione A.
- [[2026-04-29-r1-envelope-root-non-capable]] — override manuale apriva root su event_type non root-capable, rompendo invariante #5 e silenziando ObligationRecalculator. Classificazione A. Lezione: trigger manuali → `intake.event_received` source_type=human + propagate, mai root domain.
- [[2026-04-29-r1-apply-manual-correction-sql-injection]] — whitelist solo al bordo route, dominio interpolava identifier SQL non validato. Classificazione A. Lezione: validare ai bordi del **modulo**, non solo del sistema.
- [[2026-04-29-r1-previous-value-collezioni-audit]] — `str()` come serializer universale produceva letterali Python irrecuperabili per array. Classificazione A. Lezione: `str()` è per primitivi; collezioni → `json.dumps`.
- [[2026-05-01-sprint-parser-source-endpoint-read-oracle]] — endpoint tracciabilità con whitelist sintattica (`isalnum()`) anziché semantica (`FIELD_POLICIES`) → information disclosure su PII. Classificazione A. Lezione: whitelist semantica registry-driven, mai swallow Exception in tx Postgres aperta.
- [[2026-05-01-sprint-parser-audit-ledger-duplicato]] — tabella history-shaped scritta senza dedup applicativo né partial unique → duplicati su replay che il consumer policy-driven auto-elimina con motivo `policy_override:{stesso_agente}`. Classificazione A. Lezione: history-shape implica idempotency a carico del producer.
- [[2026-05-01-sprint-parser-manual-override-perde-policy]] — nuova fonte di proposte (manual_override) introdotta come side effect tracciabilità senza registrarla nel policy framework → override umano declassato da automatici al successivo merge. Classificazione A. Lezione: framework decisionali centrali richiedono doppia registrazione (flusso scrittura + framework arbitro).

## Stato attuale (vivo)

- **Fase**: Phase 9 completata + backlog architetturale R2/R6/R7 chiuso 2026-04-27. **Phase 10 GBSoftware = da aprire** — gate vincolante del go-live.
- **Soglie pilot**: 3/5 chiuse il 2026-04-19. Tempo risparmiato resta misurata-non-gate.
- **Prossima intervista padre** (KB completion): pianificazione 2026-05-02, esecuzione 2026-05-03 (vedi [[AIOS-Intervista-Padre-Follow-Up]]).
- **Margine pre-go-live**: 7 giorni (era 14, ridotto per slittamento intervista).

## Trigger condizionali — upgrade/fallback modello

> [!tip] Vision Opus 4.7 come fallback se agenti documentali sotto-performano
> Backbone coding già su Opus 4.7. Per gli agenti che processano **fatture / buste paga / 730 scansionati**, se in pilot emergono errori di estrazione o classificazione su immagini, valutare upgrade vision a Opus 4.7 (acuity 54,5% → 98,5%, immagini fino a 2576px / 3,75MP). Tenere conto del tokenizer +35% nelle stime costo. Fonte: [[Studio-AI-2026-05-03]].


> [!tip] Managed Agents come opzione architetturale per refactor post-pilot
> Anthropic ha rilasciato in **public beta** (8 aprile 2026) Managed Agents: runtime hosted con durable sessions, sandbox container, MCP integrato. Pricing $0.08/h sessione attiva (idle non si paga) + token standard. Rilevante per sostituire il loop custom di AIOS dopo il go-live: zero DevOps burden, long-running tasks (contabilizzazione, buste paga, F24) gestiti nativamente, OAuth connettori (GBSoftware-like) gestito da Anthropic. **Non toccare ora** — guardrail no-refactor fuori critical path. Valutare nel refactor post-pilot; per B2B futuro attendere GA. Fonte: [[Studio-AI-2026-05-04]].

## Repo di riferimento

Codebase: `~/projects/AIOS Studio/` (WSL).

Struttura rilevante:
- `agents/` — cinque agenti MVP
- `services/orchestration-service/` — Supervisor LLM
- `services/human-review-service/` — superficie human-in-the-loop
- `.brain/10-Progetto/Next-Steps.md` — stato Phase 10 (GBSoftware) e carryover
- `.brain/99-Archivio/phase-readiness-scope/phase-9-readiness-review.md` — ultimo readiness review completato
- `.brain/00-Bridge/` — protocollo di crossing vault ↔ brain locale (5 tipi T1-T5) e mapping aree

## Azioni aperte

- [[AIOS-Chiarire-Metriche-Pilot]] — soglia "tempo risparmiato"
- [[AIOS-Verifica-Roadmap-Agenti]] — verifica R1-R7 chiusa 2026-04-27, backlog R2/R6/R7 implementato 2026-04-27
- [[AIOS-Sanitizzazione-Note-Vault]] — top-3 chiuse 2026-04-27, restano sanitizzazioni minori post-go-live
- [[AIOS-Intervista-Padre-Follow-Up]] — seconda intervista KB (2026-05-03)
- [[AIOS-Intervista-Esperto-GBSoftware]] — intervista esperto integrazione (2026-05-01)

## Log sessioni

- [[2026-05-01]] — Sprint Parser Estensione completato (8 step + 3 giri iterate skill, 1408/1408 test verdi). Migration 055/056, BilancioGestionaleExtractor v1.1 (CE codici 60-79), BilancioXBRLParser v1.1 (tassonomia ITCC), PFE simmetrici 4→12 / 1→11 campi, ProfileFieldMergeConsumer riscritto con `field_priority_policy`, gap audit Phase 10 chiuso (D-5), endpoint tracciabilità fonte. 3 loss A chiuse via UPS in-line nei review reviewer. ADR-012 + Trade-Off-Log nel brain locale. Pattern promosso: [[Arch-Field-Priority-Policy-Framework]].
- [[2026-04-28]] — review post-merge Sprint Apprendimento Sessione 2+3: 3 BLOCKER + 4 HIGH + 3 MEDIUM via UPS, fix in commit `3c0839c`. Pattern promossi: chiave evento = UNIQUE persistita, service ritorna envelope. Loss chiusa: test E2E composition non esercita route.
- [[2026-04-28]] — triage digest AI 27-28 + capture 3 opportunità Phase 11 nel brain locale AIOS (hooks→MCP, agent frontmatter, AI Organizations research) + indice intercettazione `Phase-11-Backlog-Valutazioni`
- [[2026-04-27]] — pipeline multi-agent verità-di-prodotto + verifica R1-R7 nel codice + guardrail Phase 10 in `.brain/00-Bridge/` + estensione vault (`AIOS-Servizi-Inventario`, `AIOS-Stack-Tecnico`, `AIOS-Sanitizzazione-Note-Vault`) + redesign MECE brain locale del mattino + dismissione Codex (vedi [[Dismissione-Codex]])
- [[2026-04-26]] — split MOC in note atomiche (8 atomiche AIOS create)
- [[2026-04-20]] — aggiornamento MOC (stadio 1/2) con insight intervista padre: pain scadenze promosso, value prop relazionale, workflow firma cliente, ripriorizzazione post-MVP, ICP rafforzato.
- [[2026-04-19]] — prima intervista padre KB AIOS: soglie pilot chiuse ([[Decisione-Soglie-Pilot-AIOS]], [[AIOS-Intervista-Padre-Domande-KB]]).
- [[2026-04-15]] — brainstorm knowledge map per interview padre + 3 gap repo aggiunti a [[AIOS-Verifica-Roadmap-Agenti]]

## Collegamenti

- [[Strategia-Attuale]] — bet strategico principale + logica dei 4 filoni
- [[Identità]] — il perché della transizione e l'asimmetria Lean + giuridico
- [[Football-Trading]] — pilot "in orbita" che libera tempo per questo
- [[Studio-Del-Padre-Piattaforma]] — cliente zero
- [[Decisione-Transizione-Angelini-Studio]] — cornice decisionale della transizione
- [[Monitoraggio-regolatorio-AI]] — mitigazione rischio esogeno
- [[Finanza-Business-Pricing-AIOS]] · [[Finanza-Business-Costi-Operativi-AIOS]]
- [[Prodotto-Vault-Substrato-Di-Prodotto]]
