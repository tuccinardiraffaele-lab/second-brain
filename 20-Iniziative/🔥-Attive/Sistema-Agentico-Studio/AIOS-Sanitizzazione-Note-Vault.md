---
tipo: progetto
creato: 2026-04-27
aggiornato: 2026-04-27
stato: attivo
tags:
  - progetto/sistema-agentico
  - azione-aperta
  - vault/sanitizzazione
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
prossima_azione: "Sanitizzazioni minori post-go-live (>2026-05-10): Architettura-Tre-Strati, Timeline-Pilot, Value-Prop-Pain-E-Relazione"
blocco: ""
---

# Sanitizzazione note vault AIOS-*

> [!info] Cosa è
> Lo split del 2026-04-26 ha creato 8 note atomiche AIOS-* a partire dalla MOC [[Sistema-Agentico-Studio]] **scritte a memoria**, senza scendere nel codice. La verità di prodotto verificata il 2026-04-27 (5 Explore + 2 fact-check sul codice + `.brain/`) ha mostrato che alcune note del vault contraddicono la realtà. Questa nota traccia le sanitizzazioni dovute, in ordine di urgenza.

> [!warning] Perché conta
> Le note vault non sono per il codice — sono per la **comunicazione esterna** (pitch al padre, futura conversazione B2C, posizionamento). Una nota che dice "5 agenti rule-based" mentre il codice ha 5 agenti LLM-based (Sonnet 4 + Haiku 4.5) brucia credibilità tecnica al primo confronto serio.

## Top-3 sanitizzazioni pre-2026-05-03

> [!success] Chiuse il 2026-04-27
> Tutte e 3 le note top-priority sanate prima della 2ª intervista padre. MOC [[Sistema-Agentico-Studio]] riga 24 corretta in coda.

### 1. [[AIOS-MVP-Confine-Operativo]] — riscritta ✅

- **Stato vault precedente**: "MVP = contabilizzazione fatture + GBSoftware"
- **Realtà codice**: scope MVP = **6 use case** (intake doc / apertura pratica / contabilità operativa / adempimenti fiscali standard / scadenze-task / validazione output) + out-of-scope espliciti (payroll, audit enti pubblici, tax advisory, labor advisory, research normativa)
- **Azione fatta**: riscritta allargando perimetro a 6 use case + sezione "fuori scope" esplicita con 5 voci

### 2. [[AIOS-Architettura-Agenti]] + MOC riga 24 — corrette ✅

- **Stato vault precedente**: "5 agenti rule-based coordinati da Supervisor LLM"
- **Realtà codice**: **5 agenti LLM-based** (DocumentAgent, AccountingAgent con Sonnet 4, ValidationAgent con LLM separato VER-002, FiscalAgent, ReviewAgent) + **AIOSSupervisor con flag `USE_SUPERVISOR=false` di default** (ADR-004)
- **Azione fatta**: tabella agenti riscritta con modello/tipo + esplicitato Supervisor come overlay opzionale; MOC riga 24 corretta in coerenza

### 3. [[AIOS-Rischi-Pilot]] — aggiornata ✅

- **Stato vault precedente**: solo timeline stretta + GBSoftware gate
- **Realtà codice**: 3 red flag concreti emersi dalla verifica R1-R7:
  - Strato 1 vault baseline è PARZIALE (Knowledge Reference Service esiste ma senza auto-update normativo)
  - R6 firma cliente ASSENTE (vincolo non negoziabile D27 intervista — bloccante per dichiarativi/bilanci)
  - R7 alert scadenze PARZIALE (motore esiste, manca API + scheduler — soglia pilot #3)
- **Azione fatta**: aggiunta sezione "rischi architetturali concreti" con R3/R6/R7 + backlog 48h + reference al guardrail Phase 10 nel `.brain/`

## Sanitizzazioni minori (post-go-live)

- [[AIOS-Architettura-Tre-Strati]] — disclaimer "stato target, Knowledge Reference oggi PARZIALE"
- [[AIOS-Timeline-Pilot]] — verificare stato Phase 9 in repo + aggiungere rischio Alembic
- [[AIOS-Value-Prop-Pain-E-Relazione]] — chiarire cosa dei pain enunciati è MVP vs visione

## Fonti della verifica

- 5 Explore paralleli sulla repo `~/projects/AIOS Studio/` (2026-04-27 sera)
- 2 fact-check indipendenti (coerenza interna report + divergenze vault)
- Esito verifica R1-R7 in `~/projects/AIOS Studio/.brain/00-Bridge/Phase-10-Guardrail-Architettura.md`

## Quando

- **Top-3** prima della 2ª intervista padre **2026-05-03** — ✅ chiuse il 2026-04-27
- **Minori** post-go-live (>2026-05-10), salvo emergano usi specifici prima

## Note collegate

- [[Sistema-Agentico-Studio]]
- [[AIOS-Verifica-Roadmap-Agenti]]
- [[AIOS-Intervista-Padre-Follow-Up]]
- [[OKR-Correnti]]
