---
tipo: riflessione
creato: 2026-04-15
aggiornato: 2026-04-15
stato: attivo
tags:
  - brainstorm/progetto
  - brainstorm/sistema-agentico-studio
  - interview/preparazione
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
cynefin: complicated
framework: pr-faq
---

# Brainstorm — Knowledge Map per interview col padre (2026-04-17 sera)

> [!info] Scopo
> Derivare in modo strutturato **cosa chiedere a papà** venerdì 17 aprile sera per bootstrappare la knowledge base del vault AIOS ([[Sistema-Agentico-Studio]]), con scope ristretto al **MVP** (contabilizzazione fatture + integrazione GBSoftware) sui **10 clienti pilot**. Costruito via PR-FAQ Working Backwards, partendo dal comportamento atteso del sistema al go-live del **~10 maggio 2026** ([[KR1.3 — Go-live studio padre]]).

## Domanda di fondo

Quali conoscenze vanno catturate da papà affinché l'**AccountingAgent** di AIOS classifichi correttamente le fatture dei 10 clienti pilot e le registri in autonomia su GBSoftware, con il dipendente esperto coinvolto solo nei casi a bassa confidenza?

## Classificazione (Cynefin)

**Complicated** — esistono buone pratiche (il tuo stesso [[Processo-Costruzione-Vault-dedicato]] definisce il paradigma Interview + Retrofeedback; [[Prodotto-Vault-Substrato-Di-Prodotto]] fissa l'architettura a 3 strati). Non territorio nuovo, serve applicazione analitica.

## Press release (interna)

**Titolo**: AccountingAgent AIOS — contabilizzazione fatture automatica sui 10 clienti pilot.

**Sottotitolo**: dal 10 maggio 2026, le fatture dei 10 clienti pilot entrano in GBSoftware classificate dall'agente; l'esperto valida solo i casi a bassa confidenza.

**Cliente e problema**: il **dipendente esperto** dello studio di papà oggi riclassifica manualmente fatture in GBSoftware, in un processo di data-entry che replica scelte di classificazione già chiare nella sua testa. Il peso **non è sulla decisione** (la competenza è solida, gli errori rari) — è sul **lavoro meccanico** di inserimento. La classificazione è context-dependent sul cliente (stessa fattura può essere ricavo operativo o straordinario in base all'attività caratteristica del cliente), ma questa dipendenza è già gestibile via DB clienti strutturato, non va caricata nel vault.

**Soluzione e beneficio**: DocumentIntake (rule-based + LLM) classifica la fattura con livello di confidenza; se alto, AccountingAgent registra direttamente in GBSoftware sul cliente corretto; se basso, escalation in dashboard all'esperto prima della registrazione. Il dipendente non fa più data-entry sulle fatture chiare; il tempo risparmiato alimenta [[KR1.2 — Metriche pilot fissate con padre]].

**Perché ora**: [[Strategia-Attuale]] identifica [[Sistema-Agentico-Studio]] come bet strategico principale della transizione; la finestra competitiva (rischio endogeno di velocità) non aspetta; il pilot sullo studio del padre è il **terreno di validazione a basso rischio** prima del playbook replicabile.

## Customer FAQ (domande del dipendente esperto al sistema)

1. *"Su quale piano dei conti stai classificando? È quello che uso io nello studio o ne hai uno tuo standard?"*
2. *"Per il cliente X (real estate) la vendita di un immobile dove la metti? E per il cliente Y (supermercato)?"*
3. *"Se non sei sicuro, come me lo fai capire? Cosa devo guardare per decidere?"*
4. *"Ti fidi di un fornitore nuovo o mi chiami? Dopo che ho risposto una volta, ti ricordi per la prossima?"*
5. *"Quale regime contabile e forma giuridica stai applicando a questo cliente?"*
6. *"Cosa succede se sbaglio a validare? Come torno indietro?"*

## Internal FAQ (domande scomode del founder a sé stesso)

Tra le 5 candidate, le **3 più scomode** identificate:

1. **Copertura flusso B** — AIOS oggi gestisce le fatture che arrivano direttamente in GBSoftware via SDI/Agenzia Entrate senza passare dallo studio, o solo quelle caricate allo studio? Se no, che % del risparmio-tempo perdiamo al 10 maggio?
2. **Override non distruttivo** — quando l'esperto corregge una classificazione dell'agente, il retrofeedback aggiorna *solo* la regola per quel cliente o generalizza a tutti i clienti con attività simile? E se l'agente impara male? Manca un sistema di retraining automatico del threshold di confidenza (candidato: **Optuna** su feedback del commercialista) — **non implementato**, valutare se MVP o post-MVP.
3. **Misurabilità tempo risparmiato** — come misuriamo concretamente al 10 maggio? Self-report del dipendente, log di sistema, cronometro manuale? Senza un metodo fissato, [[KR2.1 — Paper trading debuggato|KR1.2]] resta vuoto.

## Assunzione forte da stressare con papà

> *"Per i 10 clienti pilot, il sistema popola il DB clienti automaticamente dai documenti."*

Parzialmente vera:
- **Forma giuridica**: derivabile (suffisso società, lookup P.IVA).
- **Attività caratteristica**: parzialmente derivabile (ATECO da P.IVA, ma spesso generico).
- **Regime contabile** (ordinario/semplificato/forfettario): **non** derivabile da una fattura singola — richiede fonte esterna (cassetto fiscale, scheda anagrafica cliente).

Conseguenza operativa: se non c'è un OnboardingAgent attivo al 10 maggio, *qualcuno* deve popolare il regime contabile per i 10 clienti — o papà una volta a priori, o l'esperto al primo escalation per cliente.

## Knowledge Map — domande per papà il 17 sera

Organizzate in **4 blocchi** di priorità decrescente. Blocco 1 e 2 sono **bloccanti** per il go-live; 3 e 4 possono entrare via retrofeedback successivo.

### Blocco 1 — Anagrafica e profilo dei 10 clienti pilot (PRIORITÀ MASSIMA)

- Quali sono i **10 clienti** del pilot (nome, P.IVA)?
- Per ciascuno:
  - Attività caratteristica (reale, non solo codice ATECO se ATECO è generico)
  - Regime contabile (ordinario / semplificato / forfettario)
  - Forma giuridica (ss, snc, sas, srl, spa, sapa, altro)
  - Quota stimata fatture via flusso A (caricate in studio) vs flusso B (arrivano via SDI in GBSoftware direttamente)
- Dove leggi oggi il regime contabile di questi clienti (cassetto fiscale, scheda interna dello studio, memoria)?

### Blocco 2 — Classificazione contabile: regole, piano dei conti, eccezioni

- Il **piano dei conti** che usi è quello standard CNDCEC o ne avete uno customizzato? Se customizzato, dove lo trovo?
- Le regole di classificazione **SP vs CE** e **operativo vs straordinario** dipendono dall'attività caratteristica del cliente — puoi darmi **2-3 esempi per ciascuno dei 10 clienti** dei casi tipici (fattura vendita, fattura acquisto, immobilizzazioni)?
- **Eccezioni ricorrenti**: fatture che apparentemente sembrano una cosa ma vanno classificate diversamente. Ne hai in mente 3-5 per i 10 clienti pilot?
- **Fornitori ricorrenti noti**: ci sono fornitori abituali con cui papà ha già una classificazione consolidata? (bootstrap del retrofeedback)

### Blocco 3 — Workflow esperto ↔ sistema

- Quando l'esperto riceve un'escalation dal sistema, **quanto tempo massimo** è accettabile per la sua risposta prima che diventi bottleneck?
- Come vuole **vedere la coda** delle escalation — tutte insieme a fine giornata, notifica in tempo reale, batch mattutino?
- Quando corregge una classificazione dell'agente, vuole che la correzione sia **salvata come regola** (es. "per il cliente X, fatture da fornitore Y vanno sempre in conto Z") o **singola tantum**?

### Blocco 4 — Metriche pilot (input per [[KR1.2 — Metriche pilot fissate con padre]])

- Quanti documenti/fatture in media passano dallo studio in una **settimana tipo** (non picco) — ordine di grandezza sui 10 clienti pilot?
- Quante ore/settimana il dipendente dedica oggi al data-entry in GBSoftware per questi 10 clienti?
- Su quella base: qual è una soglia di **tempo risparmiato/settimana** che al 30 giugno 2026 definisce "pilot riuscito"?
- Qual è una soglia di **accuratezza classificazione** (% senza override) sotto cui il pilot va considerato fallito?

## Pre-mortem — cause di fallimento al 30 giugno 2026

(Già emerse dalle Internal FAQ; le ricapitolo come rischi del pilot, non come nuove domande.)

- **Flusso B non coperto** → il risparmio-tempo per il dipendente è parziale, papà non vede beneficio pieno, il pilot non convince come blueprint per il secondo studio.
- **Qualità del DB clienti** insufficiente al 10 maggio → escalation su quasi tutte le fatture → esperto sovraccarico → effetto inverso (più lavoro di prima).
- **Retraining threshold non automatizzato** → la classificazione rimane rigida, l'accuratezza non migliora con l'uso, metrica #1 di [[KR1.2 — Metriche pilot fissate con padre]] stagna.

## Alternative e reality-test

- **Alternative considerate al PR-FAQ**: si poteva ridurre ulteriormente lo scope del pilot a **1-3 clienti** invece di 10, ma il founder ha già scelto 10 come scala minima per misurare pattern → alternativa scartata.
- **Cosa cambierebbe idea sul go-live del 10 maggio**: se al 2026-04-27 emerge che la Phase 10 GBSoftware non copre il flusso B e l'implementazione richiede >2 settimane, il go-live va posticipato o il perimetro ridotto ai soli clienti con prevalenza flusso A.

## Prossimi passi

- [ ] **2026-04-17 sera** — condurre l'interview col padre usando questa knowledge map, un blocco alla volta, documentando le risposte nella nota interview dedicata.
- [ ] **2026-04-27 entro** — fissare soglie metriche pilot con papà ([[KR1.2 — Metriche pilot fissate con padre]]) — in parte coperto dal Blocco 4 se l'interview del 17 le affronta.
- [ ] **Prossimo sprint coding AIOS** — verifica i 3 gap repo aggiunti in [[AIOS-Verifica-Roadmap-Agenti]] (flusso B, struttura DB clienti, retraining Optuna).

## Note collegate

- [[Sistema-Agentico-Studio]] — MOC prodotto, architettura a 3 strati
- [[Prodotto-Vault-Substrato-Di-Prodotto]] — il *cosa*: vault come parte del prodotto
- [[Processo-Costruzione-Vault-dedicato]] — il *come*: Interview + Retrofeedback
- [[Studio-Del-Padre-Piattaforma]] — cliente zero, piattaforma di transizione
- [[AIOS-Chiarire-Metriche-Pilot]] — azione aperta soglie KR1.2
- [[AIOS-Verifica-Roadmap-Agenti]] — azione aperta roadmap agenti + nuovi gap repo
- [[Strategia-Attuale]] — bet strategico, vincolo di reputazione
- [[Strumenti-Claude-Code]] — strumento con cui questo brainstorm è stato condotto (uso a monte sperimentale, gate 5bis applicato)
