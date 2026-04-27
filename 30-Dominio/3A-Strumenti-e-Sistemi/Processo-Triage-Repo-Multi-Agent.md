---
tipo: processo
creato: 2026-04-27
aggiornato: 2026-04-27
stato: attivo
tags:
  - processo/triage
  - strumenti/claude-code
  - metodo/multi-agent
area: strumenti
---

# Triage repo via pipeline multi-agent

> [!info] In una frase
> Pipeline a 4 fasi (5 Explore sonnet → 1 fact-check Opus → 3 dibattitori paralleli + 1 orchestratore Opus → esecuzione user-approved in batch revertibili) per triagiare un repo disordinato e categorizzare ogni file in `DELETE` / `KEEP-OUT` / `MOVE-IN`, garantendo zero orfani e MECE rispetto alla tassonomia target.

## Quando si usa

- Repo con **legacy directory** parallela al brain locale (es. `.knowledge/`, `.notes/`, `docs/scratch/`) accumulata nel tempo
- Brain locale già **strutturato con tassonomia** (Pattern A/B/C/D/E) ma esterno disordinato
- Necessità di **triage file-by-file** con criterio (~600+ file diventa ingestibile per un singolo agente)

## Architettura della pipeline

```
[5 Explore agents — sonnet]    →    [1 fact-check — opus]    →    [Room dibattito — 4 opus]    →    [User approval]    →    [Esecuzione 6 batch]
   triage in 5 territori MECE      consistenza + naming         orchestratore + 3 dibattitori    AskUserQuestion        commit revertibili
```

### Fase 1 — 5 Explore agents (sonnet) in parallelo

Ogni agente riceve un **territorio MECE**:
1. Knowledge legacy (`.knowledge/**`)
2. Documentazione canonica + entrypoint (`docs/**`, `README.md`, `CLAUDE.md`, `.github/**`, `.vscode/**`)
3. Code core business (`services/**`, `packages/**`, `agents/**`)
4. Code support (`tests/**`, `scripts/**`, build files)
5. Infra/ops/config (`infrastructure/**`, `deployment/**`, `configs/**`, `data/**`, `.gitignore`, `.env`)

Output uniforme: tabella `| path | categoria | rationale | dest_path_brain | wikilinks_bidir | naming_check |`. Sotto: "Open questions" max 5.

### Fase 2 — Fact-check (1 Opus)

Riceve i 5 output concatenati. Verifica:
- **Consistency** cross-territori (file in più territori? categorizzazioni contraddittorie?)
- **Naming** (Pattern A/B/C/D/E, Kebab-Case, prefissi canonici nelle cartelle giuste)
- **Wikilink reciprocity** (ogni MOVE-IN ha nota esistente che lo dovrà linkare?)
- **Anti-duplicato** (contenuto già in `.brain/`?)
- Marca `⚠ DEBATE-NEEDED` ogni caso ambiguo

### Fase 3 — Room di dibattito (4 Opus)

3 dibattitori in parallelo con **bias divergenti dichiarati**:
- **A — Conservatore**: bias verso preservare info, contrario a DELETE
- **B — Minimalista anti-debt**: applica anti-overengineering globale, contrario a MOVE-IN inutili
- **C — Architetto tassonomia**: MECE, naming, wikilink reciprocity

Poi 1 **orchestratore Opus** sintetizza i 3 output e dichiara `VERDETTO` per ogni caso, con regole:
1. Convergenza ≥2 voci con minoritario debole → maggioranza
2. Argomento più solido (Pattern citato, file letto, vincolo CLAUDE.md) → vince
3. Verifica file richiesta → `VERIFICA-REQUIRED`, esecutore umano completa

### Fase 4 — Verifiche finali (user)

L'orchestratore segnala N casi `VERIFICA-REQUIRED`. Esecutore umano legge i file specifici (~30-60 min) per chiudere i debate residui.

### Fase 5 — Manifesto + approvazione

Output finale: 5 sezioni (DELETE, MOVE-IN, KEEP-OUT con wikilink, Note brain da creare, Bug repo paralleli). User approva.

### Fase 6 — Esecuzione in batch revertibili

Sequenza canonica:
1. **DELETE** (più sicuro, revertibile via `git revert`)
2. **Bug fix** repo paralleli
3. **Wikilinks** in note brain esistenti + creazione note nuove
4. **MOVE-IN** in lotti per cartella source
5. **Cleanup** finale legacy directory
6. **Verifica** zero orfani via tooling permanente (vedi [[Strumenti-Check-Orphan-Wikilinks]])

Ogni batch un commit separato con messaggio descrittivo.

## Vincoli operativi non negoziabili

- **Niente sycophancy** in tutta la pipeline (regola §5bis del CLAUDE.md globale): i dibattitori devono difendere la loro angolatura anche contro maggioranza, l'orchestratore deve segnalare verifica invece di indovinare.
- **Sola lettura** per Explore + fact-check + room: nessuna modifica file durante deliberazione.
- **Skill canoniche path-based** per tutte le scritture su `.brain/**` o `~/Second Brain/**` (vedi [[Strumenti-Filing-Brain-Globale-Locale]]).

## Trade-off osservati

- **Pro**: scalabile a repo grandi (641 file in una sessione), produce manifesto verificabile, batch revertibili annullano errori a costo basso.
- **Contro**: costoso in token (~3-5 Opus + 5 Sonnet); l'orchestratore può allucinare nomi specifici se non vede il file (esempio osservato: "Pattern-Matrix-Brain" inventato in D1, corretto in fase 5 via lettura diretta).

## Quando NON usare

- Repo piccolo (<50 file fuori dal brain): più economico fare triage manuale.
- Brain locale ancora non strutturato: prima definire tassonomia, poi triagiare.
- Modifiche non-strutturali (refactor, feature): non è uno strumento di sviluppo, è di archiviazione/filing.

## Prima applicazione

AIOS Studio, 2026-04-27 — vedi [[Diario-2026-04-27]] sezione triage e relativo log nel `.brain/` locale del progetto.

## Note collegate

- [[Strumenti-Filing-Brain-Globale-Locale]] — la regola MECE che la pipeline applica
- [[Strumenti-Check-Orphan-Wikilinks]] — il guardrail anti-regressione installato a fine pipeline
- [[Sistema-Agentico-Studio]] — primo progetto su cui è stato applicato
- [[Processo-Knowledge-Management-Coding]] — quadro IWS in cui si inserisce
