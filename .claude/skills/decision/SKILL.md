---
name: decision
description: Usare questa skill per registrare una decisione importante con contesto, alternative considerate e rationale. Attivare quando l'utente dice "ho deciso di…", "scegliamo X al posto di Y", "facciamo così perché…", "registriamo questa decisione", "mettiamola a terra", oppure quando emerge una scelta significativa per business, prodotto, architettura, persone o strategia con impatto non banale o difficile da invertire.
allowed-tools: Read, Glob, Grep, Bash(date *)
---

# Registra Decisione

Skill di dominio: orchestra il flusso (quando creare, cosa chiedere, dove linkare). **Non scrive file direttamente**: ogni creazione o modifica (frontmatter, sezioni, wikilinks, update di `aggiornato:`) viene delegata alla skill `obsidian-markdown`. Qui non si usano né `Write` né `Edit`.

## Percorso vault

Determinato dall'area della decisione, direttamente nella cartella di dominio corrispondente (nessuna sottocartella `Decisioni/`: il filtro avviene via `tipo: decisione` nel frontmatter, come da `CLAUDE.md` del vault):

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

## Nome file

`Titolo-Decisione.md` — kebab-case con iniziale maiuscola su ogni parola, senza prefisso data (le note di dominio non sono temporali; la data è in `creato:`). Esempio: `Pricing-Piano-Pro.md`.

## Flusso

Chiedi **una domanda alla volta**, in questa sequenza:

1. "Qual è la decisione presa?" → determina titolo e nome file.
2. "A quale area appartiene?" → sceglie la cartella (vedi tabella sopra).
3. "Qual è il contesto che ha portato a questa scelta?"
4. "Quali alternative hai considerato? Perché le hai scartate?"
5. "Perché hai scelto questa opzione — quali dati o intuizioni la supportano?"
6. "Quali rischi o trade-off accetti, e come li mitighi?"
7. "Quanto è reversibile questa decisione (alta | media | bassa)?"
8. "Qual è l'impatto (alto | medio | basso)?"
9. "Entro quando la rivedi, e con quali criteri di successo?"

Dopo aver raccolto tutto, invoca `obsidian-markdown` per creare il file dal template sotto.

## Template nota

Frontmatter richiesto:

```yaml
---
tipo: decisione
creato: YYYY-MM-DD
aggiornato: YYYY-MM-DD
stato: attivo
tags:
  - decisione/<area, es. strategia | prodotto | finanza>
area: <un solo valore tra: visione | strategia | prodotto | persone | finanza | vendite | operazioni | crescita | relazioni | strumenti>
reversibilità: <alta | media | bassa>
impatto: <alto | medio | basso>
scadenza-revisione: YYYY-MM-DD
---
```

Scheletro sezioni (senza H1: Obsidian usa il nome file come titolo):

```markdown
## Contesto
[Situazione che ha portato alla decisione]

## Decisione
**[La decisione in una frase chiara]**

## Alternative considerate
1. **[Alternativa A]** — scartata perché [motivo]
2. **[Alternativa B]** — scartata perché [motivo]

## Rationale
[Perché questa scelta, quali dati/intuizioni la supportano]

## Rischi e trade-off
- [Rischio 1] — mitigazione: [come]
- [Trade-off accettato]

## Revisione
Rivedere entro [[YYYY-MM-DD]] — criteri di successo: [metriche]

## Note collegate
- [[Strategia-Attuale]]
- [[Nota-correlata]]
```

## Collegamenti automatici

- **Nota giornaliera**: cerca con `Glob` `10-Diario/Giornaliero/Diario-YYYY-MM-DD.md` per la data odierna. Se esiste, delega a `obsidian-markdown` l'append di un `[[wikilink]]` alla decisione.
- **Iniziativa correlata**: se la decisione tocca un progetto sotto `20-Iniziative/`, aggiungi il `[[wikilink]]` pertinente nel corpo.
- **Riunione di origine**: se la decisione è emersa da una riunione in `10-Diario/Riunioni/`, linka la riunione e viceversa (la nota riunione cita la decisione come wikilink nella sezione Decisioni).

Non duplicare contenuto: collega, non copiare (principio MECE del vault).

## Dopo la scrittura

- Se la decisione impatta la **strategia**, proponi al founder di aggiornare `30-Dominio/32-Strategia-Business/Strategia-Attuale.md` (delegando l'edit a `obsidian-markdown`).
- Se la decisione impatta **progetti attivi**, proponi di aggiornare `_Sistema/Dashboard.md`.
- Se la decisione tocca **OKR** correnti, proponi di aggiornare `30-Dominio/32-Strategia-Business/OKR-correnti.md`.
- Ricorda al founder la `scadenza-revisione`: è tracciabile via query Obsidian su `tipo: decisione` con data vicina.
