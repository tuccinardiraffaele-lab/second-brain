---
tipo: processo
creato: 2026-04-17
aggiornato: 2026-04-17
stato: attivo
tags:
  - processo/knowledge-management
  - strumenti/claude-code
  - metodo/iws
area: strumenti
---

# Knowledge Management — Coding

> [!info] In una frase
> Adattamento al coding di **OPL (One Point Lesson)**, **CBA (Current Best Approach)** e del principio **push-based** del DMS di [[Procter-And-Gamble|P&G IWS]]: un sistema che cattura la conoscenza nel momento in cui emerge e la porta all'operatore quando serve — senza che debba cercarla.

## Origine

Derivato da tre meccanismi IWS di [[Procter-And-Gamble]]:
- **OPL**: documento di una pagina, prevalentemente visivo, creato dall'operatore nel momento in cui risolve un problema o impara qualcosa. Tre tipi: Basic Knowledge, Problem Case, Improvement Case.
- **CBA (Current Best Approach)**: lo standard operativo corrente per un processo intero. Richiama le OPL dei singoli componenti + prescrizioni di sicurezza, qualità, rischi, e come verificare che l'esecuzione sia corretta. È la migliore pratica *nota ad oggi*, aggiornabile.
- **DMS push-based**: la conoscenza non va cercata — il DMS (Daily Management System) la porta all'operatore tramite checklist prescrittive, DDS (Daily Direction Setting) e centerline. Il design rende quasi impossibile *non* trovare l'informazione giusta.

## Problema che risolve

Copre due tipi di perdita identificati nella loss map di [[Processo-Quality-Pillar-Coding]]:

| # | Perdita | Sintomo concreto |
|---|---------|-----------------|
| 10 | **Conoscenza non catturata** | Claude Code confonde l'XGBoost per probabilità (eliminato) con quello per context threshold (attivo). Il flusso Redis → pipeline → DB non è esplicitato — ogni operazione di pulizia o debug è un'indovinata |
| 11 | **Conoscenza non trovabile** | La roadmap ristrutturata AIOS esisteva nel repo ma Claude Code non l'ha cercata prima di implementare — risultato: implementazioni disallineate, rework |

### La catena di failure

1. Una decisione viene presa in una sessione di coding (es. "eliminiamo l'XGBoost per le probabilità")
2. La decisione non viene scritta da nessuna parte nel brain locale
3. Nella sessione successiva, Claude Code non ha contesto → risponde in modo incoerente o implementa cose disallineate
4. Il founder non è esperto di coding → non può verificare se Claude Code sta usando il contesto giusto
5. Il disallineamento emerge solo quando i risultati sono sbagliati → massimo costo di rework

## Il sistema: cattura + retrieval

### Livello 1 — OPL (One Point Lesson) → nota atomica nel brain locale

Per ogni componente critico del sistema, una nota atomica nel brain locale (`<repo>/.brain/`) che descrive:

- **Cosa fa il componente** — in termini di comportamento del prodotto, non di codice
- **Cosa entra e cosa esce** — input/output concreti
- **Come verificare che funzioni** — il test operativo, non il test del codice
- **Decisioni prese** — cosa è stato cambiato e perché (es. "XGBoost per probabilità eliminato perché produceva data leak")

> [!danger] Regola di cattura
> La OPL si crea **nel momento in cui la conoscenza emerge** — durante la sessione di coding, non a fine sessione. Se Claude Code prende una decisione architetturale, elimina un componente, o scopre un comportamento non ovvio, lo scrive subito nel brain locale prima di procedere.

Tre tipi di OPL (come in P&G):
1. **Basic Knowledge**: come funziona un componente (es. "come i segnali viaggiano da Sportmonks a Redis a DB a Betfair")
2. **Problem Case**: cosa è andato storto e perché (es. "threshold hardcoded causavano data leak nel training")
3. **Improvement Case**: cosa è stato migliorato e come (es. "introdotta auto-ottimizzazione con Optuna al posto dei threshold fissi")

### Livello 2 — CBA (Current Best Approach) → nota di processo end-to-end

Per ogni flusso critico del sistema, una nota di processo nel brain locale che:

- Descrive il **processo end-to-end** in termini di comportamento del prodotto
- **Richiama le OPL** dei singoli componenti coinvolti (wikilink)
- Elenca le **prescrizioni**: cosa può andare storto, come verificare che il processo funzioni correttamente, come monitorare
- È la migliore pratica **nota ad oggi** — si aggiorna quando qualcuno (founder o Claude Code) trova un modo migliore

> [!tip] Relazione OPL ↔ CBA
> Le OPL sono i mattoncini (singolo componente). Le CBA sono il processo intero che li assembla. Quando una OPL viene aggiornata (es. un componente cambia), la CBA che la richiama va verificata per coerenza.

### Livello 3 — Push pre-sessione (DMS adattato)

> [!danger] Regola di retrieval
> Claude Code **legge il brain locale all'inizio di ogni sessione di coding** — non aspetta che il founder gli dica dove guardare.

Il principio è **push-based**: l'informazione arriva a Claude Code prima che ne abbia bisogno, non quando ormai ha già implementato qualcosa di sbagliato.

#### Navigazione via wikilink (CBA-first)

Claude Code non legge tutto il brain locale — naviga il grafo partendo dal task:

1. **Identifica il flusso**: dal task corrente, individua quale flusso end-to-end è coinvolto
2. **Legge la CBA**: la CBA del flusso è il punto di ingresso — descrive il processo intero
3. **Segue i wikilink**: la CBA contiene `[[wikilink]]` alle OPL dei singoli componenti coinvolti. Claude Code segue solo i link rilevanti per il task, non tutti
4. **Espande se necessario**: se una OPL rimanda a decisioni o componenti collegati, segue il link solo se pertinente alla catena causale del task

È lo stesso pattern del vault globale con Basic Memory MCP: nota-seme → espansione per wikilink → stop quando il nodo non è più nella catena causale.

> [!tip] Le CBA come indice navigabile
> Le CBA sono gli indici dei flussi. Le OPL sono i nodi. I wikilink sono gli archi. Claude Code naviga il grafo — non scarica l'intero database.

**Domanda-test per Claude Code prima di implementare**: *"Ho letto la CBA del flusso su cui sto per lavorare e le OPL dei componenti coinvolti?"*. Se no, navigare prima di procedere.

## Struttura nel brain locale

```
<repo>/.brain/
  knowledge/
    opl/
      <Componente>-Basic-<Descrizione>.md
      <Componente>-Problem-<Descrizione>.md
      <Componente>-Improvement-<Descrizione>.md
    cba/
      <Processo-End-To-End>.md
```

### Scaffold automatico

La struttura `<repo>/.brain/knowledge/opl/` e `<repo>/.brain/knowledge/cba/` viene creata automaticamente all'inizializzazione di un nuovo progetto (via `project-initializer`). Se Claude Code apre un progetto e la directory `.brain/knowledge/` non esiste, la crea prima di procedere con qualsiasi implementazione (fallback).

Contenuto dello scaffold iniziale:
- `opl/README.md` — "One Point Lesson — note atomiche per componente. Tre tipi: Basic Knowledge, Problem Case, Improvement Case. Naming: `<Componente>-Basic-<Descrizione>.md`, `<Componente>-Problem-<Descrizione>.md`, `<Componente>-Improvement-<Descrizione>.md`."
- `cba/README.md` — "Current Best Approach — processi end-to-end con wikilink alle OPL. Naming: `<Processo-End-To-End>.md`."

### Promozione a vault globale (via `/sprint`)

La conoscenza catturata nel `.brain/` è **locale al progetto**. Quando ha valore cross-progetto o impatto architetturale significativo, viene **promossa nel vault globale** dalla skill `/sprint`:

| Brain locale (`.brain/`) | → | Vault globale (`20-Iniziative/`) |
|---|---|---|
| OPL Basic Knowledge | → | nota `tipo: architettura` |
| OPL Problem Case | → | nota `tipo: problema-risolto` |
| OPL Improvement Case | → | nota `tipo: architettura` o `tipo: problema-risolto` |
| Trade-off (da [[Processo-Cost-Deployment]]) | → | nota `tipo: debito-tecnico` |

La promozione è **semantica, non automatica**: si promuove ciò che è trasferibile oltre il singolo progetto. La regola di filing completa è in [[Strumenti-Filing-Brain-Globale-Locale]] (soglia ≥2 occorrenze per promozione autonoma).

La nota vault promossa indica la OPL sorgente nel brain locale con il path relativo al repo (riferimento testuale, non wikilink — il vault non può linkare fuori da sé).

## Ciclo di vita

1. **Cattura**: durante la sessione, Claude Code crea la OPL nel momento in cui la conoscenza emerge
2. **Aggregazione**: quando più OPL coprono un flusso end-to-end, Claude Code propone la creazione di una CBA
3. **Push**: all'inizio di ogni sessione, Claude Code naviga il grafo CBA → OPL via wikilink (vedi [[#Navigazione via wikilink (CBA-first)]])
4. **Aggiornamento**: quando un componente cambia, la OPL si aggiorna e le CBA che la richiamano vengono verificate
5. **Promozione**: se una conoscenza vale oltre il singolo progetto, viene promossa nel vault globale via `/sprint` — vedi [[Strumenti-Filing-Brain-Globale-Locale]] per la soglia ≥2 occorrenze e la sezione [[#Promozione a vault globale (via `/sprint`)]] sopra

## Anti-pattern da evitare

- **"Lo scrivo a fine sessione"** — a fine sessione hai dimenticato i dettagli. Cattura subito.
- **"Claude Code dovrebbe ricordarselo"** — Claude Code non ha memoria tra sessioni. Se non è scritto, non esiste.
- **"Il codice è la documentazione"** — il codice dice *cosa* fa, non *perché* è stato fatto così e non in un altro modo. Le decisioni vivono nelle OPL.
- **"Cerco nel brain quando mi serve"** — il retrieval è push-based. Se devi cercarlo, il sistema ha fallito.

## Collegamenti

- [[Procter-And-Gamble]] — origine: OPL, CBA, DMS push-based di IWS
- [[Processo-Quality-Pillar-Coding]] — loss map (perdite #10 e #11)
- [[Troubleshooting-UPS-Coding]] — framework complementare per runtime failures
- [[Strumenti-Filing-Brain-Globale-Locale]] — regola di promozione brain locale → vault globale
- [[Dashboard]]
