---
tipo: concetto
creato: 2026-04-20
aggiornato: 2026-04-20
stato: attivo
tags:
  - pillar/strategico
  - strategia/leadership
area: strategia
pillar-fase: Foundation
pillar-fase-num: 0
pillar-loss:
  - Finestra-competitiva-persa
---

# Pillar — Leadership strategica

> [!info] In una frase
> Pillar di **governance del sistema strategico**: presidia la coerenza tra parti del business e strategia globale, la visibilità dello stato di avanzamento, e la capacità di riallocare tempo/attenzione per non perdere la finestra competitiva (loss #1, rischio endogeno).

## Loss proprietarie

| # | Loss bucket |
|---|-------------|
| #1 | Finestra competitiva persa — competitor più veloce occupa lo spazio dell'AI-per-piccole-realtà prima che arrivi al mercato |

## Obiettivi di fase (end-state) — Sessione 1

Definiti il 2026-04-20 via Backcasting su end-state Agility (vedi [[Brainstorm-Obiettivi-Fase-Leadership-Strategica]]).

### Foundation — end-state

Le basi di governance sono dichiarate e scritte:

- Strategia formulata come artefatto scritto ([[Strategia-Attuale]])
- OKR trimestrali attivi e operativi ([[OKR-Correnti]])
- Tutti i 7 pillar strategici mappati ([[Pillar-Doppio-Livello]])
- Per ciascuno dei 7 pillar: end-state delle 4 fasi + Health check + target zero-loss/zero-defect mappati
- Mappa concreta pillar↔sistemi con processi I/O dichiarati (artefatto nuovo, oggi non esiste; principio architetturale in [[Sistemi-Sotto-Pillar]])

### Stability — end-state

L'infrastruttura di governance funziona in modo ripetibile:

- Vault + Dashboard + mappa pillar × progetti esistono, vengono aggiornati, reggono il carico (non è ancora "al regime automatico")
- [[Processo-Review-Cadence|Review cadence]] installata: weekly + monthly girano regolari per almeno 1 trimestre consecutivo

### Predictability — end-state

Il sistema produce dati e decisioni disciplinate:

- Pipeline di segnali attiva a regime: scouting competitivo + monitoraggio regolatorio ([[Strategia-Pillar-Monitoraggio-Regolatorio]]) + feedback mercato piloti
- Trade-off cross-filone decisi con chiavi esplicite di conversione ([[Processo-Cost-Deployment]] maturo) — non più per istinto

### Agility — end-state

Il founder e il sistema operano in modo adattivo e sono riconosciuti:

- **A** — Scouting strategico fluido: individui vantaggi competitivi e li colleghi con agilità a una strategia che ne scala la redditività
- **B** — Governance adattiva cross-filone: ridefinisci la strategia in risposta a segnali endogeni/esogeni; il sistema operativo rende visibili collegamenti e avanzamento di ogni parte rispetto alla strategia globale
- **C** — Validazione esterna: peer/imprenditori ti cercano per consulenza strategica perché sai adattarti ai cambiamenti meglio di loro

## Scelta architetturale dichiarata

La **disciplina personale sul focus del bet** (MIT saltati = 0 per N settimane consecutive) **non è end-state di fase** di questo pillar. Leadership strategica è pillar di governance del sistema (infrastruttura + processi), non di autodisciplina.

## Health check e target zero-loss — Sessione 2

Definiti il 2026-04-20 (vedi [[Brainstorm-Obiettivi-Fase-Leadership-Strategica]]). Framework: SMART + Leading/Lagging + Goodhart test.

### Foundation — Health check (target 2026-04-30)

| # | Health check | Tipo |
|---|--------------|------|
| HC-F1 | [[Strategia-Attuale]] esiste con `aggiornato` ≤ 3 mesi rolling | Lagging |
| HC-F2 | [[OKR-Correnti]] esiste con trimestre corrente dichiarato e KR attivi | Lagging |
| HC-F3 | 7/7 pillar con *Obiettivi di fase* + *Health check* + *Target zero-loss* popolati (no TBD/placeholder) | Lagging |
| HC-F4 | [[Sistemi-Sotto-Pillar]] esistente + mappa concreta pillar↔sistemi come nota dedicata | Lagging |

**Goodhart mitigazioni**: HC-F1 → verifica coerenza OKR↔strategia a review mensile, non solo data; HC-F2 → ogni KR con scadenza dentro il trimestre attuale; HC-F3 → scan automatico no occorrenze TBD/placeholder; HC-F4 → mappa con almeno 1 riga per pillar + I/O dichiarato per riga.

**Target zero-loss Foundation**: *numero di pillar senza end-state + HC + target zero-loss completi al 2026-04-30 = 0*.

### Stability — Health check (target 2026-07-26)

| # | Health check | Tipo |
|---|--------------|------|
| HC-S1 | `.base` pillar × progetti renderizza senza errore, tutti i 7 pillar con `pillar-fase-num` coerente col contenuto narrativo | Lagging |
| HC-S2 | Catena continua weekly in `10-Diario/Settimanale/` per ≥ 1 trimestre consecutivo, senza buchi | Lagging + Leading implicito |
| HC-S3 | 3 note monthly consecutive in `10-Diario/Mensile/` | Lagging + Leading implicito |
| HC-S4 | Ogni weekly del trimestre contiene sezione "review pillar" strutturata come da [[Processo-Review-Cadence]] | Misto |

**Goodhart mitigazioni**: HC-S1 → check mensile coerenza frontmatter ↔ sezione "Stato corrente" di ogni pillar; HC-S2 → data creazione file ≤ domenica della settimana di riferimento; HC-S3 → review pillar con contenuto differenziato trimestre su trimestre; HC-S4 → almeno 1 riga di stato reale per ogni pillar, anche "no evidenza" esplicita.

**Target zero-loss Stability**: *note weekly + monthly mancanti o senza review pillar strutturata nel trimestre di riferimento = 0*.

### Predictability — Health check (target 2027-03-31)

| # | Health check | Tipo |
|---|--------------|------|
| HC-P1 | Scouting competitivo: ≥ 1 scan/mese nelle ultime 3 mensilità rolling | Leading |
| HC-P2 | Tutti i 6 altri pillar strategici in Stability o oltre | Lagging + gate di sistema |
| HC-P3 | Piloti attivi (qualunque siano in quel momento) con canale feedback cliente + ≥ 1 review/mese per pilota | Leading |
| HC-P4 | Registro trade-off cross-filone con chiavi di conversione [[Processo-Cost-Deployment|Cost Deployment]]: ≥ 10 trade-off storici negli ultimi 2 mesi rolling | Lagging + Leading implicito |

**Goodhart mitigazioni**: HC-P1 → ogni scan cita ≥ 1 competitor nuovo o ≥ 1 segnale nuovo su competitor noto; HC-P2 → le mitigazioni Goodhart di ciascun pillar sono già il backstop; HC-P3 → ogni review produce ≥ 1 azione di modifica prodotto o decisione di non-modifica motivata; HC-P4 → ogni riga mostra opzioni multiple con costo atteso numerico, non solo "ho scelto X".

**Target zero-loss Predictability**: *trade-off cross-filone significativi non registrati con chiavi = 0 nel trimestre*.

### Agility — Health check (target 2029-2030)

| # | Health check | Tipo |
|---|--------------|------|
| HC-A1 | ≥ 3 pivot strategici effettivi/anno (apertura/chiusura filone o riorientamento bet principale), documentati con "segnale → alternativa scartata → decisione" | Lagging |
| HC-A2 | Time-to-reallocate ≤ 2 settimane fra segnale di contesto e azione di riallocazione eseguita (eccezioni documentate ammesse) | Leading |
| HC-A3 | ≥ 1 richiesta di consulenza strategica/semestre da peer/imprenditori non in relazione commerciale | Lagging |

**Goodhart mitigazioni**: HC-A1 → pivot definito come apertura/chiusura filone o riorientamento bet principale documentato, non cambi minori; HC-A2 → "azione di riallocazione" = ≥ 1 MIT settimanale spostato, o ≥ 1 voce OKR modificata, o ≥ 1 trade-off registrato; HC-A3 → richiedente peer/imprenditore, non cliente AIOS né scommettitore FT.

**Target zero-loss Agility**: *segnali strategici rilevanti non seguiti da decisione documentata entro 2 settimane (esclusa eccezione documentata) = 0*. Coincide con la negazione di HC-A2 applicata al flusso continuo.

## Stato corrente

- **Fase**: 0 Foundation — **chiudibile condizionatamente al 2026-04-25** (con 5gg di anticipo sul target 2026-04-30)
- **Stato HC Foundation**:
	- HC-F1 ✓ [[Strategia-Attuale]] aggiornata
	- HC-F2 ✓ [[OKR-Correnti]] Q2 2026 attivi
	- HC-F3 ✓ 7/7 pillar con end-state + Health check + target zero-loss popolati
	- HC-F4 ✓ [[Sistemi-Sotto-Pillar]] esistente + **mappa concreta** scritta in [[Strategia-Mappa-Pillar-Sistemi]] (2026-04-25)
- **Gap residuo per chiusura formale**: promozione a forma canonica di 3 sistemi parziali (Pianificazione Giornaliera, Validazione Pilot, Cattura-Retrieval Info) entro 2026-04-30
- **Debito architetturale concatenato**: allineare skill `/weekly` e `/monthly` a [[Processo-Review-Cadence]] (precondizione per HC-S4)

## Rischi di fallimento identificati (Pre-mortem Sessione 1)

1. Review cadence installata sulla carta ma salta nelle settimane critiche → dati inconsistenti → Predictability non parte
2. Pipeline segnali trattata "a sensazione" → Predictability resta aneddotica
3. Mappa pillar↔sistemi mai costruita → pillar diventano burocrazia parallela ai sistemi invece che loro governance

## Collegamenti

- [[Brainstorm-Obiettivi-Fase-Leadership-Strategica]] — Sessione 1 + Sessione 2 sorgente
- [[Processo-Definizione-Obiettivi-Pillar]] — processo applicato
- [[Pillar-Doppio-Livello]] · [[Zero-Loss-Mindset]] · [[Framework-Codificato-Per-Loss]] · [[Sistemi-Sotto-Pillar]] — meta-architettura (4 facce)
- [[Strategia-Attuale]] · [[OKR-Correnti]] · [[Crescita-Priorità-Correnti]]
- [[Valori-Fondamentali#Velocità]] · [[Valori-Fondamentali#Efficacia]]
- [[Processo-Cost-Deployment]] · [[Processo-Review-Cadence]]
