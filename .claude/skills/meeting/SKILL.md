---
name: meeting
description: Usare questa skill per registrare una riunione con partecipanti, agenda, decisioni prese e azioni da fare. Attivare quando l'utente dice "ho una call con…", "prepara la nota per il meeting", "ho appena finito una riunione", "segna cosa ci siamo detti", "riassumi la call", oppure ogni volta che emerge il bisogno di catturare il contesto prima, durante o dopo un incontro con una o più persone.
allowed-tools: Read, Glob, Grep, Bash(date *)
---

# Nota Riunione

Skill di dominio: orchestra il flusso (quando creare, cosa chiedere, dove linkare). **Non scrive file direttamente**: ogni creazione o modifica (frontmatter, sezioni, wikilinks, checkbox, update di `aggiornato:`) viene delegata alla skill `obsidian-markdown`. Qui non si usano né `Write` né `Edit`.

## Percorso vault
`/home/raffaele/Second Brain/10-Diario/Riunioni/`

## Nome file
`YYYY-MM-DD-Titolo-Riunione.md` — kebab-case con iniziale maiuscola su ogni parola del titolo. Esempio: `2026-04-13-Sync-Prodotto-Q2.md`. Data odierna via `date +%Y-%m-%d`.

## Flusso

Chiedi **una domanda alla volta**, in questa sequenza:

1. "Qual è il titolo della riunione?" → determina il nome file.
2. "Con chi è la riunione?" → crea un `[[wikilink]]` per ogni persona. Per ciascuna, verifica con `Glob` se esiste già una nota sotto `40-Conoscenza/Persone/`; se manca, annota mentalmente che andrà creata (vedi "Dopo la scrittura").
3. "Qual è l'obiettivo della riunione?"
4. "Punti chiave emersi nella discussione?"
5. "Quali decisioni sono state prese? Per ciascuna, qual è il rationale?"
6. "Quali azioni sono emerse? Chi fa cosa entro quando?"
7. "C'è qualcosa di non detto, una tensione o un segnale debole da monitorare?"

Dopo aver raccolto tutto, invoca `obsidian-markdown` per creare il file dal template sotto.

## Template nota

Frontmatter richiesto:

```yaml
---
tipo: riunione
creato: YYYY-MM-DD
aggiornato: YYYY-MM-DD
stato: completato
tags:
  - riunione
  - <tag gerarchico senza `#`, es. `riunione/1-1`, `riunione/board`>
area: <un solo valore tra: visione | strategia | prodotto | persone | finanza | vendite | operazioni | crescita | relazioni | strumenti>
partecipanti:
  - "[[Persona-1]]"
  - "[[Persona-2]]"
---
```

Scheletro sezioni (senza H1: Obsidian usa il nome file come titolo):

```markdown
## Partecipanti
- [[Persona-1]] — ruolo
- [[Persona-2]] — ruolo

## Obiettivo
[Perché ci siamo incontrati]

## Discussione
[Punti chiave emersi, in ordine]

## Decisioni
1. **[Decisione]** — rationale: [perché]

## Azioni
- [ ] [Azione] → [[Persona]] entro YYYY-MM-DD

## Note a margine
[Osservazioni, tensioni, segnali deboli]
```

## Collegamenti automatici

- **Nota giornaliera**: cerca con `Glob` `10-Diario/Giornaliero/Diario-YYYY-MM-DD.md` per la data odierna. Se esiste, delega a `obsidian-markdown` l'append di un `[[wikilink]]` alla riunione nella sezione note del diario se presente, altrimenti in fondo alla nota. Non hardcodare qui il nome esatto della sezione: il template di `daily` può evolvere.
- **Iniziativa correlata**: se l'argomento tocca un progetto sotto `20-Iniziative/`, aggiungi il `[[wikilink]]` pertinente nel corpo della riunione.

Non duplicare contenuto: collega, non copiare (principio MECE del vault).

## Dopo la scrittura

- Per ogni partecipante **senza** nota in `40-Conoscenza/Persone/`, proponi al founder di crearla (nome, ruolo, contesto della relazione). Se conferma, delega la creazione a `obsidian-markdown`.
- Se sono emerse **decisioni**, suggerisci di registrarle con la skill `/decision` (se disponibile nel vault) per avere una nota canonica dedicata: la riunione resta il contesto, la decisione ha nota propria. Se `/decision` non è ancora implementata, proponi comunque di creare la nota decisione direttamente via `obsidian-markdown` seguendo le regole di frontmatter del `CLAUDE.md` del vault.
- Se sono emerse **azioni con scadenza**, ricorda al founder che i checkbox `- [ ]` sono tracciabili dalle query di Obsidian sulle task aperte.
