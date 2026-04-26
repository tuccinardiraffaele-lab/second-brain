---
tipo: processo
creato: 2026-04-20
aggiornato: 2026-04-20
stato: attivo
tags:
  - processo/pillar
  - operazioni/vault
area: operazioni
---

# Processo — Definizione obiettivi di fase pillar

> [!info] In una frase
> Metodo riutilizzabile per definire, per ciascun pillar strategico, gli obiettivi di fase (Foundation → Stability → Predictability → Agility), gli Health check oggettivi e i target zero-loss, usando Backcasting + SMART + Goodhart + Challenge layer, in **due sessioni di brainstorm separate**.

## Quando applicarlo

Al momento in cui un pillar strategico viene consolidato nel vault — quando si passa dallo scaffold iniziale alla definizione completa. Applicabile a tutti i 7 pillar della [[Pillar-Doppio-Livello|tassonomia strategica]].

Il processo presuppone:
- Pillar già creato come nota in `30-Dominio/<sottodominio>/`
- Loss proprietaria definita
- Contesto del dominio conosciuto dal founder

## Step 0 — Recupero knowledge base (pre-condizione bloccante)

> [!warning] Pre-condizione obbligatoria
> Prima di iniziare qualunque brainstorm sui pillar, **recuperare la knowledge base rilevante con criterio di sufficienza esplicito**. "Ho fatto `ls` della cartella" non è recupero. Senza lettura effettiva, il brainstorm lavora su premesse implicite e produce metriche non ancorate al contesto del progetto.

### 0.a — Input obbligatori sempre in contesto attivo

Leggere se non già in contesto della sessione corrente:

- Nota pillar target (quella da aggiornare)
- [[Procter-And-Gamble]] — origine del framework IWS
- [[Pillar-Doppio-Livello]] — distinzione pillar-fase vs progetto-stato, scala 0-3
- [[Zero-Loss-Mindset]] — principio che giustifica i target zero-loss
- [[Framework-Codificato-Per-Loss]] — gerarchia strumenti e MECE "un record vivo"

### 0.b — Input obbligatori se il pillar si aggancia a un progetto

Mapping pillar → progetti da cui recuperare KB:

| Pillar | KB progetto obbligatoria |
|--------|--------------------------|
| Leadership strategica | — (cross-progetto) |
| Governance reputazionale | AIOS (B2B vincolo) |
| Studio giuridico | AIOS (aggancio Agility → B2B) |
| Network target | — |
| Sales & Positioning | AIOS + FT (piloti da vendere) |
| Monitoraggio regolatorio | AIOS (impatto regolatorio sul B2C) |
| Delivery piloti | AIOS + FT (piloti oggetto) |

Per ogni progetto nel mapping, leggere effettivamente:

- **MOC progetto** (es. [[Sistema-Agentico-Studio]], [[Football-Trading]])
- **Note di intervista stakeholder principali** (es. [[AIOS-Intervista-Padre-Domande-KB]], [[AIOS-Intervista-Padre-Follow-Up]], [[AIOS-Intervista-Esperto-GBSoftware]])
- **Decisioni chiave** del progetto (es. [[Decisione-Soglie-Pilot-AIOS]])
- Note rilevanti al pillar specifico (es. per pillar Sales & Positioning su FT → stato pipeline retail)

Non leggere tutto — leggi ciò che è necessario per soddisfare il criterio 0.c.

### 0.c — Criterio di sufficienza (test bloccante)

Prima di procedere con Sessione 1, verifica di saper rispondere a tutti e tre questi test:

1. **So rispondere** (senza inferenze) a: *"Qual è il problema che questo pillar risolve nel contesto del progetto X?"*
2. **So nominare 2-3 vincoli concreti** del progetto che impattano le metriche del pillar (es. ciclo di vendita, dipendenze tecniche, stakeholder, tempi regolatori)
3. **So citare la data di ultimo aggiornamento** delle note chiave lette; se > 60 giorni, segnalarlo al founder prima di procedere (KB potrebbe essere stantia)

Se anche uno dei tre test non passa → Step 0 incompleto, riprendi lettura targeted.

### Anti-pattern osservato 2026-04-20

Nel brainstorm pillar Studio giuridico (Sessione 2 Health check), lo Step 0 è stato dichiarato completato dopo un semplice `ls` della cartella `Sistema-Agentico-Studio/` senza lettura di alcuna nota. Risultato: la soglia "≥ 2 studi B2B AIOS" nel Health check Agility è stata scelta come ordine di grandezza ragionevole ma **non ancorata a evidenza** sul pipeline AIOS reale. Rischio: quando si entrerà in fase Predictability/Agility (2029-2030), il numero potrebbe rivelarsi irrealistico (troppo alto o troppo basso). Questo anti-pattern ha generato la riscrittura di Step 0 in 0.a + 0.b + 0.c.

## Principi vincolanti

- **Obiettivo ≠ strumento**: l'obiettivo di fase è stato/risultato finale, non routine/attività (quella è percorso interno)
- **Le fasi sono durate**, non istanti: hanno inizio, percorso interno, fine
- **Niente invenzioni fuori dominio**: se un elemento (piano esami, soglia Ordine) è dato da un'istituzione esterna, non va creato come artefatto del pillar
- **Verificabilità esterna**: ogni end-state e Health check deve essere giudicabile da un osservatore terzo senza chiedere al founder come si sente
- **Il founder dà le soglie numeriche**: non inferire metriche, elicitare dal founder con domande-specchio
- **Il target zero-loss è derivato**, non inventato: nasce dalla negazione del Health check ("numero di eventi che violano = 0 per finestra X")

## Flusso in 2 sessioni di brainstorm separate

La definizione del pillar richiede **due brainstorm distinti**. Tentare di farli in uno solo porta a inferenze non rigorose (errore osservato il 2026-04-20 sul pilota Studio giuridico).

### Sessione 1 — End-state (obiettivi di fase)

Output: 4 end-state narrativi (uno per fase).

#### Step 1.1 — Cynefin quick check

- Complicated → framework noto (IWS) + analisi → procedi
- Complex → probing con piccoli esperimenti → procedi con cautela
- Clear → esci (no brainstorm)
- Chaotic → esci (no brainstorm)

Atteso per i pillar del sistema: tutti **Complicated con zone Complex**.

#### Step 1.2 — Elicitazione end-state Agility (Working Backwards)

Tre domande-specchio in forma aperta, **mai elencare strutture**:

1. *"Chi sei / cos'è il sistema quando questo pillar è in Agility?"* — identità, ruolo, posizionamento
2. *"Cosa fai diverso rispetto a oggi, nel quotidiano?"* — capacità adattiva, situazioni affrontate
3. *"Qual è il segnale esterno che conferma di essere in Agility?"* — fatto osservabile, non sensazione

Normalizza in 3-4 elementi distinti. Separa asset già posseduti (non obiettivo del pillar) da end-state target.

#### Step 1.3 — Backward chain (Robinson 1990)

Dal Agility end-state, per ogni fase a ritroso:

> *"Per essere [fase successiva], cosa doveva essere vero un passo prima?"*

Pensa in termini di **stato**, non di attività. Proponi 2-3 ipotesi-spunto per orientare, senza imporre. Lascia opzione C ("altro").

**Attenzione ai tagli ambigui**: l'end-state Agility può contenere stati distinti che appartengono a fasi diverse (ingresso ruolo ≠ pienamente adattivo → Predictability vs Agility). Verificare il taglio con il founder.

**Fase = durata**: chiarire se una risposta è l'ingresso, il percorso interno, o l'end-state di quella fase.

#### Step 1.4 — Challenge sessione 1

- **Pre-mortem**: "3 anni dopo Agility non raggiunta, 3 cause più probabili?"
- **WRAP widen**: "End-state alternativi che vanno considerati?"
- **Reality-test**: "Ogni end-state è verificabile da un osservatore esterno?"

### Sessione 2 — Health check + target zero-loss

Output: Health check SMART + target zero-loss per ciascuna fase.

**Pre-condizione**: Sessione 1 completata e scritta. Gli end-state sono input della sessione 2.

#### Framework combinato

- **SMART** (Doran 1981): Specific, Measurable, Achievable, Relevant, Time-bound
- **Leading/Lagging indicators** (Kaplan & Norton 1992): ogni fase ha almeno uno di ciascun tipo dove sensato
- **Goodhart's Law test** (Strathern 1997): per ogni target zero-loss, identifica rischio gaming e mitigazione

#### Flusso per ciascuna fase

1. **Ricordo end-state** dalla sessione 1
2. **Domanda-specchio** multi-osservatore: *"Un terzo (dominus, cliente, Ordine, peer) che vuole verificare senza chiederti come ti senti che sei in [fase], cosa dovrebbe vedere?"*
3. **Elicitazione misure**: chiedi al founder i fatti osservabili + le soglie numeriche. **Non inferire mai i numeri**. Se serve, proponi candidate ("≥ X pratiche/mese o ≥ Y% copertura") ma lascia scegliere al founder.
4. **Time-bound**: chiedi la finestra temporale di raggiungimento e, se applicabile, la finestra temporale di valutazione (mensile? annuale?).
5. **Test SMART** su ogni Health check: se uno dei 5 criteri non è soddisfatto, raffinare.
6. **Test Goodhart**: per ogni Health check, identifica rischio gaming e mitigazione. Se il gaming non è mitigabile, riconsiderare la misura.
7. **Classificazione Leading/Lagging**: verifica che la fase abbia entrambi dove sensato.
8. **Derivazione target zero-loss**: negazione del Health check ("mesi/anni con [metrica] sotto soglia = 0"). Non inventare nuove metriche.

#### Challenge sessione 2

- **Pre-mortem complessivo sul chain**: gate critico unico o altri gate emergono con le metriche scelte?
- **WRAP widen**: le dimensioni dell'end-state Agility sono esaustive? Se sì, lock-in per ora; revisione JIT quando si entra nella fase.
- **Reality-test finale**: tutti gli Health check + target verificabili da terzi?

## Output attesi per ciascun pillar

Per sessione 1 + sessione 2 combinate:

1. **Nota pillar aggiornata** in `30-Dominio/<sottodominio>/<...-Pillar-...>.md` con:
   - Obiettivi di fase (4 end-state)
   - Health check osservabili con SMART-time-bound
   - Target zero-loss derivati
   - Stato corrente
   - Aggancio cross-pillar esplicito
   - Input mancanti come placeholder
2. **Nota brainstorm sorgente** in `30-Dominio/<sottodominio>/Brainstorm-Obiettivi-Fase-<SlugPillar>.md` con entrambe le sessioni documentate (cynefin, framework, chain, challenge, ipotesi di gaming)
3. Aggiornamento wikilink tra nota pillar e nota brainstorm

## Anti-pattern proibiti (osservati e da evitare)

- **Chiedere al founder di elencare strutture**: *"dimmi i 4 obiettivi delle 4 fasi"* è una domanda pigra. Se lui li sa già, il brainstorm è inutile. Usa framework.
- **Scambiare strumento per obiettivo**: routine quotidiana non è obiettivo Foundation; è percorso interno.
- **Inventare artefatti esterni**: piano esami dato dall'università, soglia Ordine data dall'Ordine. Non li creare.
- **Saltare Sessione 2 (Health check)**: finire a Sessione 1 lascia end-state narrativi ma non misurabili. Il pillar diventa burocrazia.
- **Inferire metriche/numeri al posto del founder**: genera target arbitrari che il founder "conferma" per cortesia. Errore commesso il 2026-04-20, corretto con Sessione 2 separata.
- **Saltare Step 0 (KB recovery)**: il brainstorm lavora su premesse errate.
- **Lasciare end-state vaghi**: se il reality-test dice "potenzialmente vago", raffinare prima di chiudere.

## Applicazione al corpus pillar

| Pillar | Sessione 1 (end-state) | Sessione 2 (Health check + zero-loss) |
|--------|------------------------|---------------------------------------|
| [[Crescita-Pillar-Studio-Giuridico]] | ✓ 2026-04-20 | ✓ 2026-04-20 (pilota) |
| [[Strategia-Pillar-Leadership-Strategica]] | ✓ 2026-04-20 | ✓ 2026-04-20 |
| [[Vendite-Pillar-Governance-Reputazionale]] | ✓ 2026-04-20 | ✓ 2026-04-20 |
| [[Relazioni-Pillar-Network-Target]] | ✓ 2026-04-25 | ✓ 2026-04-25 |
| [[Vendite-Pillar-Sales-Positioning]] | ✓ 2026-04-25 | ✓ 2026-04-25 |
| [[Strategia-Pillar-Monitoraggio-Regolatorio]] | ✓ 2026-04-25 | ✓ 2026-04-25 |
| [[Prodotto-Pillar-Delivery-Piloti]] | ✓ 2026-04-20 | ✓ 2026-04-20 |

## Riferimenti metodologici

- Robinson, *Futures research and sustainability*, Futures 1990 (Backcasting)
- Snowden, *A Leader's Framework for Decision Making*, HBR 2007 (Cynefin)
- Doran, *There's a SMART way to write management's goals*, Management Review 1981 (SMART)
- Kaplan & Norton, *The Balanced Scorecard*, HBR 1992 (Leading/Lagging)
- Strathern, *Improving ratings: audit in the British University system*, European Review 1997 (Goodhart's Law test)
- Klein, *Performing a Project Premortem*, HBR 2007
- Heath & Heath, *Decisive*, 2013 (WRAP)

## Collegamenti

- [[Pillar-Doppio-Livello]] — tassonomia dei pillar
- [[Zero-Loss-Mindset]] — principio che giustifica i target zero-loss
- [[Framework-Codificato-Per-Loss]] — Health check come strumento misurabile
- [[Processo-Review-Cadence]] — meccanismo di avanzamento fase via monthly
- [[Procter-And-Gamble]] — origine IWS
