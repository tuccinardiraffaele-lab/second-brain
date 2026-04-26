---
tipo: architettura
creato: 2026-04-26
aggiornato: 2026-04-26
stato: attivo
progetto: "[[Sistema-Agentico-Studio]]"
tags:
  - aios/architettura
  - aios/agenti
  - prodotto/design
area: prodotto
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari: []
forma_aggancio: asset
sistema_owner: "[[Processo-Quality-Pillar-Coding]]"
---

# AIOS — Architettura tecnica degli agenti

> [!info] In una frase
> Cinque agenti rule-based coordinati da un **Supervisor LLM**, con tre invarianti architetturali non negoziabili (no coupling diretto, separazione execution↔validation, workflow firma cliente). Stato repo al 2026-04-13.

## Mappa agenti (stato repo 2026-04-13)

| Codice | Agente | Ruolo |
|---|---|---|
| AGT-001 | **DocumentAgent** | classifica documenti in ingresso (FatturaPA, CU, bilanci PDF) |
| AGT-002 | **AccountingAgent** | contabilizzazione |
| AGT-003 | **FiscalAgent** | pratiche fiscali (DICHIARATIVA/GENERICA, CU, bilanci) |
| AGT-00? | **ValidationAgent** | valida output DocumentAgent; su confidenza bassa → escalation al commercialista |
| AGT-004 | **ReviewAgent** | assembla review package per il commercialista (no self-validation) |

## Review e validazione come invariante

Tre invarianti architetturali non negoziabili del sistema:

- **Nessun coupling diretto agente-agente**: il coordinamento passa sempre dal Supervisor o da contratti espliciti.
- **Separazione execution ↔ validation**: chi esegue non valida sé stesso; il ReviewAgent presenta al commercialista ma non approva.
- **Workflow obbligato con firma cliente per dichiarativi e bilanci**: per questi due flussi la procedura deve prevedere **colloquio con il cliente + firma** prima di proseguire (vincolo esplicitato dal titolare, vedi [[AIOS-Intervista-Padre-Domande-KB|D23, D27]]). Non è una review interna: è uno step esterno obbligato nel flusso.

## Agenti pensati ma non (ancora) nel codice

- **Agente finanziario/advisory** — originariamente in testa al founder, sarebbe dovuto suggerire al cliente leve fiscali e insight sulla base dei risultati dell'AccountingAgent per migliorare la situazione finanziaria. Attualmente **accorpato in parte in FiscalAgent e AccountingAgent**. Deep dive rinviato all'ultimazione MVP (vedi [[AIOS-Verifica-Roadmap-Agenti]]).
- **Agente consulenza del lavoro** — citato in intervista, **non ancora trovato nel brain del progetto**. Da verificare (vedi [[AIOS-Verifica-Roadmap-Agenti]]).

## Audit primitive agentiche

Vedi [[AIOS-Audit-Primitive-Agentiche]] per la tabella delle ~12 primitive (Supervisor, sub-agent, skill-as-procedure, hook/guardrail, MCP/tool frontier, memoria per-cliente, memoria globale, reasoning trace, pseudonymizer, validation indipendente, human review, self-evolution governata).

## Domande aperte

> [!question]
> - Dove è la "roadmap ristrutturata" nel repo che include l'agente consulenza lavoro? (vedi [[AIOS-Verifica-Roadmap-Agenti]])

## Collegamenti

- [[Sistema-Agentico-Studio]] — MOC del progetto
- [[AIOS-Architettura-Tre-Strati]] — gli agenti come strato 3
- [[AIOS-Audit-Primitive-Agentiche]] — primitive agentiche
- [[AIOS-Verifica-Roadmap-Agenti]] — azione aperta roadmap
- [[AIOS-Intervista-Padre-Domande-KB]] — fonte D23, D27
