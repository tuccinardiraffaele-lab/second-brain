---
tipo: progetto
creato: 2026-04-13
aggiornato: 2026-04-27
stato: attivo
tags:
  - progetto/sistema-agentico
  - prodotto/ai
  - strategia/bet-principale
area: prodotto
prossima_azione: "Completare integrazione GBSoftware (Phase 10)"
blocco: ""
repo_path: ~/projects/AIOS Studio
brain_path: ~/projects/AIOS Studio/.brain
---

# Sistema Agentico Studio

> [!info] In una frase
> Sistema multi-agente per **studi commercialisti + consulenza del lavoro medio-piccoli** che automatizza il lavoro manuale a valore nullo (contabilizzazione, classificazione documenti, scadenziario) portando dentro lo studio **ordine lean + AI insieme**. È il **bet strategico principale** della transizione corporate → consulenza (vedi [[Strategia-Attuale]]).

## Cosa fa concretamente

Cinque agenti AI rule-based, coordinati da un **Supervisor LLM**, che eseguono i lavori time-consuming tipici di uno studio commerciale: contabilizzazione fatture (con classificazione SP/CE), generazione bilanci, classificazione documenti in ingresso (FatturaPA, CU, bilanci), organizzazione scadenziario, sollecito clienti, review package per il commercialista.

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
- [[AIOS-Audit-Primitive-Agentiche]] — primitive agentiche (~12)

**Pilot**
- [[AIOS-Timeline-Pilot]] — go-live ~10 maggio 2026 + metriche al 30 giugno
- [[AIOS-Rischi-Pilot]] — rischi specifici del pilot
- [[Decisione-Soglie-Pilot-AIOS]] — soglie chiuse il 2026-04-19

## Stato attuale (vivo)

- **Fase**: Phase 9 completata (Human Review Surface). **Phase 10 GBSoftware = da iniziare** — gate vincolante del go-live.
- **Soglie pilot**: 3/5 chiuse il 2026-04-19. Tempo risparmiato resta misurata-non-gate.
- **Prossima intervista padre** (KB completion): pianificazione 2026-05-02, esecuzione 2026-05-03 (vedi [[AIOS-Intervista-Padre-Follow-Up]]).
- **Margine pre-go-live**: 7 giorni (era 14, ridotto per slittamento intervista).

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
- [[AIOS-Verifica-Roadmap-Agenti]] — roadmap agenti futuri (advisory finanziario, consulenza lavoro)
- [[AIOS-Intervista-Padre-Follow-Up]] — seconda intervista KB (2026-05-03)
- [[AIOS-Intervista-Esperto-GBSoftware]] — intervista esperto integrazione (2026-05-01)

## Log sessioni

- [[2026-04-27]] — redesign MECE del brain locale `.brain/` + dismissione Codex (vedi [[Dismissione-Codex]]) + 4 ADR conformati a skill `decision`
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
