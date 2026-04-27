---
tipo: concetto
creato: 2026-04-26
aggiornato: 2026-04-27
stato: attivo
progetto: "[[Sistema-Agentico-Studio]]"
tags:
  - aios/rischi
  - prodotto/risk
area: prodotto
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari:
  - "[[Strategia-Pillar-Leadership-Strategica]]"
forma_aggancio: input
sistema_owner: "[[Processo-Validazione-Pilot]]"
---

# AIOS — Rischi del pilot

> [!info] In una frase
> Tre famiglie di rischi: **strategici di sistema** (mappati altrove), **specifici del pilot** (timeline, soglie, GBSoftware, ripetibilità) e **architetturali concreti** emersi dalla verifica codice del 2026-04-27 (R3, R6, R7 con guardrail nel `.brain/`).

## Rischi già mappati a livello strategico

Vedi [[Strategia-Attuale#Rischi strategici]] per:

- **Endogeno** — velocità competitiva (controllo pieno, è quello che toglie il sonno)
- **Esogeno** — regolatorio AI in ambito contabile/giuslavoristico (cecità attuale, mitigazione via [[Monitoraggio-regolatorio-AI]])

## Rischi specifici del pilot

- **Timeline stretta** — Phase 10 non iniziata, deadline ~10 maggio "sfidante ma non irrealizzabile". Se slitta, il playbook per il secondo studio slitta con essa.
- **Metriche soglia mancanti** — *parzialmente chiuso*: 3 soglie su 5 fissate il 2026-04-19 ([[Decisione-Soglie-Pilot-AIOS]]). Resta misurata-non-gate il tempo risparmiato (vedi [[AIOS-Chiarire-Metriche-Pilot]]).
- **Dipendenza hard da GBSoftware** — integrazione Phase 10 è gate assoluto del pilot. Un intoppo tecnico ferma tutto.
- **Ripetibilità del pattern caos → ordine → AI** — funziona sicuramente nello studio del padre; che un secondo studio caotico accetti di farsi "lean-ificare" insieme all'onboarding del vault è un'assunzione ancora da validare.

## Rischi architetturali concreti (verifica codice 2026-04-27)

> [!danger] Stato verificato
> Verifica R1-R7 fatta il 2026-04-27 con pipeline multi-agent (5 Explore + 2 fact-check). Esito: 1 OK / 2 PARZIALE / 4 ASSENTE. Dettaglio completo + evidenze `file:line` in `~/projects/AIOS Studio/.brain/00-Bridge/Phase-10-Guardrail-Architettura.md`. **Bloccanti per go-live 2026-05-10: R2, R6, R7.**

### R3 — Strato 1 vault baseline — PARZIALE

`knowledge-reference-service` esiste come baseline normativo italiano (domain + routes + tests presenti, seed JSON in `data/seed/deadline_rules.json`), ma **manca l'auto-update normativo**: nessun job schedulato, `sync-ade-calendar.py` è solo manuale, due fonti separate (`knowledge.fiscal_rules` vs `governance.deadline_rules`) non fuse.

**Impatto**: non bloccante per go-live, ma **essenziale per il pitch** della "knowledge baseline come asset difendibile" ([[Prodotto-Vault-Substrato-Di-Prodotto]]). Promettere al padre o a futuri prospect un sistema che "si tiene aggiornato sulla normativa" oggi sarebbe falso.

### R6 — Validation gate firma cliente — ASSENTE

Vincolo non negoziabile (D27 intervista): per dichiarativi e bilanci il workflow deve fermarsi su **colloquio cliente + firma** prima di proseguire. Verifica codice: la FSM AIOS (`packages/workflow-sdk/aios_workflow/transitions.py`) **non include** stati `PENDING_CLIENT_SIGNATURE` né `PENDING_CLIENT_APPROVAL`; l'enum `ReviewStatus` di `human-review-service` non ha "awaiting client".

**Impatto**: **bloccante** se i 10 pilot includono dichiarativi/bilanci nel periodo di osservazione (maggio-agosto = momento critico). Senza gate, il sistema può chiudere pratiche a livello tecnico senza la firma legale dovuta.

### R7 — Alert engine scadenze — PARZIALE

Soglia pilot #3 = ≥95% scadenze senza segnalazioni AdE. Verifica codice: motore presente (`DeadlineScanner` con loop 300s, `DeadlineEnforcementService`, eventi `governance.deadline.{approaching,urgent,overdue}`), ma:

- Endpoint `POST /deadlines/reminders/emit` **non esposto** (route `__init__.py` vuoto)
- Endpoint `GET /practices/{practice_id}/deadlines/upcoming` **non esposto**
- Nessuno scheduler che invochi `sync-ade-calendar.py` automaticamente

**Impatto**: **bloccante** per la soglia pilot #3. Senza esposizione API e auto-sync, le scadenze possono essere calcolate internamente ma non comunicate proattivamente.

### Backlog 48h (in ordine di blocco)

In ordine di peso bloccante per go-live 2026-05-10:

1. **R6** — stati FSM firma cliente + gate evento `client_signature.received`
2. **R2** — endpoint lettura fatture GB (flusso B), bloccante se >50% volume sui 10 pilot
3. **R7** — esposizione API deadlines + scheduler auto-sync

Dettaglio completo in `~/projects/AIOS Studio/.brain/00-Bridge/Phase-10-Guardrail-Architettura.md`.

## Collegamenti

- [[Sistema-Agentico-Studio]] — MOC del progetto
- [[Strategia-Attuale]] — rischi strategici di sistema
- [[Monitoraggio-regolatorio-AI]] — mitigazione rischio esogeno
- [[AIOS-Timeline-Pilot]] — timeline e metriche
- [[AIOS-MVP-Confine-Operativo]] — gate GBSoftware + scope MVP
- [[AIOS-Architettura-Agenti]] — 5 agenti LLM-based + invariante firma cliente (R6)
- [[AIOS-Verifica-Roadmap-Agenti]] — esito sintetico R1-R7
- [[AIOS-Sanitizzazione-Note-Vault]] — fonte della riscrittura
- [[AIOS-Intervista-Padre-Follow-Up]] — 2ª intervista 2026-05-03 chiude domande aperte
