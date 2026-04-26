---
tipo: concetto
creato: 2026-04-20
aggiornato: 2026-04-20
stato: attivo
tags:
  - pillar/strategico
  - vendite/governance
  - reputazione
area: vendite
pillar-fase: Foundation
pillar-fase-num: 0
pillar-loss:
  - Contaminazione-relazione-studio-clienti
---

# Pillar — Governance reputazionale

> [!info] In una frase
> Presidia il confine fra ruolo di consulente (verso clienti del padre e, in futuro, propri) e ruolo di venditore di software: evita che un tentativo di cross-selling B2B peer prematuro contamini le relazioni fornitore↔cliente già attive e il network del padre (notai, consulenti del lavoro).

## Loss proprietarie

| # | Loss bucket |
|---|-------------|
| #2 | Contaminazione relazione studio → clienti — i clienti commerciali/contabili di oggi sono potenziali clienti AIOS di domani; una mossa sbagliata rompe entrambe le relazioni |

## Obiettivi di fase (4 end-state)

Sorgente: [[Brainstorm-Obiettivi-Fase-Governance-Reputazionale]] (2026-04-20).

| Fase | End-state |
|------|-----------|
| **0 Foundation** | Vincolo reputazionale riconosciuto come principio strategico + **mappa iniziale network padre** classificata MECE per posizione strategica (4 categorie: target B2B futuro / off-limits / neutro / alleati) + zero mosse B2B peer |
| **1 Stability** | **Policy scritta** segmenti approcciabili vs off-limits + **status di praticante consulente del lavoro** avviato nello studio |
| **2 Predictability** | **Abilitazione consulente del lavoro acquisita** + primi outreach B2B peer mossi con **zero eventi di contaminazione** |
| **3 Agility** | Riferimento del Golfo di Gaeta + proattività bidirezionale (cross-sell clienti + B2B peer) + **inbound spontaneo** da peer, clienti, terzi |

## Health check SMART per fase

### Foundation (time-bound 2026-06-30)

| ID | Misura | Soglia | Tipo |
|----|--------|--------|------|
| HC-F1 | Contatti classificati MECE {target B2B / off-limits / neutro / alleati} | **≥ 30** | Leading |
| HC-F2 | Outreach B2B peer espliciti/formali prima di policy scritta | **= 0** | Zero-loss |
| HC-F3 | Revisione mappa — giorni dall'ultima | **≤ 30** (mensile) | Leading |

Goodhart: HC-F1 mitigato da **campione di 3 random rivisitati** a ogni review mensile (no target di riclassificazione). HC-F3 mitigato da revisione che tocca **≥ 3 persone esistenti**. Esclusione esplicita HC-F2: outreach impliciti (chiacchiere, post LinkedIn tecnici) fuori dal contatore.

### Stability (time-bound praticantato ≤ 2027-12-31)

| ID | Misura | Soglia | Tipo |
|----|--------|--------|------|
| HC-S1 | Copertura policy cross-selling sui segmenti della mappa | **100%** | Lagging |
| HC-S2 | Iscrizione praticantato Ordine consulenti del lavoro | **entro 2027-12-31** | Lagging binario |
| HC-S3 | Policy rivista a ogni aggiunta/riclassificazione mappa | **100% trigger** | Leading |
| HC-S4a | Outreach B2B peer in Stability — probe controllati | **≤ 2** | Lagging volume |
| HC-S4b | Eventi di contaminazione dai probe | **= 0** | Zero-loss |

> [!tip] Volume vs contaminazione
> HC-S4a/b **separano volume da contaminazione**. I probe sono esperimenti intenzionali per raccogliere evidenza prima di Pred; la metrica intoccabile è contaminazione = 0, non "zero tentativi".

### Predictability (time-bound abilitazione ≤ 2029-06-30)

| ID | Misura | Soglia | Tipo |
|----|--------|--------|------|
| HC-P1 | Abilitazione consulente del lavoro acquisita | **entro 2029-06-30** | Lagging binario |
| HC-P2 | Volume outreach B2B peer | **≥ 3/anno** | Leading |
| HC-P3 | % outreach con gate checklist policy applicato | **100%** | Leading |
| HC-P4 | Eventi di contaminazione (a/b/c/d sotto) | **= 0** su intera durata Pred | Zero-loss |

> [!danger] Definizione operativa "evento di contaminazione"
> Quattro tipi, tutti pesano uguale, tutti "da evitare come la peste":
> - **(a)** peer approccia il padre lamentandosi dopo un tuo outreach
> - **(b)** cliente dello studio del padre ti percepisce/definisce esplicitamente come "venditore di software" (segnale riportato da terzi)
> - **(c)** peer rifiuta una presentazione formale del padre citando il tuo approccio precedente
> - **(d)** introduzione del padre verso un peer si chiude negativamente per ragioni legate a un tuo contatto pregresso

### Agility (time-bound ingresso 2030-2031)

| ID | Misura | Soglia | Tipo |
|----|--------|--------|------|
| HC-A1 | Inbound peer spontaneo (commercialisti/consulenti del lavoro) | **≥ 5/anno** | Lagging |
| HC-A2 | Presentazioni da clienti al loro network | **≥ 2/anno** | Lagging |
| HC-A3 | Citazioni da notai/banche/associazioni locali | **≥ 2/anno** | Lagging |
| HC-A4 | Eventi di contaminazione | **= 0** rolling 12 mesi | Zero-loss |
| HC-A5 | Volume outreach B2B peer | **in crescita** vs anno precedente | Leading |

**Denominatore territoriale**: 15 studi commerciali/consulenza del lavoro nel Golfo di Gaeta. HC-A1 = 5/15 = 33% penetrazione annuale.

## Target zero-loss sintetici

Il **gate critico unico** che attraversa tutte le fasi è **contaminazione = 0**. Una singola contaminazione in qualunque fase blocca l'avanzamento.

| Target | Finestra |
|--------|----------|
| Mesi con `contatti classificati < 30` dopo 2026-06-30 | **= 0** |
| Outreach B2B peer prima di policy Stability | **= 0** assoluto |
| Mesi senza revisione mappa | **= 0** |
| Probe Stability con contaminazione | **= 0** |
| Outreach Pred senza gate checklist policy | **= 0** |
| Eventi di contaminazione (a/b/c/d) Pred | **= 0** intera durata |
| Anni Agility con contaminazione | **= 0** rolling 12 mesi |

## Sub-step per avanzamento

- **0 → 1**: completare mappa network ≥ 30 contatti classificati MECE entro 2026-06-30 + scrivere policy cross-selling 100% copertura segmenti
- **1 → 2**: iscrivere praticantato Ordine consulenti del lavoro entro 2027-12-31 + eseguire ≤ 2 probe controllati con zero contaminazione
- **2 → 3**: ottenere abilitazione entro 2029-06-30 + mantenere ≥ 3 outreach/anno con checklist 100% e contaminazione = 0 per intera durata Pred
- **3 → mantenimento Agility**: consolidare inbound spontaneo ≥ 5/anno peer + ≥ 2/anno clienti + ≥ 2/anno terzi, rolling annuale

## Stato corrente

- **Fase**: 0 Foundation — vincolo riconosciuto in [[Strategia-Attuale]] ma mappa network non ancora costruita, policy non scritta
- **Gap a Stability**: (a) mappa ≥ 30 contatti classificati MECE da costruire entro 2026-06-30, (b) policy scritta con 100% copertura segmenti da redigere, (c) iscrizione praticantato da pianificare verso 2027-12-31
- **Prossima azione**: catturare primi 30 contatti del network padre + impostare file mappa con 4 categorie MECE

## Collegamenti

- [[Brainstorm-Obiettivi-Fase-Governance-Reputazionale]] — sorgente Sessione 1 + 2
- [[Processo-Definizione-Obiettivi-Pillar]] — metodo applicato
- [[Pillar-Doppio-Livello]] · [[Zero-Loss-Mindset]] · [[Framework-Codificato-Per-Loss]]
- [[Strategia-Attuale#Il vincolo di reputazione (principio non negoziabile)]]
- [[Identità]] — identità consulente da consolidare prima di espansione B2B
- [[Sistema-Agentico-Studio]] — prodotto oggetto del vincolo B2B
- [[Studio-Del-Padre-Piattaforma]] — network di riferimento
- [[Vendite-Pillar-Sales-Positioning]] — pillar gemello sul fronte vendita
- [[Relazioni-Pillar-Network-Target]] — pillar adiacente (network post-transizione)
