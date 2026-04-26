---
name: obsidian-reader
description: Cerca e legge contesto rilevante dal vault Obsidian. Usare prima di rispondere a domande strategiche, quando serve contesto storico, o per trovare note correlate.
allowed-tools: Read, Glob, Grep, Bash(obsidian *), Bash(find *)
---

# Obsidian Reader — Ricerca contesto nel vault

Questa skill copre **strategia di ricerca e caricamento mirato** del vault. Non duplica la sintassi Obsidian né le operazioni di scrittura.

## Delega obbligatoria

| Forma | Skill / Agente |
|---|---|
| Esplorazione ampia / ricerche multi-step | sub-agent `vault-explorer` (quando disponibile) |
| Ricerche operative su vault aperto (`search`, `backlinks`, `tasks`, `tags`, `property:get`, `daily:read`) | `obsidian-cli` |
| Sintassi Obsidian in output (wikilinks, embed, callout) | `obsidian-markdown` |
| Scrittura/aggiornamento note | `obsidian-writer` (o sub-agent `obsidian-writer-agent`) |
| Estrazione contenuto da URL web | `defuddle` |

Regola: se Obsidian è aperto, **preferisci `obsidian-cli`** a Grep/find — è più veloce e indicizzato. Cadi su Grep/Glob/find solo se la CLI non è disponibile o serve scansione filesystem grezza.

## Percorso vault
- Da WSL/Linux: `/home/raffaele/Second Brain`
- Da Windows: `\\wsl.localhost\Ubuntu-22.04\home\raffaele\Second Brain`

## Regola globale di esclusione
Tutte le ricerche filesystem (Glob, Grep, find) devono escludere `.obsidian/` e `.trash/`:
- Glob: `**/*.md` e poi filtrare, oppure restringere a sotto-cartelle note (`10-Diario/**`, `30-Dominio/**`).
- Grep: aggiungere `--glob '!.obsidian/**' --glob '!.trash/**'`.
- find: `-not -path "*/.obsidian/*" -not -path "*/.trash/*"`.

## Strategie di ricerca (in ordine di efficienza)

### 1. Vault aperto → `obsidian-cli`
```bash
obsidian search query="strategia pricing" limit=20
obsidian backlinks file="OKR-correnti"
obsidian tasks query="todo" limit=50
obsidian tags sort=count counts
obsidian property:get name="tipo" file="Strategia-Q2-2026"
```

### 2. Ricerca per tag / proprietà frontmatter (filesystem)
```bash
# Tutte le decisioni
rg -l "^tipo: decisione$" "/home/raffaele/Second Brain" \
  --glob '*.md' --glob '!.obsidian/**'
```
(equivalente Grep tool: `pattern: "^tipo: decisione$"`, `glob: "*.md"`, `output_mode: "files_with_matches"`)

### 3. Ricerca per contenuto (filesystem)
Grep tool con `pattern` keyword, `glob: "*.md"`, `-i: true`, `output_mode: "content"` per vedere lo snippet, oppure `files_with_matches` per la lista.

### 4. Note recenti (ultimi N giorni)
```bash
find "/home/raffaele/Second Brain" -name "*.md" \
  -not -path "*/.obsidian/*" -not -path "*/.trash/*" \
  -mtime -7 -type f | sort
```

### 5. Esplorazione struttura
Glob tool con pattern `30-Dominio/**/*.md` (o sotto-cartella di interesse). Evita scansioni full-vault salvo necessità.

## Pattern di caricamento tiered
1. **Entra dagli indici**: parti da `_Sistema/Dashboard.md` o dalle MOC in `40-Conoscenza/Mappe/` per orientarti, non dal contenuto grezzo.
2. **Restringi per area/tipo**: usa frontmatter (`tipo:`, `area:`) prima di full-text.
3. **Leggi solo il necessario**: apri le note candidate una alla volta, non tutto il vault.
4. **Segui i wikilinks**: da una nota rilevante, espandi solo verso note linkate utili.

## Quando NON usare questa skill
- Per **scrivere** o aggiornare note → `obsidian-writer`.
- Per estrarre testo da una **URL web** → `defuddle`.
- Per creare **viste database** o **canvas** → `obsidian-bases` / `json-canvas`.
- Per ricerche operative complesse multi-step su vault aperto → delega al sub-agent `vault-explorer` (quando disponibile).

## Output atteso
Sommario strutturato con:
- **Cosa ho trovato**: 1 frase di sintesi.
- **Note rilevanti**: lista di `[[wikilinks]]` con 1 riga di contesto ciascuna e path relativo `cartella/Nota.md`.
- **Citazioni dirette**: snippet `> ...` con riferimento alla nota di origine.
- **Gap / aperti**: cosa non è stato trovato o resta ambiguo.

Esempio:
```markdown
**Trovato**: 3 note su pricing Q2.

- [[Strategia-Q2-2026]] (`30-Dominio/32-Strategia-Business/`) — definisce target ARR
- [[Decisione-Pricing-Tier-Pro]] (`30-Dominio/32-Strategia-Business/`) — tier Pro a 49€/mese

> "Il pricing Pro punta al segmento mid-market con 49€/mese" — [[Decisione-Pricing-Tier-Pro]]

**Aperto**: nessuna nota copre il pricing Enterprise.
```
