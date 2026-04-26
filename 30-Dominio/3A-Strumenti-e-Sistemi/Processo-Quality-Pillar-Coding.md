---
tipo: processo
creato: 2026-04-17
aggiornato: 2026-04-20
stato: attivo
tags:
  - processo/quality
  - strumenti/claude-code
  - metodo/iws
area: strumenti
---

# Quality Pillar — Coding

> [!info] In una frase
> Adattamento al coding del **Quality Pillar** di [[Procter-And-Gamble|P&G IWS]]: un sistema a gate che elimina il gap tra ciò che viene costruito e ciò che serviva, verificando la **conformità del prodotto ai requirement** — non la correttezza del codice.

## Origine

Derivato dal Quality Pillar e dall'Autonomous Maintenance del framework **IWS (Integrated Work System)** di [[Procter-And-Gamble]]. In IWS il Quality Pillar persegue **zero quality defects** lungo tutta la supply chain; l'AM traccia i difetti sulla macchina con tag, severità e ciclo open→closed. Qui la "macchina" è il codebase, l'"operatore" è il founder (o Claude), il "prodotto conforme" è il software che si comporta come descritto nei requirement.

## Problema che risolve

Copre tre tipi di perdita identificati nella [[#Loss map]]:

| # | Perdita | Sintomo |
|---|---------|---------|
| 7 | **Code correctness vs outcome correctness** | I test passano, il prodotto non fa ciò che serve |
| 6 | **Feature gap non dichiarato** | Il prodotto funziona all'80% ma nessuno dichiara il 20% mancante |
| 3 | **Wrong target** | Si costruisce la cosa sbagliata per requisito ambiguo |

### La catena di failure che produce queste perdite

1. Il founder descrive un comportamento desiderato con esempi concreti
2. Claude traduce in piano tecnico → il founder non può validarlo (linguaggio sbagliato)
3. Claude implementa → verifica solo code correctness (test passano)
4. Gli esempi originali non vengono mai riusati come acceptance criteria
5. Il gap emerge solo in produzione/utilizzo reale → massimo costo di rework

## Il flusso a gate

### Gate 0 — Assunzioni tecniche (impatto sul prodotto)

> [!danger] Regola
> Ogni scelta tecnica che introduce un'assunzione (dati approssimati, valori hardcoded, proxy invece di misure dirette, dipendenze non aggiornate) viene **tradotta in impatto sul comportamento del prodotto** e presentata al founder prima di procedere.

Claude non presenta l'assunzione in linguaggio tecnico ("i threshold sono hardcoded"). La riformula in conseguenza osservabile: *"il sistema potrà barare sui dati storici perché conosce già i risultati"*.

**Domanda-test per Claude**: *"Questa scelta tecnica potrebbe produrre un comportamento del prodotto diverso da quello che il founder si aspetta, oggi o quando le condizioni cambiano?"*. Se sì, dichiararlo prima di implementare.

Questo gate copre la perdita #5 (debito tecnico che esplode) — vedi [[#Loss map]].

### Gate 0b — Ricognizione pre-integrazione

> [!danger] Regola
> Prima di integrare un componente esterno (API, servizio, ambiente di deploy), Claude **cerca referenze esterne** di chi ha già risolto lo stesso problema di integrazione e **documenta il contesto ambientale** nel brain locale del progetto.

Due azioni obbligatorie:
1. **Ricerca referenze**: cercare implementazioni esistenti dello stesso tipo di integrazione (es. altri progetti che usano le API Betfair, altri deploy su VPS con lo stesso stack). Estrarre i problemi noti e le soluzioni adottate.
2. **Documentazione contesto ambientale**: scrivere nel brain locale dove vivono le configurazioni dell'ambiente target (variabili d'ambiente, path, servizi attivi) per evitare di ripartire da zero ad ogni sessione.

**Domanda-test per Claude**: *"Se qualcuno dovesse rifare questa integrazione tra 3 mesi, troverebbe tutto il contesto necessario nel brain locale?"*. Se no, documentare prima di procedere.

Questo gate copre la perdita #4 (integration failure) — vedi [[#Loss map]].

### Gate 1 — Piano in linguaggio prodotto

> [!danger] Regola
> Claude **non** presenta il piano in termini di codice. Lo riformula in termini di **comportamento osservabile del prodotto**: *"il prodotto passerà dal comportamento A al comportamento B"*.

Il founder valida il piano sul piano funzionale. Se non riesce a validare → il piano è nel linguaggio sbagliato, Claude riformula.

**Domanda-test per Claude prima di procedere**: *"Il founder, senza competenze di coding, può giudicare se questo piano produrrà il risultato che vuole?"*. Se la risposta è no, riformulare.

> [!warning] Si applica a OGNI piano, non solo ai piani di implementazione
> Gate 1 e Gate 2 si attivano anche quando il piano è di **verifica/osservazione runtime**, di **quality gate pre-match**, di **dry-run** o di **diagnosi strutturata**. Un piano che dichiara "non-goal: modificare codice" non è read-only ai fini di questa skill: è scrittura di un artefatto che definisce il comportamento atteso del prodotto, e va in linguaggio prodotto per costruzione. Vale per piani inline in chat, per plan mode di Claude Code (output in `~/.claude/plans/`) e per piani salvati in `<repo>/.brain/planning/`.

### Gate 2 — Acceptance criteria

Gli esempi forniti dal founder (link, screenshot, descrizioni di comportamento) diventano **acceptance criteria (AC)** espliciti, numerati, verificabili.

Regole:
- Ogni AC descrive un **comportamento osservabile del prodotto**, non un fatto tecnico
- Formato: `AC-01: <soggetto> <azione> <risultato atteso>`
- Se un esempio non è traducibile in AC verificabile → chiarire **prima** di scrivere codice
- Gli AC vengono presentati al founder per validazione prima dell'implementazione

> [!example] Esempio
> Esempio del founder: *"Quando arriva un segnale, voglio ricevere una notifica Telegram con il nome della partita e la quota"*
>
> AC derivati:
> - `AC-01: Il bot Telegram invia un messaggio entro 1 minuto dalla generazione del segnale`
> - `AC-02: Il messaggio contiene nome della partita (Home vs Away) e quota numerica`
> - `AC-03: Se il segnale arriva a mercato chiuso, il messaggio lo indica esplicitamente`

### Implementazione

Fase di coding. Nessun gate qui — Claude implementa liberamente.

### Gate 3 — Verifica outcome vs acceptance criteria

> [!danger] Regola
> La verifica è sul **comportamento del prodotto**, non sui test del codice. "I test passano" non è sufficiente.

Per ogni AC, Claude verifica:
- **Pass**: il prodotto si comporta come descritto nell'AC (con evidenza: screenshot, log di output, comportamento osservato)
- **Fail**: il prodotto non si comporta come descritto → il delta viene registrato come **difetto**
- **Non verificabile**: Claude non ha accesso per verificare (es. no browser) → lo dichiara esplicitamente, **non** dichiara "fatto"

I difetti trovati vengono registrati nel defect register del progetto.

### Ciclo Continuous Improvement

> [!warning] Non è disclosure, è iterazione
> Il feature gap non viene dichiarato e basta — è un **trigger di iterazione**. Il ciclo non si chiude finché la similarità non raggiunge ≥99%.

Flusso:
1. Calcolare la similarità corrente (vedi [[#Calcolo similarità]])
2. Se <99% → identificare il delta, iterare
3. Per ogni difetto: Claude propone la severità, il founder valida
4. Risolvere, ri-verificare al Gate 3
5. Il difetto si chiude **solo** quando il Gate 3 conferma conformità all'AC di riferimento
6. **Done = ≥99% similarità**

## Calcolo similarità

```
Similarità = (AC soddisfatti / AC totali × 100) − Σ penalità difetti
```

- Ogni AC ha peso uguale di default (sovrascrivibile se un criterio è più critico)
- Ogni difetto ha una severità che si traduce in penalità:

| Severità | Penalità | Descrizione |
|----------|----------|-------------|
| **Critico** | −10% | Il prodotto non fa ciò che dovrebbe in un flusso primario |
| **Maggiore** | −5% | Il prodotto lo fa ma in modo scorretto/incompleto su un flusso secondario |
| **Minore** | −1% | Imperfezione marginale (UI, wording, edge case raro) |

> [!tip] Implicazione pratica
> Un difetto critico da solo porta sotto il 90% — impossibile dichiarare "fatto" senza risolverlo. Due difetti minori tolgono il 2% — risolvibili nell'iterazione CI.

## Defect register

### Struttura

```
<repo>/.brain/
  autonomous-maintenance/
    defects/
      open/
        <Progetto>-<Feature>-<Descrizione>-<YYYY-MM-DD>.md
      closed/
        <Progetto>-<Feature>-<Descrizione>-<YYYY-MM-DD>.md
```

### Template file difetto

```yaml
---
progetto: <sigla progetto>
feature: <nome feature>
severità: critico | maggiore | minore
penalità: 10% | 5% | 1%
stato: aperto | chiuso
data-apertura: YYYY-MM-DD
data-chiusura:
acceptance-criterion: "AC-XX: <testo dell'AC violato>"
---
```

Corpo:
- **Fenomeno osservato** — cosa succede (non perché)
- **Comportamento atteso** — dall'AC di riferimento
- **Delta** — differenza concreta tra osservato e atteso
- **Root cause** — compilato quando trovata (via [[Troubleshooting-UPS-Coding|UPS]] se serve)
- **Fix applicato** — compilato a chiusura

### Ciclo di vita del difetto

1. **Apertura**: Claude rileva il difetto al Gate 3, propone la severità
2. **Validazione**: il founder conferma o corregge la severità
3. **Risoluzione**: fix implementato
4. **Verifica**: Gate 3 ri-eseguito sull'AC di riferimento
5. **Chiusura**: solo se Gate 3 passa → file spostato in `closed/`

## Loss map

Mappa completa dei tipi di perdita identificati, con framework di attacco:

| # | Tipo di perdita | Dominio | Framework | Stato |
|---|----------------|---------|-----------|-------|
| 1 | Runtime failure (bug) | Coding | [[Troubleshooting-UPS-Coding\|UPS]] | Coperto |
| 2 | Rework | Coding | Prevenuto dai Gate 1-2 di questo processo | Coperto |
| 3 | Wrong target | Coding | Gate 1-2 di questo processo | Coperto |
| 4 | Integration failure | Coding | Gate 0b (ricognizione pre-integrazione) + brain locale per contesto ambientale | Coperto |
| 5 | Debito tecnico che esplode | Coding | Gate 0 (assunzioni tecniche tradotte in impatto prodotto) | Coperto |
| 6 | Feature gap non dichiarato | Coding | Gate 3 + ciclo CI di questo processo | Coperto |
| 7 | Code vs outcome correctness | Coding | Gate 3 di questo processo | Coperto |
| 8 | Decisione ritardata (costo trade-off) | Strategico | [[Processo-Cost-Deployment\|Cost Deployment]]: chiavi di conversione + registro trade-off con auto-correzione | Coperto |
| 9 | Focus disperso | Strategico | Guardrail OKR + [[Crescita-Priorità-Correnti\|Priorità]] | Coperto |
| 10 | Conoscenza non catturata | Strategico | [[Processo-Knowledge-Management-Coding\|Knowledge Management]]: OPL + CBA nel brain locale, cattura nel momento in cui emerge | Coperto |
| 11 | Conoscenza non trovabile | Strategico | [[Processo-Knowledge-Management-Coding\|Knowledge Management]]: retrieval push-based, Claude Code legge il brain locale prima di implementare | Coperto |
| 12 | Assenza di continuous improvement | Entrambi | Ciclo CI di questo processo (coding); [[Processo-Review-Cadence\|Review Cadence]] settimanale/mensile/trimestrale (strategico) | Coperto |

## Implementazione come Skill Claude Code

Dal 2026-04-17 questo processo vive anche come **skill globale** di Claude Code: `~/.claude/skills/quality-pillar/SKILL.md`. Attivazione automatica su ogni task che può impattare il comportamento del prodotto, **su ogni richiesta di scrivere un piano (implementazione, verifica, osservazione runtime, deploy, diagnosi) e ad ogni ingresso in plan mode**, più invocazione esplicita con `/quality-pillar`. Scope globale: disponibile in ogni progetto senza duplicazione. Pattern generale: vedi [[Decisione-Skill-vs-CLAUDE-md]].

## Come si applica a una sessione con Claude Code

> [!tip] Comportamento atteso di Claude Code
> 0. **All'ingresso in plan mode o alla richiesta di scrivere un piano**: il piano nasce già con Gate 1 (linguaggio prodotto) e Gate 2 (AC numerati) in testa, prima delle sezioni tecniche. Vale anche per piani di sola osservazione/verifica.
> 1. **Prima di tutto**: verificare se ci sono assunzioni tecniche da tradurre in impatto prodotto (Gate 0) e se serve ricognizione pre-integrazione (Gate 0b).
> 2. **Prima dell'implementazione**: presentare il piano in linguaggio prodotto (Gate 1), poi derivare AC dagli esempi del founder (Gate 2). Chiedere validazione su entrambi.
> 3. **Dopo l'implementazione**: verificare ogni AC contro il comportamento reale del prodotto (Gate 3), non limitarsi a "i test passano".
> 4. **Se similarità <99%**: registrare i difetti, proporre severità, iterare fino a convergenza.
> 5. **Mai dichiarare "fatto"** se la verifica outcome non è stata eseguita o non è possibile. In quel caso dichiarare esplicitamente cosa non è stato verificato.

## Anti-pattern da evitare

- **"I test passano, quindi funziona"** — code correctness ≠ outcome correctness
- **Piano in linguaggio tecnico** presentato al founder per validazione — se non può giudicarlo, il gate è inutile
- **Dichiarare "fatto" senza Gate 3** — il difetto emerge in produzione al massimo costo
- **Feature gap come disclosure** — "manca il 20%" senza iterare è una perdita accettata, non gestita
- **Difetto chiuso senza ri-verifica** — il fix non è validato finché il Gate 3 non passa

## Regola MECE: un solo record vivo per evento

Con due territori di tracciamento (UPS in `.brain/debug/`, Quality Pillar in `.brain/autonomous-maintenance/defects/`), la regola vincolante è: **un evento di loss coding ha un solo record ufficiale vivo alla volta**.

- **Runtime-first** (fenomeno osservato senza AC di riferimento): nasce in `debug/`. Alla chiusura va classificato A/B/C. Se A → ticket debug diventa storico, defect diventa record vivo.
- **Gate-first** (Gate 3 fallisce su AC): nasce direttamente in `defects/`. UPS si esegue **dentro** il file defect come sezione `## Diagnosi UPS`, non come ticket separato.

## Classificazione di chiusura A/B/C

Ogni ticket debug alla chiusura deve ricadere in UNA classe. Se non classificabile → non chiudibile.

| Classe | Significato | Artefatto prodotto |
|--------|-------------|--------------------|
| **A — Violazione AC esistente** | Rompe AC già dichiarato | Promozione a defect |
| **B — Gap di AC** | Requirement mai dichiarato | AC nuovo creato; se violato, defect |
| **C — Falso positivo** | Comportamento corretto frainteso | Archiviazione con nota esplicita |

Nessun ticket diventa orfano. Codificato in [[Framework-Codificato-Per-Loss]] e nelle skill `troubleshooting-ups` + `quality-pillar`.

## Collegamenti

- [[Procter-And-Gamble]] — origine: Quality Pillar e Autonomous Maintenance di IWS
- [[Troubleshooting-UPS-Coding]] — framework complementare per runtime failures (perdita #1)
- [[Decisione-Adozione-UPS-Coding]] — precedente di adozione P&G → coding
- [[Valori-Fondamentali#Efficacia]] — "colpire il bersaglio vero, attingendo alla fonte giusta"
- [[Valori-Fondamentali#Velocità]] — "velocità senza efficacia è rumore"
- [[Strumenti-Claude-Code]]
- [[Dashboard]]
