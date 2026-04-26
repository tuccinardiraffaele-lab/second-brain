---
name: weekly
description: Usare questa skill per creare o aggiornare la review settimanale del diario. Attivare quando l'utente dice "facciamo la review della settimana", "chiudiamo la settimana", "cosa è andato questa settimana", "pianifica la prossima settimana", "retrospettiva settimanale", oppure a fine settimana per riflettere su cosa è andato, cosa no, e definire le priorità dei prossimi sette giorni.
allowed-tools: Read, Glob, Grep, Bash(date *)
---

# Review Settimanale

Skill di dominio: orchestra il flusso (quando creare, cosa chiedere, dove linkare). **Non scrive file direttamente**: ogni creazione o modifica (frontmatter, sezioni, wikilinks, checkbox, update di `aggiornato:`) viene delegata alla skill `obsidian-markdown`. Qui non si usano né `Write` né `Edit`.

## Percorso vault
`/home/raffaele/Second Brain/10-Diario/Settimanale/`

## Nome file
`Settimanale-YYYY-Www.md` — es. `Settimanale-2026-W15.md`. Calcola con `date +%G-W%V` (settimana ISO; `%G` è l'anno ISO che può differire da `%Y` a cavallo d'anno).

## Flusso

1. Calcola settimana ISO corrente e verifica con `Glob` se il file esiste.
2. Se **non esiste** → invoca `obsidian-markdown` per crearlo dal template sotto. Poi chiedi, **una domanda alla volta**:
   - "Cosa ha funzionato questa settimana? Quali vittorie, anche piccole?"
   - "Cosa non ha funzionato o ti ha bloccato?"
   - "Quali insight o lezioni porti con te?"
   - "Come sei messo rispetto agli [[OKR-Correnti]] e alle [[Crescita-Priorità-Correnti]]?"
   - "**Review pillar — cadenza settimanale** (da [[Pillar-Doppio-Livello]] + [[Processo-Review-Cadence]] Livello 1): per ciascuno dei 7 pillar strategici, cattura in una riga le evidenze di attività e le loss catturate nella settimana. Usa forma compatta: `[[NomePillar]]: <evidenza attività o «no evidenza»> — loss: <wikilink loss o «nessuna»>`. Scansiona `30-Dominio/*/Loss-*.md` creati nella settimana per cattura automatica delle loss."
   - "Quali sono le 3 priorità della prossima settimana?"
   - "Scansiona `_Sistema/Scadenziere.md`: ci sono entry con data ≤14 giorni da oggi? Quali vanno promosse tra i MIT o le priorità della prossima settimana? Quali chiuse (fatto/slittato/cancellato) vanno spostate in `## Archivio`?"
   - "**Skill globali — check re-eval** (cadenza settimanale, livello 1): scansiona `~/.claude/skills/` per modifiche ai `SKILL.md` delle skill critiche (`troubleshooting-ups`, `iterate`, `quality-pillar`, `sprint`) negli ultimi 7 giorni con `find ~/.claude/skills -name SKILL.md -mtime -7`. Se trovate → re-eval obbligatorio prima del prossimo commit (vedi `~/.claude/evals/README.md`). È uscito un nuovo modello Claude questa settimana? Se sì → re-eval delle 3 skill più usate (regressione test). Registra l'eventuale azione in 'Prossima settimana'."

   Ogni risposta viene inserita via `obsidian-markdown` nella sezione appropriata, senza sovrascrivere contenuto esistente.
3. Se **esiste** → leggilo, mostra cosa c'è già, e chiedi cosa vuole aggiornare/aggiungere. Delega l'edit a `obsidian-markdown` e aggiorna `aggiornato:` al giorno corrente.

## Template nota nuova

Frontmatter richiesto:

```yaml
---
tipo: diario
creato: YYYY-MM-DD
aggiornato: YYYY-MM-DD
stato: attivo
settimana: "YYYY-Www"
tags:
  - diario/settimanale
---
```

Nessun campo `area` (la review è trasversale). La proprietà `settimana` è il contratto con la skill `daily`, che la usa per linkare automaticamente il diario giornaliero alla review settimanale.

Scheletro sezioni (senza H1: Obsidian usa il nome file come titolo):

```markdown
## 🏆 Vittorie
- 

## 🧱 Ostacoli
- 

## 💡 Insight
- 

## 🎯 Stato OKR e Priorità
- Rispetto a [[OKR-Correnti]]: 
- Rispetto a [[Crescita-Priorità-Correnti]]: 

## 🏛️ Review pillar (cadenza settimanale)
<!-- da [[Pillar-Doppio-Livello]] + [[Processo-Review-Cadence]] L1 — capture superficiale: evidenze attività + loss catturate -->
- [[Strategia-Pillar-Leadership-Strategica]]: <evidenza o no evidenza> — loss: <wikilink o nessuna>
- [[Vendite-Pillar-Governance-Reputazionale]]: 
- [[Crescita-Pillar-Studio-Giuridico]]: 
- [[Relazioni-Pillar-Network-Target]]: 
- [[Vendite-Pillar-Sales-Positioning]]: 
- [[Strategia-Pillar-Monitoraggio-Regolatorio]]: 
- [[Prodotto-Pillar-Delivery-Piloti]]: 

## 🛠️ Skill globali — stato eval (cadenza settimanale)
<!-- da ~/.claude/evals/ — capture leggera: skill modificate questa settimana + check uscita nuovo modello -->
- Skill modificate (find -mtime -7): 
- Nuovo modello Claude questa settimana: 
- Re-eval da pianificare: 

## ⏭️ Prossima settimana
- [ ] Priorità 1
- [ ] Priorità 2
- [ ] Priorità 3
```

Nessuna sezione "Giorni della settimana" nel template: il legame con le note giornaliere è già garantito dalla proprietà `settimana` nel frontmatter, che Obsidian può interrogare dinamicamente (Bases, Dataview). Non duplicare a mano qualcosa che è già query-abile.

## Collegamenti automatici

- **Iniziative attive**: se emergono progetti sotto `20-Iniziative/🔥-Attive/`, aggiungi `[[wikilink]]` pertinenti nelle sezioni Vittorie/Ostacoli.
- **OKR e Priorità**: i `[[wikilinks]]` a `[[OKR-Correnti]]` e `[[Crescita-Priorità-Correnti]]` sono già nel template, non servono lookup runtime.

Non duplicare contenuto: collega, non copiare (principio MECE del vault).

## Dopo la scrittura

- Se sono emerse **decisioni** significative, suggerisci di registrarle con `/decision`: la review settimanale resta il contesto, la decisione ha nota propria.
- Se è emerso un **tema aperto** che merita esplorazione strutturata (scelta complessa, area da mettere a fuoco prima di decidere), proponi `/brainstorm` per una sessione framework-driven dedicata.
- Se le priorità della prossima settimana impattano un'iniziativa attiva, proponi di aggiornare la nota dell'iniziativa sotto `20-Iniziative/🔥-Attive/`.
- Ricorda al founder che i checkbox `- [ ]` in "Prossima settimana" sono tracciabili dalle query di Obsidian sulle task aperte.
- Se durante la review sono emersi commitment o review programmate oltre i 7 giorni, registrali in `[[Scadenziere]]` con data e fonte — non lasciarli solo nel diario.
