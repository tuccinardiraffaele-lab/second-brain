---
tipo: concetto
creato: 2026-04-20
aggiornato: 2026-04-20
stato: attivo
tags:
  - concetto/p-g-iws
  - principio/meta
  - strategia/sistema
area: conoscenza
---

# Pillar come doppio livello

> [!info] In una frase
> Il pillar opera **simultaneamente** come gate operativo locale oggettivo (Health check + Audit per avanzare di fase) e come inventario strategico cross-entità (mappa aggregata di maturità pillar × entità sempre pronta, che guida le decisioni strategiche quando la domanda arriva dal mercato).

## Il principio in P&G IWS

In Procter & Gamble, ogni sito manifatturiero avanza nelle 4 fasi IWS — **Foundation → Stability → Predictability → Agility** — solo se **tutti i 12 pillar** raggiungono il livello richiesto dalla fase successiva. Nessun cherry-picking: un pillar indietro blocca il passaggio di fase dell'intero sito. La maturità è oggettiva, certificata da **Health check** e **Audit**, mai interpretativa.

A livello aziendale, P&G non guida gli investimenti dai pillar. Il capex segue la strategia di mercato. Ma l'azienda **sa sempre in anticipo quale sito attivare** perché la mappa aggregata pillar × sito è sempre disponibile.

## Rationale generativo

La tassonomia dei 12 pillar P&G **non è MECE per funzione aziendale**. È MECE per **proprietario di classe di loss**. La domanda generativa originale:

> *"Qual è il loss tree del sito — e chi deve essere il proprietario formale di ciascuna classe di perdita?"*

Ogni pillar = guardiano di una classe di loss. Niente pillar "Cost" (Cost Deployment è strumento trasversale), niente pillar "Innovation" stand-alone. Dal loss tree + criterio di proprietà esclusiva nascono i pillar, non al contrario.

## Pillar-fase ≠ progetto-stato (distinzione fondamentale)

Due dimensioni **ortogonali**, spesso confuse:

| Dimensione | Cosa misura | Esempio Delivery piloti |
|-----------|-------------|-------------------------|
| **Fase del pillar** | Maturità del **framework** che il pillar rappresenta (SOP definite, KB codificata, processi formalizzati, Health check misurabili) | "Il framework di delivery come insieme di SOP/KB/checklist di go-live è dichiarato ma non ancora codificato" |
| **Stato del progetto** | Avanzamento operativo di un progetto specifico che **applica** quel framework | "FT è in fase di debugging P&L; AIOS ha soglie fissate" |

**Il pillar Delivery piloti in Foundation NON significa "FT e AIOS sono in Stability"**. La fase del pillar descrive la maturità del **framework sottostante**. Lo stato dei progetti vive nelle MOC dei progetti (`20-Iniziative/🔥-Attive/<Progetto>/`), non nella nota pillar.

Conseguenza operativa: la mappa aggregata `pillar × progetto` è una **matrice** in cui:
- Riga pillar indica la maturità del framework (governance)
- Colonna progetto indica lo stato specifico (esecuzione)
- L'incrocio è utile per capire dove il progetto può contare su framework maturo e dove no

## La triade dei principi meta P&G

Questo principio è **una delle tre facce** dello stesso sistema:

| Principio | Dimensione che presidia | Nota |
|-----------|-------------------------|------|
| **Pillar a doppio livello** (questa) | *Chi* presidia — tassonomia MECE di proprietà | — |
| **Zero-Loss Mindset** | *Perché* si agisce — rifiuto ontologico + risorse scalabili | [[Zero-Loss-Mindset]] |
| **Framework codificato per tipo di loss** | *Come* si agisce — gerarchia strumenti + misurabilità + 1 record vivo | [[Framework-Codificato-Per-Loss]] |

I tre stanno insieme. Senza uno, gli altri due non tengono:
- Senza pillar → zero-loss diventa sentimento, framework diventa improvvisazione
- Senza zero-loss → pillar diventano burocrazia, framework diventa teatro
- Senza framework → pillar mappano proprietà senza sapere cosa fare

## Applicazione al mio sistema strategico

### Loss tree strategica (8 classi, chiuse il 2026-04-20)

| # | Classe di loss |
|---|----------------|
| 1 | Finestra competitiva persa |
| 2 | Contaminazione relazione studio → clienti |
| 3 | Identità consulente del lavoro non costruita |
| 4 | Networking target post-transizione non coltivato |
| 5 | Vantaggio asimmetrico Lean/corporate non attivato |
| 6 | Rischio regolatorio non monitorato |
| 7 | Capability marketing & sales mancante |
| 8 | Maturità piloti non raggiunta entro finestra competitiva |

**Fuori perimetro**: capitale personale (pre-condizione, sarà dismessa a transizione completata).

### Tassonomia 7 pillar strategici

| # | Pillar | Loss bucket | Sottodominio |
|---|--------|-------------|--------------|
| 1 | [[Strategia-Pillar-Leadership-Strategica]] | #1 | 32-Strategia-Business |
| 2 | [[Vendite-Pillar-Governance-Reputazionale]] | #2 | 36-Vendite-e-Crescita |
| 3 | [[Crescita-Pillar-Studio-Giuridico]] | #3 | 38-Crescita-Personale |
| 4 | [[Relazioni-Pillar-Network-Target]] | #4 | 39-Relazioni-e-Network |
| 5 | [[Vendite-Pillar-Sales-Positioning]] | #5, #7 | 36-Vendite-e-Crescita |
| 6 | [[Strategia-Pillar-Monitoraggio-Regolatorio]] | #6 | 32-Strategia-Business |
| 7 | [[Prodotto-Pillar-Delivery-Piloti]] | #8 | 33-Prodotto-e-Tecnologia |

### Scala fasi (0-3)

| Fase-num | Fase | Significato generico P&G |
|----------|------|--------------------------|
| 0 | Foundation | Basi dichiarate, standard minimo, awareness |
| 1 | Stability | Performance consistente, processi ripetibili |
| 2 | Predictability | Operazione prevedibile con metriche stabili |
| 3 | Agility | Operazioni adattive, risposta rapida al cambiamento |

Il significato specifico di ogni fase per ogni pillar va **derivato dalla natura del pillar**, non applicato meccanicamente.

### Livello operativo — pillar tecnici esistenti

I pillar tecnici codificati (sprint 2026-04-17) **non duplicano** i 7 strategici: stanno **sotto il pillar #7 Delivery piloti** come strumenti operativi:

- [[Processo-Quality-Pillar-Coding]]
- [[Troubleshooting-UPS-Coding]]
- [[Processo-Knowledge-Management-Coding]]
- [[Processo-Cost-Deployment]]
- [[Processo-Review-Cadence]]

## Scaffold delle loss strategiche

Le loss strategiche (pillar 1-6, non-coding) vivono nel vault globale direttamente — non passano dal brain locale (che è territorio coding).

**Path**: `30-Dominio/<sottodominio>/Loss-<PillarSlug>-<YYYY-MM-DD>-<slug>.md`

Esempi:
- `30-Dominio/32-Strategia-Business/Loss-Leadership-2026-04-20-MIT-Saltato-AIOS.md`
- `30-Dominio/38-Crescita-Personale/Loss-Studio-Giuridico-2026-05-03-Giorno-Senza-Studio.md`

**Frontmatter standard**:

```yaml
---
tipo: loss
creato: YYYY-MM-DD
pillar: "[[NomePillar]]"
livello: 1 | 2 | 3
stato: aperta | chiusa
failure-mode: <descrizione sintetica>
classificazione-chiusura: A | B | C | N/A
tags:
  - loss/<pillar-slug>
area: <area>
---
```

**Cattura istantanea**: quando una loss strategica si manifesta, entry immediata in quella cartella. Niente batch, niente "la scrivo alla weekly". Coerente con Mossa 4 di [[Zero-Loss-Mindset]].

**Promozione globale**: le loss strategiche sono **già** nel vault globale. Non c'è promozione ulteriore. La detection cross-progetto riguarda solo le loss coding (che nascono nel brain locale e vengono promosse via `/sprint`).

## Meccanismo di avanzamento automatico

Trigger nella [[Processo-Review-Cadence|Review Cadence]] a granularità crescente:

| Cadenza | Granularità | Azione |
|---|---|---|
| **Weekly** | Superficiale | Capture evidenze attività pillar + loss catturate nella settimana |
| **Monthly** | Health check oggettivi | Review Health check aperti. Step completato → avanzamento automatico `pillar-fase-num` |
| **Trimestrale** | Roadmap pillar | Verifica coerenza roadmap con strategia; ridisegno eventuale |

**Infrastruttura**:
- Ogni nota pillar ha frontmatter strutturato (`pillar-fase`, `pillar-fase-num`, `pillar-loss`)
- `.base` aggregante renderizza la matrice pillar × progetto in Dashboard
- L'edit del frontmatter ricalcola automaticamente la mappa

## Collegamenti

- [[Procter-And-Gamble]] — origine del principio
- [[Zero-Loss-Mindset]] · [[Framework-Codificato-Per-Loss]] — triade
- [[Processo-Quality-Pillar-Coding]] · [[Troubleshooting-UPS-Coding]] · [[Processo-Knowledge-Management-Coding]] · [[Processo-Cost-Deployment]] · [[Processo-Review-Cadence]] — pillar tecnici operativi
- [[Strategia-Attuale]] · [[OKR-Correnti]] · [[Identità]]
- [[Valori-Fondamentali#Efficacia]]
- [[Dashboard]]
