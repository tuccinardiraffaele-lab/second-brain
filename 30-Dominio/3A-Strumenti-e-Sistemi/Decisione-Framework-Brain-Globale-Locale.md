---
tipo: decisione
creato: 2026-04-14
aggiornato: 2026-04-15
stato: attivo
tags:
  - strumenti/claude-code
  - strumenti/obsidian
  - decisione/architettura
  - knowledge-management
area: strumenti
---

# Decisione — Framework Brain Globale-Locale

> [!info] In una frase
> Il vault Obsidian diventa il **brain globale** che alimenta Claude Code in qualsiasi progetto, tramite un MCP server in sola lettura. Ogni progetto locale mantiene un suo `.brain/` indipendente che custodisce i dettagli tecnici. I due strati si collegano via wikilinks + regola di filing MECE.

## Contesto

Oggi il confine tra [[Strumenti-Claude-Code]] globale e vault è netto:

- `~/.claude/CLAUDE.md` → istruzioni globali (personalità, anti-overengineering)
- `~/Second Brain/CLAUDE.md` → istruzioni applicabili solo quando Claude gira *dentro* il vault
- Progetti locali (es. [[Football-Trading]], [[Sistema-Agentico-Studio]]) → non vedono nulla del vault

Il bisogno è **invertire il flusso**: il vault deve diventare fonte di verità globale, interrogabile da qualsiasi progetto, senza saturare il context window (anche con 1M token di Opus 4.6 l'approccio "carica tutto" non scala).

## Obiettivo

Dare a Claude Code, ovunque lo si apra, accesso on-demand a:

- Identità, valori, strategia, OKR (contesto sempre utile)
- Decisioni strategiche passate
- SOP generali e metodologie
- Concetti di dominio (giuridico, AI, Lean)
- Persone e relazioni

Senza:

- Caricare tutto il vault in memoria a ogni sessione
- Duplicare la stessa informazione in N repo
- Perdere il controllo sulle convenzioni di scrittura del vault

## Alternative considerate

> [!abstract] Ricerca condotta su fonti autorevoli
> Documentazione ufficiale Anthropic, engineering blogs, repo GitHub con track record verificato (>100 stelle, autori riconosciuti, manutenzione attiva). Scartati: thread social, articoli senza autore, repo abbandonati.

### A1. Static import nel CLAUDE.md globale

**Come**: `@~/Second Brain/30-Dominio/…` nel CLAUDE.md globale.
**Pro**: zero codice, funziona subito.
**Contro**: context-bloat permanente, non scala con la crescita del vault, carica tutto sempre.
**Scartata.**

### A2. SessionStart hook che inietta digest

**Come**: hook globale Python che all'avvio di ogni progetto legge N note chiave dal vault e le inietta nel context.
**Pro**: digest dinamico, possibile filtro per progetto corrente.
**Contro**: manutenzione script, context comunque caricato anche quando non serve.
**Parzialmente adottata** (il digest L0+L1 va nel CLAUDE.md globale come testo statico curato, senza bisogno dell'hook).

### A3. MCP server sul vault (lookup on-demand)

**Come**: un MCP server espone tool tipo `search_notes`, `read_note`, `recent_activity`. Claude li chiama solo quando serve.
**Pro**: zero context-bloat a priori, scala indefinitamente, agnostico rispetto all'agente (funziona anche con Codex/Gemini).
**Contro**: latenza tool call, dipendenza dal server.
**Adottata come strategia principale.**

### Implementazioni MCP-Obsidian valutate

| Repo | Stelle | Accesso | Decisione |
|---|---|---|---|
| `basicmachines-co/basic-memory` | 2.9k | FS + SQLite index | **Scelta** — multi-project nativo, non richiede Obsidian aperto, doc Claude Code dedicata |
| `cyanheads/obsidian-mcp-server` | 448 | via Local REST API plugin | Scartata — richiede Obsidian aperto |
| `StevenStavrakis/obsidian-mcp` | 677 | FS diretto | Scartata — warning "backup before use", manutenzione incerta |

### Fork di Basic Memory per imporre convenzioni custom

**Come**: fork + modifica tool di scrittura perché rispettino frontmatter e naming del vault.
**Pro**: scritture conformi alle regole del vault.
**Contro**: manutenzione continua, ogni upstream da mergiare manualmente, sforzo iniziale non banale, tempo sottratto al bet principale ([[Sistema-Agentico-Studio]]).
**Scartata** (vedi mitigazione sotto: l'Opzione "sola lettura" risolve il problema senza fork).

### Wrapper MCP custom sopra Basic Memory

**Come**: piccolo MCP server che espone solo `search`/`read` di Basic Memory e aggiunge una `write_note` custom conforme alle convenzioni del vault.
**Decisione**: **valutata ma differita**. Si costruisce solo dopo aver dimostrato che il flusso "sola lettura + skill di scrittura esistenti" lascia buchi reali.

### Pattern architetturali adottati

- **L0-L3 progressive token budgeting** (ispirato a [eugeniughelbur/obsidian-second-brain](https://github.com/eugeniughelbur/obsidian-second-brain)):
	- L0 (sempre caricato): identità + progetti attivi + North Star + valori operativi, ~200 token nel CLAUDE.md globale
	- L1 (sempre caricato): mappa curata del vault, ~300-400 token nel CLAUDE.md globale
	- L2 (on-demand): note singole lette via `read_note`
	- L3 (on-demand): espansione backlinks via `search`
- **Separazione CLAUDE.md vs knowledge base** (da Basic Memory docs): il CLAUDE.md dice *come* lavorare, il vault custodisce *cosa* sai.
- **Modello A** (brain locale indipendente): `.brain/` nel repo di ogni progetto, non sincronizzato con Obsidian. Scelta contro il Modello B (symlink/submodule verso il vault) per maggior pulizia e minor sync.

### Prior art consultato

- `breferrari/obsidian-mind` — utile per il layer hook (SessionStart/PostToolUse) che automatizza il vault. Non adottato come base ma pattern tenuto in riserva per fasi successive.
- `Giobebbe/second-brain-os-template` — utile come ispirazione per la separazione Contesto/Business/Progetti. Non adottato: è single-vault single-project, non copre il caso cross-project.

## Decisione

**Basic Memory come MCP server** che espone il vault a qualsiasi Claude Code, configurato in **sola lettura** (Opzione 1):

- Claude può chiamare `search_notes`, `read_note`, `recent_activity`, `list_directory`, `build_context`.
- Claude **non** può chiamare `write_note`, `edit_note`, `delete_note`, `move_note`.
- Tutte le scritture nel vault continuano a passare dalle skill esistenti (`/decision`, `/daily`, `/weekly`, `/sprint`, `/meeting`, `/brainstorm`, `/session-close`) che rispettano frontmatter, naming, wikilinks, callout del vault.

**Promozione dei pattern (locale → globale)** mantenuta senza scritture dirette:

1. Claude legge nota locale.
2. Cerca precedenti simili nel vault via `search_notes`.
3. Se trova ≥2 occorrenze del pattern, propone promozione in conversazione.
4. Su approvazione utente, Claude invoca la skill appropriata (`/decision` o `/sprint`) per scrivere la nota concettuale nel vault **conforme** alle regole.

Vedi [[Strumenti-Filing-Brain-Globale-Locale]] per la regola canonica di cosa va globale vs locale.

## Rischi identificati e mitigazione

> [!warning] Rischio 1 — Contaminazione frontmatter
> Basic Memory ha un suo schema frontmatter (`title`, `type`, `permalink`). Il vault usa schema custom ricco (`tipo`, `creato`, `aggiornato`, `stato`, `tags`, `area`, `progetto`). La documentazione non chiarisce se Basic Memory modifica frontmatter esistente durante la scansione iniziale.
>
> **Mitigazione**: prima dell'installazione sul vault reale → (1) test in sandbox su copia di 5 note, (2) ispezione codice sorgente Basic Memory nel punto di scrittura, (3) backup completo del vault.

> [!warning] Rischio 2 — Scritture non conformi
> Basic Memory è bidirezionale per default. Tool di scrittura automatici non seguirebbero le convenzioni del vault.
>
> **Mitigazione**: Opzione 1 (sola lettura) imposta via istruzioni esplicite nel CLAUDE.md globale. Scritture vault sempre via skill.

> [!warning] Rischio 3 — File `.base` e `.canvas` invisibili
> Gli MCP Obsidian leggono solo Markdown. Bases (cockpit, okr, filoni) e Canvas restano opachi a Claude.
>
> **Mitigazione**: accettato come limite. Query su dashboard → Claude chiede all'utente o legge le note-fonte.

> [!warning] Rischio 4 — Ricerca testuale, non semantica
> Basic Memory usa full-text search (SQLite FTS), non RAG vettoriale. Query per concetto con keyword diverse dalla nota potrebbero non trovare.
>
> **Mitigazione**: disciplina nei titoli e negli abstract delle note. RAG vettoriale valutabile in futuro se il limite si dimostra bloccante.

## Conseguenze operative

- Il CLAUDE.md globale (`~/.claude/CLAUDE.md`) viene ristrutturato secondo nuovo indice MECE (vedi [[Brain-Framework-Implementazione]] per indice completo e stato di implementazione).
- Ogni progetto locale ottiene una cartella `.brain/` con struttura standard (decisions/, architecture/, debt/, sprint/, meetings/, people/).
- Ogni `CLAUDE.md` di progetto contiene un puntatore esplicito al brain locale + istruzione "per contesto strategico usa MCP Basic Memory sul vault".
- La skill `/weekly` viene estesa con scansione pattern-promotion sui `.brain/` della settimana.

## Decisioni che restano da prendere

- Soglia promozione: fissata a **≥2 occorrenze** (un pattern dimostrato, non ipotizzato).
- Meccanismo 2 (scansione periodica) agganciato a **/weekly** esistente, non skill separata.
- Path dei repo dei progetti: da definire (probabilmente `~/projects/<nome>/`).



## Aggiornamento 2026-04-15 — Step C chiuso

Il framework è ora **operativo a livello di pipeline**:
- **Step A** (2026-04-15): Basic Memory MCP installato sul vault con hardening completo (config `ensure_frontmatter_on_sync: false`, `disable_permalinks: true`, `auto_update: false`; deny-rules in `settings.json` su tutti i tool di scrittura MCP). Vedi [[Decisione-Hardening-Basic-Memory]].
- **Step B** (2026-04-15): scaffold `.brain/{architecture,state,decisions,debug,metrics,planning}/` creato su `~/projects/ai-football-trading/` (commit `2fa13b7`). CLAUDE.md di progetto esteso con 5 regole operative. Hook `vault-write-guard.sh` esteso a pattern `*/.brain/*`.
- **Step C** (2026-04-15): `~/.claude/CLAUDE.md` globale riscritto a 13 sezioni. Skill `iterate` creata per assorbire il ciclo iterativo execute→review→decisione. 2 regole di design nuove integrate: [[Decisione-Lookup-MCP-Scoped-Semantico]] + [[Decisione-Stile-Tecnico-Effetto-Prodotto]].

**Risultato parziale**: inventario empirico 2026-04-15 ha rivelato che il vault e i `.brain/` sono ancora **sotto-popolati** (6 aree dominio vuote, `40-Conoscenza/` intera vuota, `.brain/` FT a 0 note, AIOS senza brain locale). La pipeline risponde ma non ha ancora materiale sufficiente per domande ICP/value-prop oltre le 2 MOC di progetto.

**Azione corrente**: Roadmap a 7 punti post-Step C in [[Brain-Framework-Implementazione]]. Priorità #1 = interview del vault post-esame studio giuridico 2026-04-17.

## Collegamenti

- [[Strumenti-Filing-Brain-Globale-Locale]] — regola canonica di filing
- [[Brain-Framework-Implementazione]] — roadmap e stato di implementazione
- [[Identità]] · [[Valori-Fondamentali]] · [[Strategia-Attuale]]
- [[Sistema-Agentico-Studio]] · [[Football-Trading]]
- [[Troubleshooting-UPS-Coding]] — meta-processo affine (altra metodologia del knowledge system)
