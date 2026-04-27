---
tipo: architettura
creato: 2026-04-26
aggiornato: 2026-04-27
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
> Cinque agenti **LLM-based** (Anthropic Sonnet 4 / Haiku 4.5) con un **AIOSSupervisor opzionale** (`USE_SUPERVISOR=false` di default), tre invarianti architetturali non negoziabili (no coupling diretto, separazione execution↔validation, workflow firma cliente). Verità di prodotto verificata sul codice il 2026-04-27.

> [!warning] Correzione 2026-04-27
> Versione precedente diceva "5 agenti rule-based coordinati da Supervisor LLM". **Falso**: tutti e 5 gli agenti usano LLM, e il Supervisor è un overlay opzionale disattivato di default. Vedi [[AIOS-Sanitizzazione-Note-Vault]].

## Mappa agenti (verità codice 2026-04-27)

| Codice | Agente | Modello / Tipo | Ruolo |
|---|---|---|---|
| AGT-001 | **DocumentAgent** | LLM-based | classifica documenti in ingresso (FatturaPA, CU, bilanci PDF) |
| AGT-002 | **AccountingAgent** | **Sonnet 4** | contabilizzazione fatture con classificazione SP/CE |
| AGT-003 | **FiscalAgent** | LLM-based | pratiche fiscali (DICHIARATIVA/GENERICA, CU, bilanci) |
| AGT-004 | **ValidationAgent** | **LLM separato** (VER-002) | valida output indipendentemente dall'agente che esegue; su confidenza < soglia → escalation umana |
| AGT-005 | **ReviewAgent** | LLM-based | assembla review package per il commercialista (no self-validation) |

> [!info] AIOSSupervisor — overlay opzionale
> `AIOSSupervisor` esiste come servizio di orchestrazione LLM, ma il flag **`USE_SUPERVISOR=false` è il default** (decisione architetturale ADR-004). In modalità default i 5 agenti sono coordinati da contratti espliciti via event bus / workflow-sdk; il Supervisor LLM si attiva solo quando il flag è esplicitamente true. **Implicazione pitch**: parlare di "Supervisor che orchestra" è impreciso per la configurazione attuale del pilot.

## Tre invarianti architetturali non negoziabili

- **Nessun coupling diretto agente-agente**: il coordinamento passa sempre da contratti espliciti (event bus, workflow-sdk) o, opzionalmente, dal Supervisor.
- **Separazione execution ↔ validation**: chi esegue non valida sé stesso. ValidationAgent è un LLM separato (VER-002); il ReviewAgent presenta al commercialista ma non approva.
- **Workflow obbligato con firma cliente per dichiarativi e bilanci**: per questi due flussi la procedura prevede **colloquio cliente + firma** prima di proseguire (D23, D27 intervista padre). Vincolo ancora **ASSENTE nel codice** (vedi R6 in [[AIOS-Rischi-Pilot]] e Phase-10-Guardrail nel `.brain/`) — bloccante per go-live se i 10 pilot includono dichiarativi/bilanci nel periodo di osservazione.

## Agenti pensati ma non (ancora) nel codice

- **Agente finanziario/advisory** — originariamente in testa al founder, avrebbe dovuto suggerire leve fiscali al cliente. Attualmente **accorpato in parte in FiscalAgent e AccountingAgent**. Deep dive rinviato post-MVP (vedi [[AIOS-Verifica-Roadmap-Agenti]]).
- **Agente consulenza del lavoro** — citato in intervista (D8), **non ancora trovato nel brain del progetto**. Da verificare (vedi [[AIOS-Verifica-Roadmap-Agenti]]).

## Audit primitive agentiche

Vedi [[AIOS-Audit-Primitive-Agentiche]] per la tabella delle ~12 primitive (Supervisor, sub-agent, skill-as-procedure, hook/guardrail, MCP/tool frontier, memoria per-cliente, memoria globale, reasoning trace, pseudonymizer, validation indipendente, human review, self-evolution governata).

## Domande aperte

> [!question]
> - In quale orizzonte si valuta l'attivazione di `USE_SUPERVISOR=true`? È legato a complessità del workflow o a metriche di qualità?
> - Dove è la "roadmap ristrutturata" nel repo che include l'agente consulenza lavoro? (vedi [[AIOS-Verifica-Roadmap-Agenti]])

## Collegamenti

- [[Sistema-Agentico-Studio]] — MOC del progetto
- [[AIOS-Architettura-Tre-Strati]] — gli agenti come strato 3
- [[AIOS-Audit-Primitive-Agentiche]] — primitive agentiche
- [[AIOS-Verifica-Roadmap-Agenti]] — azione aperta roadmap + esito R1-R7
- [[AIOS-Rischi-Pilot]] — R6 firma cliente come gap architetturale
- [[AIOS-Stack-Tecnico]] — stack Anthropic-only (Sonnet 4 / Haiku 4.5)
- [[AIOS-Intervista-Padre-Domande-KB]] — fonte D23, D27
- [[AIOS-Sanitizzazione-Note-Vault]] — fonte della riscrittura
