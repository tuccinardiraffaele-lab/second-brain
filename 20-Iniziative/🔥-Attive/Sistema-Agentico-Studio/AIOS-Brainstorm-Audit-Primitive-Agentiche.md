---
tipo: riflessione
creato: 2026-04-15
aggiornato: 2026-04-15
stato: attivo
tags:
  - brainstorm/progetto
  - brainstorm/sistema-agentico-studio
  - claude-code
  - architettura-agentica
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
cynefin: complex
framework: rumelt
---

# Brainstorm — Audit primitive agentiche AIOS vs Claude Code

## Domanda di fondo

Ora che conosco le primitive standard di Claude Code (skill, hook, MCP, sub-agent) e la visione Jensen GTC 2026 sull'OS agentico, AIOS Phase 0-9 regge il confronto con lo stato dell'arte, o sta reinventando in forma custom pattern che hanno già una forma più matura?

## Classificazione (Cynefin)

**Complex** — territorio nuovo, nessun AIOS per studi professionali ben funzionante da copiare. La validità dei pattern emerge solo provandoli sul campo, non applicando best practice note.

## Diagnosis

AIOS Phase 0-9 ha costruito ciascun mattone agentico (agenti, tool, guardrail, memoria) in forma custom perché pre-esisteva alla maturazione dei pattern standard (Claude Code, visione Jensen GTC 2026). Il rischio non è "aver sbagliato" — è aver **internalizzato un'architettura buona-ma-non-ottimale come se fosse ovvia**, e di portarsi dietro il debito nelle Phase 10-12 senza nominarlo.

Sotto-diagnosi confermata dal founder: sulla **self-evolution governata** (sez. 4.6 URS, EVL-001..008) c'è una leva competitiva reale — Jensen la promuove in forma autonoma, AIOS la governa per vincoli normativi italiani. Presidiarla è imperdonabile se persa, ma **fuori MVP**.

## Guiding policy

Tre bucket temporali per non mescolare orizzonti.

### Pre-go-live (≤2026-05-10) — Freeze + scaffold audit agganciato al punto 7 roadmap brain

- ✅ Farai: creare lo **scaffold** della nota di audit come parte del seed `.brain/` AIOS (punto 7 di [[Brain-Framework-Implementazione]], anticipato da "post-go-live" a "in questi giorni"). Niente refactor dei 5 agenti, 6 tool, FSM, ValidationAgent.
- ❌ Non farai: aprire workstream di audit a sé stante. Se funziona e passa 1981 test, non si tocca.

### Post-go-live immediato (giugno) — Compilazione audit

- ✅ Farai: riempire tabella primitive + giudizio (equivalente / sottodimensionato / assente) + ranking top-3 gap per leva competitiva × effort. Input diretto per planning Phase 12.
- ❌ Non farai: audit che diventa refactor totale. Il gate è una gap-list *ranked*, non un piano di riscrittura.

### Medio termine (Phase 12+) — Leva competitiva

- ✅ Farai: accelerare self-evolution governata come differenziatore vs competitor che copiano il modello NVIDIA "senza supervisione".
- ❌ Non farai: self-evolution autonoma su regole normative cogenti (EVL-008 invariante).

> [!tip] Principio unificante
> Claude Code e visione Jensen sono uno **specchio retroattivo**: servono a **nominare il pattern** che AIOS ha già o gli manca, non a dettare la forma. Il dominio fiscale italiano rimane il driver.

### Vincolo architetturale sospeso (one-off)

NFR-001 vieta framework esterni di orchestrazione. Per questo esercizio il vincolo è sospeso: Claude Code come **pattern-reference**, non come runtime. In produzione AIOS continua a girare via Anthropic API diretta (Claude Code CLI non deployabile server-side).

## Coherent actions

### Bucket 1 — In questi giorni (agganciato al punto 7 roadmap brain)

- [ ] **A1** — Durante seeding `.brain/` AIOS, creare `Audit-Primitive-Agentiche-AIOS.md` in `.brain/architecture/` come una delle note seed. Tabella vuota con ~12 righe primitive: Supervisor, sub-agent, skill-as-procedure, hook/guardrail, MCP/tool frontier, memoria per-cliente, memoria globale (brain), reasoning trace, pseudonymizer, validation indipendente, human review, self-evolution governata.
- [ ] **A2** — Aggiornare [[Brain-Framework-Implementazione]]: (a) promuovere punto 7 da "post-go-live" a "in questi giorni"; (b) aggiungere sotto-task "seed `.brain/architecture/Audit-Primitive-Agentiche-AIOS.md`".
- [ ] **A3** — Aggiornare [[Sistema-Agentico-Studio]] frontmatter con `repo_path` + `brain_path` (gap identificato il 2026-04-15, disallineato vs Football Trading).
- [ ] **Budget duro**: max 3h totali per A1+A2+A3. Oltre questa soglia, sottrae tempo critico a Phase 10 GBSoftware.

### Bucket 2 — Giugno (post-stabilizzazione go-live)

- [ ] **B1** — Compilare tabella audit: per ogni riga, giudizio + 1-2 righe motivazione + link ad ADR/codice. Finestra: 1 sessione concentrata 3-4h.
- [ ] **B2** — Gap-list ranked top-3 → input planning Phase 12.

### Bucket 3 — Phase 12+ (luglio+)

- [ ] **C1** — Self-evolution governata (EVL-001..008) promossa da SHOULD a MUST su feature identificata da B2.
- [ ] **C2** — Eventuale adozione MCP-over-HTTP come frontiera GBSoftware se B1 lo classifica "sottodimensionato".

## Pre-mortem

Ottobre 2026. Brainstorming fallito. Tre cause più probabili:

1. **Punto 7 anticipato sottrae tempo a Phase 10 GBSoftware** → go-live slitta oltre il 10 maggio. **Mitigazione**: budget 3h duro, scaffold minimo (no popolamento iper-preciso).
2. **B1 slitta a settembre** — stabilizzazione go-live + secondo esame studio giuridico + marketing/sales saturano giugno-agosto. Gap-list non alimenta Phase 12 in tempo, debito si replica. **Mitigazione**: B1 deliberatamente a metà giugno con 5 settimane di buffer dal go-live; reality-test esplicito qui sotto.
3. **L'audit diventa accademico** — 12 primitive mappate, giudizi eleganti, zero azioni. Rischio di dichiarare "AIOS equivalente a Claude Code" per conferma identitaria (sycophancy architettonica). **Mitigazione**: B2 obbliga a *ranking* top-3 → scelta, non descrizione.

## Alternative e reality-test

### Alternative considerate

- **Inlining dei gap** (annotare durante Phase 11, niente nota dedicata) — scartata dal founder in favore dell'audit strutturato. Motivazione: meno sistematico, rischia di catturare solo i gap che cadono addosso, non quelli che richiedono confronto attivo.
- **Non fare l'audit affatto** — scartata implicitamente scegliendo di farlo. Registrata per completezza.
- **Audit pre-go-live come workstream a sé** — scartata per vincolo temporale duro (go-live 10 maggio).

### Reality-test

> [!question] Segnale per cambiare idea
> Se al **2026-06-01** Phase 11 (vault-substrato normativo) non è ancora partita e l'audit scaffold è ancora vuoto, rivalutare: promuovere l'audit a pre-Phase 11 oppure ripiegare su inlining. Soglia dichiarata esplicitamente per non decidere per fede.

## Prossimo passo

- [ ] **Entro 2026-04-20** — A1 + A2 + A3 eseguiti, budget 3h duro.
- [ ] **Prossima sessione coding AIOS** — seeding `.brain/` AIOS con punto 7 roadmap brain, nota audit inclusa nel seed `architecture/`.
- [ ] Registrare `/decision` sulla scelta "audit strutturato vs inlining" + vincolo al punto 7 (scelta matura, vale la pena formalizzarla per non riaprirla).

## Note collegate

- [[Sistema-Agentico-Studio]] — MOC del bet strategico
- [[Brain-Framework-Implementazione]] — punto 7 della roadmap post-Step C a cui A1 si aggancia
- [[Strumenti-Filing-Brain-Globale-Locale]] — pattern trasferito da second-brain personale ad AIOS
- [[Prodotto-Vault-Substrato-Di-Prodotto]] — Phase 11, feature di prodotto (baseline normativo), non in scope di questo audit
- [[Decisione-Framework-Brain-Globale-Locale]] — decisione architetturale brain globale+locale
- [[Strategia-Attuale]] — vincolo reputazionale B2B + rischio endogeno velocità competitiva
- [[OKR-Correnti]] — ambiente di trade-off temporale
- [[AIOS-Brainstorm-Knowledge-Map-Padre]] — brainstorming precedente sulla stessa iniziativa
