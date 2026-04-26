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

# Framework codificato per tipo di loss

> [!info] In una frase
> Ogni classe di loss richiede un percorso specifico attraverso una gerarchia di strumenti dedicati (AM → UPS → Capex). La sequenza obbligatoria è **diagnosi → classificazione → scelta del livello di strumento**, mai viceversa. Senza questo vincolo metodologico, la loss sopravvive (troppo in basso) o l'investimento spreca risorse (troppo in alto).

## Il principio in P&G IWS

In P&G ogni pillar possiede una classe di loss (vedi [[Pillar-Doppio-Livello]]) e ciascun livello di maturità ha il suo strumento dedicato:

| Livello | Strumento | Costo | Quando |
|---------|-----------|-------|--------|
| 1 | **AM (Autonomous Maintenance)** | Quasi zero, immediato, vicino all'operatore | Loss superficiali, basic conditions non rispettate |
| 2 | **UPS (Unified Problem Solving)** | Tempo diagnostico strutturato, zero capex | Loss con causa ricorrente non ovvia |
| 3 | **Modifica / Capex** | Tempo lungo + investimento grande | Loss strutturali/sistemiche |

Il rationale è MECE per natura della loss, non per "potenza" dello strumento. Lo strumento giusto è quello **proporzionato alla classe di loss**, non il più potente disponibile.

## Due errori speculari

**Errore 1 — Saltare troppo in alto**: capex per una loss AM-trattabile. L'investimento risolve, ma consuma risorse sproporzionate e **non costruisce capability** (il team non impara AM, non impara UPS). La prossima loss simile ricade nello stesso pattern.

**Errore 2 — Fermarsi troppo in basso**: quick-fix ripetuti senza risalire alla causa base. La loss **ritorna in variante dello stesso failure mode**. Esempio concreto: un macchinario che non chiude gli astucci può essere settato via AM per riprendere produzione; ma senza UPS, alla produzione successiva il failure mode si ripresenta (astucci chiusi nel verso sbagliato invece di non chiusi). Senza chiudere la causa base, la loss è solo *deviata*.

**Radice comune**: entrambi gli errori nascono da **classificazione saltata o incompleta**. La regola meta non è "scegli lo strumento" — è "classifica la loss e attraversa tutti i livelli che la sua natura richiede".

## Misurabilità e dataset — la pre-condizione del principio

Senza misurabilità, la distinzione fra occorrenza isolata (livello 1) e pattern ricorrente (livello 2) è impossibile. Serve un **dataset delle occorrenze** con:

- **Naming convention standardizzata** (date + slug)
- **Frontmatter strutturato** minimo: `tipo: loss`, `pillar`, `livello`, `stato`, `failure-mode`
- **Query deterministica alla chiusura di ogni livello 1**: "esistono occorrenze simili già registrate? Quante? In quale arco temporale?"

Se la risposta mostra ricorrenza → escalation a livello 2 (UPS) obbligata. Se UPS rivela causa strutturale → livello 3 (capex).

## Architettura a 3 livelli del dataset

Il dataset vive su tre territori distinti, con fisionomia diversa e promozione esplicita tra di essi.

| Livello | Dove | Tipo di loss | Popolato da |
|---------|------|--------------|-------------|
| **1. Brain locale** | `<repo>/.brain/debug/` + `<repo>/.brain/autonomous-maintenance/defects/` | Loss coding (alta frequenza, basso peso singolo) | UPS + Quality Pillar durante sessioni coding |
| **2. Vault progettuale** | `20-Iniziative/🔥-Attive/<Progetto>/losses/` | Loss coding promosse con valore riusabile | Skill `/sprint` a fine sessione coding |
| **3. Vault globale** | `30-Dominio/<sottodominio>/losses/` (sotto il pillar proprietario) | Loss strategiche cross-progetto | Skill `/sprint` (detection auto) + `/monthly` (backstop) |

**Regola di promozione 1 → 2**: solo loss chiuse con causa base documentata e valore cross-sessione. Scarta fix banali, falsi positivi senza lezione, ticket senza classificazione finale.

**Regola di promozione 2 → 3**: (a) stessa classe di loss in ≥2 progetti distinti, oppure (b) loss singola con impatto trasversale dichiarato (es. finestra competitiva → sempre globale).

## Regola MECE: un solo record vivo per evento

Con due framework concorrenti (UPS scrive in `.brain/debug/`, Quality Pillar scrive in `.brain/autonomous-maintenance/defects/`), il rischio è **doppia tracciatura** dello stesso evento. Regola vincolante codificata nelle skill `troubleshooting-ups` e `quality-pillar`:

**Un evento di loss coding ha un solo record ufficiale vivo alla volta.**

- **Runtime-first** (fenomeno osservato, nessun AC di riferimento): nasce in `debug/`. Alla chiusura → classificazione A/B/C. Se A → ticket debug diventa storico (`promosso-a-defect`), defect diventa record vivo.
- **Gate-first** (AC violato al Gate 3): nasce direttamente in `defects/`. UPS si esegue **dentro** il file defect come sezione `## Diagnosi UPS`, NON come ticket separato.

## Classificazione di chiusura A/B/C (obbligatoria per i ticket debug)

Ogni ticket debug, alla chiusura, deve ricadere in UNA di queste classi. Se non classificabile → non chiudibile, serve più evidenza.

| Classe | Significato | Artefatto prodotto |
|--------|-------------|--------------------|
| **A — Violazione AC esistente** | Il fenomeno rompe un AC già dichiarato | Promozione a defect (+ fix) |
| **B — Gap di AC** | Comportamento atteso non era mai stato dichiarato | Crea AC nuovo; se violato, promozione a defect |
| **C — Falso positivo** | Il comportamento era corretto, l'aspettativa era sbagliata | Archivia con nota esplicita del perché |

**Effetto sul prodotto**: nessun ticket diventa orfano. Ogni chiusura lascia un artefatto tracciabile (defect, AC nuovo, o lezione esplicita sul comportamento corretto).

## La triade chiusa dei principi meta P&G

Questo principio chiude la triade con [[Pillar-Doppio-Livello]] e [[Zero-Loss-Mindset]]. I tre stanno insieme:

- **Pillar a doppio livello** — *chi* presidia (tassonomia MECE di proprietà)
- **Zero-loss mindset** — *perché* si agisce (rifiuto ontologico + risorse scalabili)
- **Framework codificato per tipo di loss** — *come* si agisce (gerarchia strumenti + misurabilità + un solo record vivo)

Senza uno dei tre, gli altri due non tengono:
- Senza pillar → zero-loss diventa sentimento, framework diventa improvvisazione
- Senza zero-loss → pillar diventano burocrazia, framework diventa teatro
- Senza framework → pillar mappano proprietà senza sapere cosa fare, zero-loss ha energia senza strumento

## Applicazione al mio sistema strategico

### Livello 1 — Brain locale (coding)
Già implementato: UPS produce `.brain/debug/`, Quality Pillar produce `.brain/autonomous-maintenance/defects/`. Le skill aggiornate (`troubleshooting-ups` + `quality-pillar`) forzano la regola "un solo record vivo" + classificazione A/B/C alla chiusura.

### Livello 2 — Vault progettuale
La skill `/sprint` (ora globale, disponibile da qualunque repo) legge le loss chiuse dal brain locale, filtra per valore cross-sessione, e promuove a `20-Iniziative/🔥-Attive/<Progetto>/losses/`.

### Livello 3 — Vault globale
Due meccanismi complementari:
- **Deterministico in `/sprint`**: prima di scrivere una loss progettuale nuova, query cross-progetto per `failure-mode` simile. Se trovata in progetto diverso → propone promozione a globale.
- **Backstop in `/monthly`**: scan mensile cross-progetto delle loss promosse nel mese, per catturare pattern semantici non visti dal match sintattico.

## Collegamenti

- [[Procter-And-Gamble]] — origine dei framework
- [[Pillar-Doppio-Livello]] — scheletro della tassonomia
- [[Zero-Loss-Mindset]] — energia + infrastruttura
- [[Troubleshooting-UPS-Coding]] — livello 2 applicato al coding
- [[Processo-Quality-Pillar-Coding]] — regola MECE + Gate 3 + defect register
- [[Processo-Knowledge-Management-Coding]] — cattura nel brain locale
- [[Processo-Cost-Deployment]] — monetizzazione per capex (livello 3)
- [[Processo-Review-Cadence]] — weekly (capture) / monthly (promozione cross-progetto) / trimestrale (roadmap pillar)
- [[Dashboard]]
