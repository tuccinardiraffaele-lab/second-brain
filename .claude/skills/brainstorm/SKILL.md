---
name: brainstorm
description: Guida il founder in una sessione di brainstorming strutturata framework-driven (Cynefin → Rumelt o PR-FAQ → pre-mortem/WRAP) su temi strategici o deep dive di progetto. Attivare con "aiutami a ragionare su…", "facciamo un brainstorming", "devo pensare a…", "voglio andare deep su…", "esploriamo insieme", o quando emerge un problema aperto da mettere a fuoco prima di decidere. Se la decisione è già presa usa `/decision`; per note atomiche tecniche di progetto usa `/sprint`.
allowed-tools: Read, Glob, Grep, Bash(date *)
---

# Brainstorm — Riflessione framework-driven

Skill di dominio: orchestra il flusso (quale framework applicare, cosa chiedere, dove scrivere). **Non scrive file direttamente**: ogni creazione o modifica viene delegata a `obsidian-markdown`. Qui non si usano né `Write` né `Edit`.

Il brainstorming qui non è generazione libera di idee né coaching socratico: è **applicazione esplicita di framework decisionali validati**. Claude nomina il framework che sta usando, ne applica i passi, e tiene traccia esplicita degli output intermedi.

## Gate di apertura — Modalità ragionamento a monte

Prima di entrare nel Router, ricorda e applica la **sezione 5bis del `~/.claude/CLAUDE.md` globale** ("Modalità ragionamento a monte"):

- **Niente sycophancy** — se la tesi del founder ha un buco, chiamalo subito, non dopo.
- **Niente premesse inventate** — ogni fatto usato per dedurre va chiesto o marcato come ipotesi non verificata.
- **Niente sovrastrutture non realizzabili** — ogni mossa deve essere eseguibile nel contesto reale (vincoli di tempo, competenza, capitale, reputazione).
- **Fonti autorevoli** — i framework citati in questa skill (Cynefin/Snowden, Rumelt, Bryar & Carr, Klein pre-mortem, Heath WRAP) sono track record comprovato; non aggiungere framework "inventati" o parafrasi non attribuite. Se serve una fonte esterna, dichiaralo e chiedi conferma prima di procedere.

Se durante la sessione stai per violare uno dei divieti, **fermati e segnalalo** invece di procedere — anche a costo di rompere il ritmo del framework.

## Metodologia — tre strati

La sessione combina tre framework in sequenza. Ogni strato ha uno scopo preciso.

### Strato 1 — Router (Cynefin, Snowden, HBR 2007)

Prima domanda sempre: classifica il problema.

- **Clear** — causa-effetto ovvia, best practice nota → non fare brainstorming, applica la procedura. Esci dalla skill.
- **Complicated** — richiede analisi, esistono buone pratiche → procedi con lo strato 2 in modalità analitica.
- **Complex** — causa-effetto visibile solo a posteriori, serve probing → strato 2 con enfasi su piccoli esperimenti.
- **Chaotic** — crisi, serve azione rapida → non brainstorming, proponi di uscire e agire.

Chiedi: *"In una frase, qual è il problema? Lo conosci bene, richiede analisi, o è territorio nuovo?"*

### Strato 2 — Sostanza

In base al **taglio** (strategico vs progetto), applica uno dei due scheletri.

**Taglio strategico** → **Rumelt kernel** (Good Strategy / Bad Strategy, 2011):

1. **Diagnosis** — "Qual è la natura della sfida? Non la soluzione, il problema." Forza una diagnosi prima di saltare alle opzioni.
2. **Guiding policy** — "Qual è l'approccio generale che affronta la diagnosi? Cosa farai, cosa non farai?"
3. **Coherent actions** — "Quali azioni concrete, coordinate, implementano la guiding policy?"

Obiettivo: distinguere strategia vera da lista di obiettivi / OKR / slogan.

**Taglio progetto** → **Working Backwards / PR-FAQ** (Amazon, Bryar & Carr 2021):

1. **Press release** — "Se annunciassi oggi il risultato di questa scelta, cosa direbbe il comunicato? Cliente, problema, beneficio, perché ora."
2. **Customer FAQ** — "Quali 3-5 domande farebbe un cliente/utente scettico?"
3. **Internal FAQ** — "Quali 3-5 domande interne sono scomode? Costo, rischio, dipendenze, trade-off tecnici."

Obiettivo: forzare chiarezza sull'esito desiderato prima di discutere implementazione.

### Strato 3 — Challenge (Pre-mortem + WRAP)

Prima di chiudere, sempre, due passaggi.

**Pre-mortem** (Klein, HBR 2007): *"È tra un anno. La scelta che stiamo valutando è fallita. Dammi le tre cause più probabili."* Forza identificazione dei rischi nascosti.

**WRAP — Widen & Reality-test** (Heath, Decisive 2013):
- **Widen**: "Se questa opzione non fosse disponibile, cosa faresti? Aggiungiamo almeno un'alternativa seria."
- **Reality-test**: "Quale dato, test o conversazione di 1h potrebbe cambiarti idea? Se nessuno, stai decidendo per fede."

Obiettivo: rompere narrow framing e confirmation bias.

## Flusso operativo

1. **Classifica (Cynefin)** — una domanda, risposta rapida. Se Clear/Chaotic → esci.
2. **Determina il taglio** — strategico o progetto? Se strategico, chiedi l'`area` (vedi tabella sotto in "Percorso vault e nome file"). Se progetto, chiedi quale progetto di `20-Iniziative/🔥-Attive/`.
3. **Applica lo scheletro** (Rumelt o PR-FAQ) — una fase alla volta, nomina il framework esplicitamente ("ora siamo in Diagnosis").
4. **Challenge layer** — pre-mortem + WRAP. Non saltabile.
5. **Sintesi e follow-up** — scrivi la nota via `obsidian-markdown`, proponi il prossimo passo.

Non applicare tutti i framework "a tappeto": il router decide. Se il founder dà già risposte mature su una fase, non insistere — passa alla successiva.

## Percorso vault e nome file

Il percorso dipende dal **taglio**:

**Taglio strategico** → cartella di dominio corrispondente all'`area`:

| area | cartella |
|---|---|
| visione | `30-Dominio/31-Visione-e-Valori/` |
| strategia | `30-Dominio/32-Strategia-Business/` |
| prodotto | `30-Dominio/33-Prodotto-e-Tecnologia/` |
| persone | `30-Dominio/34-Persone-e-Leadership/` |
| finanza | `30-Dominio/35-Finanza/` |
| vendite | `30-Dominio/36-Vendite-e-Crescita/` |
| operazioni | `30-Dominio/37-Operazioni/` |
| crescita | `30-Dominio/38-Crescita-Personale/` |
| relazioni | `30-Dominio/39-Relazioni-e-Network/` |
| strumenti | `30-Dominio/3A-Strumenti-e-Sistemi/` |

**Taglio progetto** → dentro la cartella del progetto: `20-Iniziative/🔥-Attive/<NomeProgetto>/`.

**Nome file**: `Brainstorm-Titolo.md` — kebab-case con iniziale maiuscola, titolo breve che cattura la domanda di fondo. Nessun prefisso data (la data è in `creato:`). Esempio: `Brainstorm-Pricing-Piano-Pro.md`. Se si torna sullo stesso tema, aggiorna il file esistente e la data `aggiornato:`; se il tema è maturato in una scelta, proponi `/decision`.

## Template nota

Frontmatter richiesto:

```yaml
---
tipo: riflessione
creato: YYYY-MM-DD
aggiornato: YYYY-MM-DD
stato: attivo
tags:
  - brainstorm/<strategico | progetto>
  - brainstorm/<area o nome-progetto>
area: <visione | strategia | prodotto | persone | finanza | vendite | operazioni | crescita | relazioni | strumenti>
progetto: "[[NomeProgetto]]"
cynefin: <complicated | complex>
framework: <rumelt | pr-faq>
---
```

**Note sui campi:**
- `tags`: il secondo segmento va normalizzato in kebab-case minuscolo (es. `brainstorm/pricing-piano-pro`, non `brainstorm/PricingPianoPro`). Coerente con la convenzione dei tag gerarchici del vault.
- `progetto`: includere solo se taglio = progetto; altrimenti omettere la riga.
- `cynefin` e `framework`: campi custom non previsti dalla tassonomia base in `CLAUDE.md`, usati per query e filtri Obsidian (Bases/Dataview) su questa famiglia di note.

Scheletro sezioni (senza H1). La struttura varia per framework applicato.

**Se framework = rumelt:**

```markdown
## Domanda di fondo
[La domanda in una frase]

## Classificazione (Cynefin)
[Complicated | Complex] — [motivo]

## Diagnosis
[La natura reale del problema, non la soluzione]

## Guiding policy
[Approccio generale, cosa farai / cosa non farai]

## Coherent actions
- [Azione 1]
- [Azione 2]

## Pre-mortem
- [Causa di fallimento 1]
- [Causa 2]
- [Causa 3]

## Alternative e reality-test
- Alternative considerate: [almeno una oltre a quella preferita]
- Cosa cambierebbe idea: [dato/test/conversazione]

## Prossimo passo
- [ ] [Azione concreta, entro quando]

## Note collegate
- [[...]]
```

**Se framework = pr-faq:**

```markdown
## Domanda di fondo
[La domanda in una frase]

## Classificazione (Cynefin)
[Complicated | Complex] — [motivo]

## Press release (interno)
**Titolo**: [...]
**Sottotitolo**: [...]
**Cliente e problema**: [...]
**Soluzione e beneficio**: [...]
**Perché ora**: [...]

## Customer FAQ
1. [Domanda] → [risposta]
2. ...

## Internal FAQ
1. [Domanda scomoda] → [risposta onesta]
2. ...

## Pre-mortem
- [Causa di fallimento 1]
- [Causa 2]
- [Causa 3]

## Alternative e reality-test
- Alternative considerate: [...]
- Cosa cambierebbe idea: [...]

## Prossimo passo
- [ ] [...]

## Note collegate
- [[...]]
```

## Collegamenti automatici

- **Nota giornaliera**: cerca con `Glob` `10-Diario/Giornaliero/Diario-YYYY-MM-DD.md` per la data odierna. Se esiste, delega a `obsidian-markdown` l'append di un `[[wikilink]]` al brainstorming.
- **Taglio strategico**: linka a `30-Dominio/32-Strategia-Business/Strategia-Attuale.md` e, se pertinente, `OKR-correnti.md`.
- **Taglio progetto**: linka alla MOC del progetto e compila `progetto:` nel frontmatter.

Non duplicare contenuto: collega, non copiare (MECE).

## Dopo la scrittura — proposte di follow-up

Una sola proposta, la più rilevante:

- Se è emersa una **scelta matura** → `/decision`.
- Se è un brainstorming **tecnico di progetto** con note atomiche utili (architettura, debito, problema risolto) → `/sprint`.
- Se il reality-test ha identificato un **dato/test** da raccogliere → ricorda il next step con deadline.
- Se non è maturo per nessuna → chiudi senza forzare.

## Riferimenti metodologici

- Snowden, *A Leader's Framework for Decision Making*, HBR 2007 (Cynefin)
- Rumelt, *Good Strategy / Bad Strategy*, Crown 2011 (kernel)
- Bryar & Carr, *Working Backwards*, 2021 (PR/FAQ)
- Klein, *Performing a Project Premortem*, HBR 2007
- Heath & Heath, *Decisive*, 2013 (WRAP)
