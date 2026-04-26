---
name: daily
description: Usare questa skill per creare o aggiornare la nota giornaliera del diario. Due flussi distinti — (1) pianificazione di domani la sera prima, attivata da "pianifichiamo la giornata", "pianifichiamo domani", "facciamo la pianificazione di domani"; (2) gestione della nota di oggi (riflessione mattutina, check serale), attivata da "apri il diario di oggi", "cosa devo fare oggi", "com'è andata oggi", "chiudo la giornata", "riflessione serale".
allowed-tools: Read, Glob, Grep, Bash(date *)
---

# Diario Giornaliero

Skill di dominio: orchestra il flusso (quando creare, cosa chiedere, dove linkare). **Non scrive file direttamente**: ogni creazione o modifica viene delegata alla skill `obsidian-markdown`. Qui non si usano né `Write` né `Edit`.

## Percorso vault e naming
- Cartella: `/home/raffaele/Second Brain/10-Diario/Giornaliero/`
- Nome file: `YYYY-MM-DD.md` (es. `2026-04-15.md`). Niente prefisso `Diario-`. Data via `date +%Y-%m-%d`.

## Disambiguazione dei due flussi

| Trigger dell'utente | Flusso da eseguire | Data target |
|---|---|---|
| "pianifichiamo la giornata", "pianifichiamo domani", "facciamo la pianificazione di domani" | **Flusso A — Pianificazione serale di domani** | Domani (`date -d tomorrow +%Y-%m-%d`) |
| "apri il diario di oggi", "cosa devo fare oggi", "com'è andata oggi", "chiudo la giornata", "riflessione serale" | **Flusso B — Gestione nota di oggi** | Oggi (`date +%Y-%m-%d`) |

Se ambiguo, chiedi: *"Stai pianificando domani o stai lavorando sulla nota di oggi?"*

---

## Flusso A — Pianificazione serale di domani

Attivato da "pianifichiamo la giornata" e varianti.

1. Calcola la data di domani: `date -d tomorrow +%Y-%m-%d`.
2. Verifica con `Glob` se esiste già `10-Diario/Giornaliero/<domani>.md`:
   - Se **non esiste** → crea la nota applicando il template `_Sistema/Templates/Pianificazione-Giornaliera.md` (vedi sotto per la sostituzione dei placeholder Templater).
   - Se **esiste** con contenuto → chiedi all'utente: *"La nota di domani esiste già. Vuoi continuare la pianificazione esistente o sovrascriverla?"*
3. Guida l'utente sezione per sezione del template, in ordine:
   - **Shutdown di oggi** (MIT chiusi/aperti, inbox svuotato, microattività ripianificate)
   - **Essential intent di domani** (una sola frase)
   - **MIT max 3** (con filone di riferimento da [[OKR-Correnti]] e energy required)
   - **Time-block** (mattina/pomeriggio corporate + sera lavoro proprio + buffer reattivo)
   - **Capture aperto** (input da non perdere)
4. Inserisci le risposte nella nota via `obsidian-markdown` (non sovrascrivere sezioni non toccate).
5. Aggiorna `aggiornato:` al giorno corrente.

### Sostituzione placeholder Templater (quando creo via filesystem)

Il template `_Sistema/Templates/Pianificazione-Giornaliera.md` usa sintassi Templater (`<% ... %>`) che funziona **solo dentro Obsidian**. Quando creo il file via filesystem, devo sostituire a mano:

| Placeholder Templater | Sostituire con |
|---|---|
| `<% tp.date.now("YYYY-MM-DD") %>` | data odierna (`date +%Y-%m-%d`) |
| `<% tp.file.title %>` | data target = domani |
| `<% moment(tp.file.title).subtract(1, 'day').format("YYYY-MM-DD") %>` | oggi (= domani − 1) |

---

## Flusso B — Gestione nota di oggi

Attivato dai trigger di "oggi". Mantiene il comportamento storico della skill.

1. Calcola la data odierna: `date +%Y-%m-%d`. Verifica con `Glob` se il file esiste.
2. Se **non esiste** → invoca `obsidian-markdown` per crearlo dal template "nota di oggi" (sotto), poi chiedi: *"Quali sono le tue 3 priorità per oggi?"*
3. Se **esiste** → leggilo e chiedi in ordine:
   - "Come è andata la giornata rispetto alle priorità?"
   - "C'è stato un insight o una lezione importante?"
   - "Qualcosa da portare a domani?"

   Poi invoca `obsidian-markdown` per: (a) aggiungere le risposte nelle sezioni appropriate **senza sovrascrivere** il contenuto esistente, (b) aggiornare `aggiornato:` al giorno corrente.

### Template "nota di oggi" (Flusso B)

Frontmatter:

```yaml
---
tipo: diario
creato: YYYY-MM-DD
aggiornato: YYYY-MM-DD
stato: attivo
---
```

Nessun campo `area` (il diario è trasversale).

Scheletro sezioni (senza H1: Obsidian usa il nome file come titolo):

```markdown
## 🎯 Focus del giorno
- [ ] Priorità 1
- [ ] Priorità 2
- [ ] Priorità 3

## 📝 Note

## 💡 Insight
```

---

## Collegamenti automatici (entrambi i flussi)

- Calcola la settimana ISO con `date +%G-W%V` (es. `2026-W15`). Cerca con `Grep` in `10-Diario/Settimanale/` la nota che dichiara quella settimana nel frontmatter (proprietà `settimana`, formato `YYYY-Www`); se esiste, aggiungi un `[[wikilink]]` alla nota trovata.
- Se l'utente menziona un progetto sotto `20-Iniziative/`, aggiungi il `[[wikilink]]` pertinente.
- Non duplicare contenuto: collega, non copiare (principio MECE del vault).
