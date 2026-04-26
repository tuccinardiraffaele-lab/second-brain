---
tipo: concetto
creato: 2026-04-20
aggiornato: 2026-04-25
stato: attivo
tags:
  - concetto/p-g-iws
  - principio/meta
  - strategia/sistema
area: conoscenza
---

# Sistemi sotto pillar

> [!info] In una frase
> Sotto ogni pillar si agganciano **sistemi** con processi di input/output chiari: il pillar è il proprietario della loss e degli obiettivi di fase; il sistema è il meccanismo operativo attraverso cui il pillar raggiunge i suoi obiettivi. Un sistema può servire più pillar (cross-pillar).

## Il principio

- **Pillar** = governance. Proprietario formale di una classe di loss (MECE) + obiettivi di fase + Health check + target zero-loss. Il pillar non esegue — decide cosa deve essere vero.
- **Sistema** = meccanismo operativo. Processo con input e output dichiarati che produce gli outcome richiesti dal pillar. Il sistema esegue.
- **Relazione**: ogni pillar è agganciato a uno o più sistemi; ogni sistema serve uno o più pillar. La relazione è un grafo, non una tabella 1:1.

Senza sistemi il pillar diventa burocrazia (dichiara ma non produce). Senza pillar il sistema diventa improvvisazione (produce senza ownership della loss).

## Quarta faccia della meta-architettura P&G

Triade meta già in vault: [[Pillar-Doppio-Livello]] + [[Zero-Loss-Mindset]] + [[Framework-Codificato-Per-Loss]]. Questo principio è la **quarta faccia**:

| Principio | Dimensione presidiata |
|---|---|
| [[Pillar-Doppio-Livello]] | *Chi* presidia — tassonomia MECE di proprietà |
| [[Zero-Loss-Mindset]] | *Perché* si agisce — rifiuto ontologico + risorse scalabili |
| [[Framework-Codificato-Per-Loss]] | *Come* si agisce — gerarchia strumenti + 1 record vivo |
| **Sistemi sotto pillar** (questa) | *Con cosa* si agisce — meccanismi operativi collegati ai pillar via I/O |

Senza la quarta faccia, il pillar resta un'entità dichiarativa scollegata dall'esecuzione.

## Esempio dichiarato dal founder

> [!example] Quality coding → Delivery piloti
> Il [[Processo-Quality-Pillar-Coding|sistema del Quality pillar (tecnico, coding)]] si aggancia al pillar strategico [[Prodotto-Pillar-Delivery-Piloti|Delivery piloti]]. Il pillar Delivery piloti dichiara gli obiettivi di fase (piloti in produzione, metriche pilot raggiunte); il sistema Quality coding garantisce che quegli obiettivi siano raggiunti *con conformità al requirement*, non solo con codice che compila.

Questo esempio chiarisce due proprietà:

1. **I sistemi esistenti nel vault (pillar tecnici coding) non duplicano i pillar strategici** — li servono.
2. **Un sistema può servire più pillar**: Quality coding serve Delivery piloti ma anche Governance reputazionale (difetto visibile al cliente B2C erode reputazione).

## Forma canonica di un sistema

Per qualificarsi come "sistema" sotto un pillar, serve:

- **Input dichiarato**: cosa entra (trigger, dati, evento, richiesta)
- **Output dichiarato**: cosa esce (artefatto, decisione, misura, gate superato)
- **Processo**: sequenza di passi codificata (non improvvisata)
- **Owner operativo**: chi lo fa girare (nel single-founder: quale time-block/contesto)
- **Agganci pillar**: quali pillar consuma l'output come evidenza di avanzamento

Senza I/O dichiarati, è un'attività, non un sistema.

## Oggi in vault — sistemi già codificati

Inventario parziale (da completare quando si costruirà la mappa concreta):

- [[Processo-Quality-Pillar-Coding]] — Quality coding
- [[Troubleshooting-UPS-Coding]] — UPS per diagnosi
- [[Processo-Knowledge-Management-Coding]] — OPL/CBA push-based
- [[Processo-Cost-Deployment]] — rendere visibili trade-off
- [[Processo-Review-Cadence]] — cadenza DMS adattata
- [[Processo-Definizione-Obiettivi-Pillar]] — definizione end-state pillar (serve Leadership strategica)
- [[Processo-Pianificazione-Giornaliera]] — sistema operativo personale (forma canonica 2026-04-25)
- [[Processo-Validazione-Pilot]] — verdetto pass/fail/inconclusive su pilot in produzione (forma canonica 2026-04-25)
- [[Processo-Cattura-E-Retrieval-Informazioni]] — infrastruttura cattura+retrieval del brain globale (forma canonica 2026-04-25)

La **mappa concreta pillar↔sistemi** è stata scritta il 2026-04-25 in [[Strategia-Mappa-Pillar-Sistemi]] via architettura multi-agent. **HC-F4 chiusa il 2026-04-25** con la promozione a forma canonica dei 3 sistemi parziali; con essa è chiuso l'intero step Foundation del pillar [[Strategia-Pillar-Leadership-Strategica]].

## Implicazione per i nuovi sistemi

Quando nasce l'esigenza di un nuovo sistema (es. pipeline monitoraggio regolatorio, sistema scouting competitivo):

1. Identificare il pillar proprietario della loss servita
2. Dichiarare I/O + processo + owner operativo prima di eseguirlo
3. Registrare aggancio nel pillar e, viceversa, nel sistema (bidirezionale)

Senza questi passi, il sistema nasce scollegato dalla governance e si perde la tracciabilità loss→esecuzione.

## Collegamenti

- [[Procter-And-Gamble]] — origine IWS
- [[Pillar-Doppio-Livello]] · [[Zero-Loss-Mindset]] · [[Framework-Codificato-Per-Loss]] — altre 3 facce della meta-architettura
- [[Strategia-Pillar-Leadership-Strategica]] — pillar che dichiara la mappa pillar↔sistemi come artefatto Foundation
- [[Processo-Definizione-Obiettivi-Pillar]] — processo che precede la costruzione della mappa
- [[Brainstorm-Obiettivi-Fase-Leadership-Strategica]] — sede originaria dell'insight
