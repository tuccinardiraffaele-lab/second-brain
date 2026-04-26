---
name: obsidian-writer
description: Scrive note strutturate nel vault Obsidian con frontmatter YAML corretto, wikilinks e struttura MECE. Usare quando si devono creare o aggiornare note nel second brain.
allowed-tools: Write, Edit, Read, Glob, Grep, Bash(mkdir *)
---

# Obsidian Writer — Guida alla scrittura nel vault

Questa skill copre **destinazione, frontmatter di dominio e struttura MECE** delle note del second brain. Non duplica la sintassi Obsidian.

## Delega obbligatoria

Per la sintassi Obsidian (wikilinks, embed, callout, properties, tag, comments, math, mermaid) **devi invocare `obsidian-markdown`**. Non scrivere quella sintassi a mano da qui.

Per altre forme di contenuto nel vault, usa la skill giusta:

| Forma | Skill |
|---|---|
| File `.base` (viste database) | `obsidian-bases` |
| File `.canvas` (mappe visive) | `json-canvas` |
| Ricerca/lettura contesto dal vault (check duplicati, note correlate) | `obsidian-reader` |
| Operazioni CLI sul vault (search, open, task, plugin) | `obsidian-cli` |
| Estrazione contenuto da URL web | `defuddle` |

## Percorso vault
- Da WSL/Linux: `/home/raffaele/Second Brain`
- Da Windows: `\\wsl.localhost\Ubuntu-22.04\home\raffaele\Second Brain`

## Processo di scrittura (SEMPRE seguire questi step)

### 1. Determina la destinazione
> **Source of truth.** Questa skill è il riferimento canonico per il filing delle note. Se un'altra skill introduce o modifica una convenzione strutturale (es. cartelle progetto, nuovi tipi di nota), aggiorna **prima** questa tabella e poi allinea le altre skill.

Mappa il contenuto alla cartella corretta:

| Tipo di contenuto        | Cartella destinazione                    |
|--------------------------|------------------------------------------|
| Cattura rapida           | 00-Inbox/                                |
| Nota giornaliera         | 10-Diario/Giornaliero/YYYY-MM-DD.md      |
| Review settimanale       | 10-Diario/Settimanale/YYYY-Wnn.md        |
| Review mensile           | 10-Diario/Mensile/YYYY-MM.md             |
| Review trimestrale       | 10-Diario/Trimestrale/YYYY-Qn.md         |
| Nota riunione            | 10-Diario/Riunioni/YYYY-MM-DD-Titolo.md  |
| Progetto attivo (MOC)    | 20-Iniziative/🔥-Attive/<Nome>/<Nome>.md — sempre dentro la cartella omonima, anche se al momento non ha satelliti |
| Nota satellite di progetto attivo (azione aperta, verifica, chiarimento, nota atomica) | 20-Iniziative/🔥-Attive/<Nome-Progetto>/<Nome-Nota>.md, con `progetto: "[[Nome-Progetto]]"` nel frontmatter |
| Processo ricorrente      | 20-Iniziative/♻️-Ricorrenti/<Nome>/<Nome>.md se ha satelliti; altrimenti 20-Iniziative/♻️-Ricorrenti/<Nome>.md |
| Idea in esplorazione     | 20-Iniziative/〰️-In-Esplorazione/<Nome>.md (promuovi a cartella quando compaiono satelliti) |
| Progetto in pausa        | 20-Iniziative/💤-In-Pausa/<Nome>/<Nome>.md se ha satelliti; altrimenti 20-Iniziative/💤-In-Pausa/<Nome>.md |
| Visione/valori           | 30-Dominio/31-Visione-e-Valori/          |
| Strategia                | 30-Dominio/32-Strategia-Business/        |
| Prodotto/tech            | 30-Dominio/33-Prodotto-e-Tecnologia/     |
| Leadership/persone       | 30-Dominio/34-Persone-e-Leadership/      |
| Finanza                  | 30-Dominio/35-Finanza/                   |
| Vendite/crescita         | 30-Dominio/36-Vendite-e-Crescita/        |
| Operazioni               | 30-Dominio/37-Operazioni/                |
| Crescita personale       | 30-Dominio/38-Crescita-Personale/        |
| Relazioni/network        | 30-Dominio/39-Relazioni-e-Network/       |
| Strumenti/sistemi        | 30-Dominio/3A-Strumenti-e-Sistemi/       |
| Concetto/framework       | 40-Conoscenza/Concetti/                  |
| Fonte/libro/articolo     | 40-Conoscenza/Fonti/                     |
| Persona/contatto         | 40-Conoscenza/Persone/                   |
| Mappa concettuale (MOC)  | 40-Conoscenza/Mappe/                     |
| Template                 | _Sistema/Template/                       |

### 2. Verifica duplicati
Prima di creare una nuova nota, cerca nel vault una nota affine (preferisci `obsidian-reader` o `obsidian-cli`; in fallback Glob/Grep). Se esiste, aggiornala invece di crearne una nuova (principio MECE).

### 3. Naming dei file
- Convenzione: **Iniziale-Maiuscola-kebab-case** (es. `Strategia-Q2-2026.md`).
- Trattino `-` al posto degli spazi.
- Date sempre `YYYY-MM-DD`. Per la data corrente usa `date +%Y-%m-%d` via Bash, non hardcodare.
- Mai creare due file che differiscono solo per case (Linux distingue, Windows no).
- Le cartelle in `20-Iniziative/` contengono emoji nel nome (`🔥-Attive`, `♻️-Ricorrenti`, `〰️-In-Esplorazione`, `💤-In-Pausa`): cita il path esatto con virgolette in Bash per evitare problemi di escaping.

### 4. Frontmatter YAML obbligatorio

Campi e valori ammessi (allineati a `CLAUDE.md`):

- `tipo`: `decisione | riflessione | processo | riunione | concetto | persona | fonte | progetto | diario | mappa`
  - Per review settimanale/mensile/trimestrale → `tipo: diario`.
  - I template in `_Sistema/Template/` hanno frontmatter libero (servono come scaffold).
- `stato`: `attivo | completato | in-pausa | archiviato`
- `area`: `visione | strategia | prodotto | persone | finanza | vendite | operazioni | crescita | relazioni | strumenti`
- `creato`, `aggiornato`: `YYYY-MM-DD` (data corrente)
- `tags`: lista, lowercase gerarchici con `/` (`strategia/okr`, `decisione/prodotto`). **Senza `#`** nel frontmatter YAML (il `#` si usa solo nel corpo della nota).

```yaml
---
tipo: decisione
creato: YYYY-MM-DD
aggiornato: YYYY-MM-DD
stato: attivo
tags:
  - strategia/pricing
  - decisione/prodotto
area: strategia
---
```

### 5. Struttura del corpo
Lo scaffold sotto è solo lo **scheletro semantico** delle sezioni. Per la sintassi Obsidian effettiva (wikilinks, callout, embed, properties, alias) → `obsidian-markdown`.

```markdown
# Titolo della nota

> [!info] Contesto
> Perché questa nota esiste, cosa l'ha generata.

## Contenuto principale
Il cuore della nota — decisione presa, riflessione, processo, concetto.

## Implicazioni
Cosa cambia, quali sono le conseguenze.

## Prossimi passi
- [ ] Azione concreta con scadenza
- [ ] Altra azione

## Note collegate
- [[Nota-correlata]] — relazione
```

### 6. Wikilinks
- Collega SEMPRE ad almeno **1 nota esistente** (verifica prima per evitare link rotti). Aggiungine altre quando ha senso semantico, senza forzare.
- Per la sintassi completa di wikilinks, embed, callout, properties → usa `obsidian-markdown`.

### 7. Aggiorna la Dashboard (solo per progetti in 🔥-Attive)
Aggiorna `_Sistema/Dashboard.md` solo quando crei un nuovo progetto in `20-Iniziative/🔥-Attive/` o cambi lo stato di uno esistente. Negli altri casi, non toccarla.

## Encoding
- Scrivi SEMPRE in UTF-8 senza BOM.
- Caratteri italiani con accenti (à, è, é, ì, ò, ù) sono supportati.
