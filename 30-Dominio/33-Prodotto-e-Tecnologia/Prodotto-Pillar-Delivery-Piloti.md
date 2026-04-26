---
tipo: concetto
creato: 2026-04-20
aggiornato: 2026-04-20
stato: attivo
tags:
  - pillar/strategico
  - prodotto/delivery
area: prodotto
pillar-fase: Foundation
pillar-fase-num: 0
pillar-loss:
  - Maturita-piloti-non-in-tempo
---

# Pillar — Delivery piloti

> [!info] In una frase
> Presidia la **maturità del framework di delivery a doppio livello** (vault globale Second Brain + vault locale in ogni repo pilota, **che include `.brain/`**) che fa arrivare FT, AIOS e piloti futuri allo stato di leva strategica entro la finestra competitiva. Il pillar misura il framework, non lo stato dei singoli piloti (che vive nelle MOC).

## Architettura chiarita (2026-04-20)

- **Vault globale** = Second Brain (`~/Second Brain/`) — principi, processi, loss cross-progetto
- **Vault locale** = Obsidian vault dentro ciascuna repo pilota, che **comprende `.brain/` come sottocartella navigabile** — non sono due entità separate
- **Regole di scambio globale↔locale** vivono in [[Strumenti-Filing-Brain-Globale-Locale|Filing-Brain-Globale-Locale]]
- **Dichiarazione del framework** vive in una nota canonica dedicata (da creare come parte di Foundation)

## Loss proprietarie

| # | Loss bucket |
|---|-------------|
| #8 | Maturità piloti non raggiunta entro finestra competitiva |

## Natura del pillar (cappello sui pillar tecnici)

Cappello strategico sopra i pillar tecnici operativi, che sono strumenti di esecuzione del framework, non pillar autonomi:

| Pillar tecnico | Presidio |
|----------------|----------|
| [[Processo-Quality-Pillar-Coding]] | Conformità prodotto ai requirement |
| [[Troubleshooting-UPS-Coding]] | Diagnosi evidence-based |
| [[Processo-Knowledge-Management-Coding]] | Cattura/retrieval conoscenza |
| [[Processo-Cost-Deployment]] | Visibilità costo trade-off |
| [[Processo-Review-Cadence]] | CI strategico periodico |

## Roadmap — Health check SMART + target zero-loss

### Foundation (0) — dichiarazione del principio + template riusabile

**End-state**: doppio livello dichiarato come principio + pillar tecnici noti ma applicazione disomogenea. Foundation include **A1 (framework dichiarato)** e **A2 (template riusabile)** per anticipare i meccanismi strutturali.

**Health check (verificabile da terzo):**

| ID | Metrica | Soglia | Tipo | Gaming mitigation |
|----|---------|--------|------|-------------------|
| F-HC1 | Esistenza nota canonica `Framework-Delivery-Piloti-Doppio-Livello` nel vault globale, aggiornata ≤6 mesi | presente + aggiornata | leading | nota citata da almeno 1 `.brain/` di pilota attivo |
| F-HC2 | Template riusabile `.brain/` + vault locale disponibile come scaffold forkabile | presente | leading | template ha una entry nel vault globale con istruzioni di init |
| F-HC3 | Evidenza applicazione per pilota attivo (OPL o CBA o loss chiusa nel `.brain/`) | **≥1 per pilota** | lagging | ciascuna OPL/CBA/loss deve avere ≥1 wikilink entrante |
| F-HC4 | Regole di scambio globale↔locale dichiarate | nota [[Strumenti-Filing-Brain-Globale-Locale|Filing-Brain-Globale-Locale]] esiste e riferisce il framework | leading | — |

**Finestra di valutazione**: **mensile** (review `/monthly`).

**Time-bound raggiungimento Foundation**: entro **2026-06-30** (fine giugno, 2 mesi dopo go-live AIOS — tempo per chiudere la dichiarazione dopo che il pilota primario è in produzione).

**Target zero-loss (negazione Health check):**

- Mesi con F-HC1 assente/non aggiornata da >6 mesi = **0**
- Mesi con F-HC2 assente una volta raggiunta Foundation = **0**
- Mesi con <1 evidenza F-HC3 per pilota attivo = **0**
- Mesi con regole di scambio assenti = **0**

---

### Stability (1) — AIOS framework locale completo, FT in setup

**End-state**: AIOS ha `.brain/` + vault Obsidian locale completo; FT ancora in setup. AIOS prioritario perché bet principale.

**Health check:**

| ID | Metrica | Soglia | Tipo | Gaming mitigation |
|----|---------|--------|------|-------------------|
| S-HC1 | `.brain/` AIOS **completo** — tutti i componenti: `knowledge/opl/` (≥3 flussi principali), `knowledge/cba/`, `debug/`, `knowledge/trade-offs/`, `knowledge/loss/` (loss chiuse promosse al globale) | tutti presenti e popolati | lagging | ogni OPL/CBA deve avere ≥1 wikilink entrante da altra nota (locale o globale) |
| S-HC2 | Vault Obsidian locale AIOS (che include `.brain/`) con frontmatter standard + MOC locale linkato a [[Sistema-Agentico-Studio]] + ≥1 nota per area KB intervista padre | presente | lagging | MOC locale citato da MOC globale |
| S-HC3 | FT ha **≥1 componente avviato** dei minimi S-HC1 (setup iniziato, non completato) | ≥1 | leading | componente citato da almeno un'altra nota |

**Finestra di valutazione**: mensile.

**Time-bound raggiungimento Stability**: entro **2026-05-31** (fine maggio, ≤2 settimane post go-live AIOS 2026-05-10).

**Target zero-loss:**

- Mesi post-go-live AIOS con S-HC1 sotto soglia (uno dei 5 componenti mancante) = **0**
- Mesi con S-HC2 sotto soglia = **0**
- Mesi con FT senza alcun componente avviato = **0**

---

### Predictability (2) — framework su N=2 + ciclo feedback reale bidirezionale

**End-state**: framework applicato a entrambi i piloti stabilmente + almeno un ciclo feedback locale→globale promosso e ricaduto in cascata sull'altro pilota (bidirezionale).

**Health check:**

| ID | Metrica | Soglia | Tipo | Gaming mitigation |
|----|---------|--------|------|-------------------|
| P-HC1 | FT raggiunge "Stability completo" (S-HC1 + S-HC2 pieni) | raggiunto | lagging | stessa gaming mitigation di S-HC1/S-HC2 |
| P-HC2 | Promozioni feedback **bidirezionali** (≥1 locale→globale **e** ≥1 globale→locale), per ogni pilota attivo | ≥1 in ogni direzione per pilota | lagging | ogni promozione citata in ≥1 review mensile (proof of use) prima di contare |
| P-HC3 | Ricaduta in cascata sull'altro pilota — principio promosso al globale ha (a) wikilink entrante dal secondo repo **e** (b) artefatto concreto nel secondo repo in cui è stato applicato | presente entrambe | lagging | — |

**Finestra di valutazione**: mensile + verifica trimestrale.

**Time-bound raggiungimento Predictability**: entro **fine Q3 2026** (2026-09-30). 3 mesi di vita operativa post go-live AIOS per generare ciclo feedback reale.

**Target zero-loss:**

- Trimestri post-Stability senza ≥1 promozione bidirezionale per pilota attivo = **0**
- Trimestri senza ≥1 ricaduta in cascata tracciata = **0**

---

### Agility (3) — feedback automatico + onboarding standardizzato + grafo navigabile

**End-state**: A3 (hook automatico) + A4 (onboarding pilota #3 in ≤1 giorno) + A5 (grafo navigabile da peer esterno in ≤30 min). A1 e A2 sono già Foundation.

**Health check:**

| ID | Metrica | Soglia | Tipo | Gaming mitigation |
|----|---------|--------|------|-------------------|
| A-HC1 | Hook/automazione feedback locale→globale attivo — trigger post-commit o equivalente che rileva nuove OPL/loss e propone promozione | hook presente e funzionante, ≥1 promozione reale/mese per ≥3 mesi | leading+lagging | check di funzionamento hook in review mensile |
| A-HC2 | Pilota #3 onboardato tramite scaffold standard + mappatura globale in **≤1 giorno di setup**, senza riadattamento ad-hoc | ≤1 giorno cronometrato | lagging | pilota #3 = progetto con stakeholder esterno reale + obiettivi di business propri (no esperimento interno) |
| A-HC3 | Peer tecnico esterno apre vault globale + vault locale e naviga collegamenti **senza assistenza founder** in ≤30 min | ≤30 min cronometrati | lagging | peer esterno reale, non founder |

**Finestra di valutazione**: mensile + re-test A-HC3 semestrale con peer diverso.

**Time-bound raggiungimento Agility**: entro **fine 2030**. Gated dall'apertura del filone B2B AIOS post abilitazione consulente del lavoro (2029).

**Target zero-loss:**

- Mesi con hook A-HC1 rotto = **0**
- Onboarding pilota #3 con durata >1 giorno = **0**
- Navigazione peer esterno >30 min = **0**

---

## Ancoraggi cross-pillar

### Verso Sales Positioning + Governance Reputazionale

Il framework a doppio livello **entra a far parte dell'offerta B2B di AIOS** (decisione strategica 2026-04-20). Il framework non è solo strumento interno: è asset vendibile agli studi peer come componente proposta di valore AIOS B2B.

- [[Vendite-Pillar-Sales-Positioning]] → framework = componente della proposta di valore B2B
- [[Vendite-Pillar-Governance-Reputazionale]] → B2B off-limits fino 2029, quindi commercializzazione framework gated dallo stesso vincolo

### Verso pillar tecnici operativi

I 5 pillar tecnici sono *strumenti* del framework: loro maturano per disciplina esecutiva, il pillar Delivery misura se il framework che li ospita è codificato/automatizzato/stress-testato.

## Pre-mortem (3 cause confermate)

1. Feedback locale→globale resta manuale senza A3/hook → ciclo si spezza sotto pressione.
2. Onboarding mai stress-testato per assenza di pilota #3 → framework resta ottimizzato per N=2 e collassa al primo nuovo progetto.
3. Divergenza grafo globale/locale per mancata disciplina di link → A5 evapora silenziosamente.

## Stato corrente (2026-04-20)

- **Fase pillar**: Foundation (0) in progresso
- **Foundation gap**: F-HC1 (nota canonica framework da creare), F-HC2 (template riusabile da creare), F-HC3 (evidenze ≥1 per pilota da verificare), F-HC4 (regole scambio già in [[Strumenti-Filing-Brain-Globale-Locale|Filing-Brain-Globale-Locale]] — verificare che riferisca il framework)
- **Prossimo movimento**: creazione nota `Framework-Delivery-Piloti-Doppio-Livello` + template riusabile `.brain/` + vault locale (target: entro fine maggio 2026, in parallelo a completamento Stability AIOS)

## Collegamenti

- [[Brainstorm-Obiettivi-Fase-Delivery-Piloti]] — sorgente Sessione 1+2
- [[Pillar-Doppio-Livello]] — distinzione pillar-fase vs progetto-stato
- [[Processo-Definizione-Obiettivi-Pillar]] — metodo
- [[Strumenti-Filing-Brain-Globale-Locale|Filing-Brain-Globale-Locale]] — regole scambio globale↔locale
- [[Sistema-Agentico-Studio]] · [[Football-Trading]]
- [[Processo-Quality-Pillar-Coding]] · [[Troubleshooting-UPS-Coding]] · [[Processo-Knowledge-Management-Coding]] · [[Processo-Cost-Deployment]] · [[Processo-Review-Cadence]]
- [[Vendite-Pillar-Sales-Positioning]] · [[Vendite-Pillar-Governance-Reputazionale]]
- [[OKR-Correnti]] · [[KR1.3 — Go-live studio padre]] · [[KR2.1 — Paper trading debuggato]]
