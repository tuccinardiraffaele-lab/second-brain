---
name: session-close
description: Usare questa skill per chiudere in modo strutturato una sessione di lavoro significativa, facendo domande al founder per identificare cosa salvare e scrivendo le note nel vault. Attivare quando l'utente dice "chiudiamo la sessione", "salviamo quello che è emerso", "fine sessione", "cosa portiamo a casa", "fammi il wrap-up", oppure al termine naturale di una conversazione o di un blocco di lavoro in cui sono emersi insight, decisioni, riflessioni o azioni da preservare.
---

# Chiusura sessione strutturata

## Processo di chiusura (segui ESATTAMENTE questi step)

### Step 1: Riepilogo della sessione
Riepiloga in 3-5 bullet cosa è emerso dalla sessione:
- Decisioni prese
- Insight generati
- Problemi risolti
- Domande aperte rimaste
- Azioni concordate

### Step 2: Questionario rapido (fai UNA domanda alla volta)

**Domanda 1**: "Ho identificato questi elementi dalla nostra sessione:
[lista]. C'è qualcosa che manca o che vuoi aggiungere?"

**Domanda 2**: "Di questi elementi, quali vuoi salvare nel vault?
(tutti / seleziona / nessuno)"

**Domanda 3** (se ci sono decisioni): "Per la decisione su [X],
qual è stato il ragionamento principale? Voglio catturarlo."

**Domanda 4**: "C'è una priorità o un cambio di focus che devo
aggiornare nella Dashboard?"

### Step 3: Scrittura nel vault
Per ogni elemento confermato:
1. Determina la cartella corretta (segui la mappa di `obsidian-writer`)
2. Verifica se esiste già una nota da aggiornare (Glob/Grep)
3. Scrivi/aggiorna delegando la sintassi a `obsidian-markdown` e il frontmatter/destinazione a `obsidian-writer`
4. Inserisci wikilinks a note correlate
5. Conferma al founder cosa hai scritto e dove

### Step 4: Aggiorna la Dashboard
Solo se ci sono cambiamenti a progetti in `🔥-Attive/` o priorità,
aggiorna `_Sistema/Dashboard.md`.

### Step 5: Aggiorna il diario
Aggiungi un entry alla nota giornaliera
`10-Diario/Giornaliero/YYYY-MM-DD.md` con:
```markdown
## Sessione Claude [HH:MM]
- **Focus**: [argomento principale]
- **Outcome**: [risultato principale]
- **Note salvate**: [[Nota-1]], [[Nota-2]]
- **Prossimi passi**: [azioni]
```

### Step 6: Aggiorna MOC progetti toccati
Per ogni nota salvata con frontmatter `progetto: "[[NomeProgetto]]"`
(tipicamente note `architettura`, `debito-tecnico`, `problema-risolto`
create da `/sprint`), apri la MOC del progetto in
`20-Iniziative/🔥-Attive/<NomeProgetto>/<NomeProgetto>.md` e aggiungi
sotto `## Log sessioni` un wikilink alla nota giornaliera di oggi:

```markdown
## Log sessioni
- [[Diario-YYYY-MM-DD]]
```

Se il wikilink del giorno è già presente (più sprint nella stessa
giornata), non duplicarlo. Delega l'edit a `obsidian-markdown`.

### Step 7: Conferma finale
"Sessione chiusa. Ho salvato [N] note in [cartelle].
La Dashboard è aggiornata. Buon lavoro!"

## Se il founder dice "niente da salvare"
Rispondi: "Ok, nessun salvataggio. Se cambi idea, puoi
sempre invocare /session-close più tardi. A presto!"
