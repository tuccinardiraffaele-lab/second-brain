---
tipo: progetto
creato: 2026-04-14
aggiornato: 2026-04-26
stato: attivo
tags:
  - iniziativa/strumenti
  - claude-code
  - knowledge-management
  - roadmap
area: strumenti
---

# Brain Framework — Implementazione

> [!info] In una frase
> Roadmap operativa per implementare il framework "brain globale + brain locale" per Claude Code, deciso il 2026-04-14 (vedi [[Decisione-Framework-Brain-Globale-Locale]]).

## Stato

**Step A, B e C completati** (2026-04-15). Framework brain globale + locale operativo. Popolamento iper-preciso delle cartelle di dominio rinviato (vedi Follow-up in fondo).

## Obiettivo

Portare in produzione il framework entro tempi compatibili con il go-live [[Sistema-Agentico-Studio]] (~10 maggio 2026) senza sottrarre tempo critico al bet principale. L'implementazione deve essere **leggera e iterativa**: step piccoli, testabili, reversibili.

## Roadmap — 3 Step sequenziali

### Step A — Setup Basic Memory MCP sul vault

**Obiettivo**: avere Basic Memory installato, configurato sul vault in sola lettura, agganciato a Claude Code globale.

**Stato**: ✅ completato 2026-04-15 (test end-to-end cross-progetto da verificare al prossimo restart Claude Code).

**Sotto-task**:
- [x] Verificato `uv` 0.11.2 presente su WSL
- [x] Path con spazio `~/Second Brain/` gestito correttamente da Basic Memory (nome file con accenti inclusi)
- [x] Mitigazione Rischio 1 (frontmatter): sandbox test su 5 note → vedi [[Decisione-Hardening-Basic-Memory]]
- [x] Mitigazione Rischio 1: ispezione codice via sandbox (più efficace che riga-per-riga)
- [x] Backup vault pre-BM in `~/backups/vault-2026-04-15-pre-bm.tar.gz`
- [x] `uv tool install basic-memory` → v0.20.3
- [x] Progetto `key-path` registrato in `~/.basic-memory/config.json` puntato al vault
- [x] Reindex completo: 52 entities embedded, 20/20 sample hash invariati
- [x] MCP server registrato scope user: `claude mcp add basic-memory --scope user -- basic-memory mcp`
- [x] Deny-rules in `~/.claude/settings.json` per `write_note`, `edit_note`, `delete_note`, `move_note`, `canvas`, `project_management`
- [x] **Test end-to-end** (2026-04-15): `search_notes "identità"` da progetto esterno → 10 risultati pertinenti. `mcp__basic-memory__write_note` non esposto a Claude in sessione esterna (deny-rule lavora a livello di esposizione tool, non solo permission check).

**Criterio di successo**: da `~/projects/<qualsiasi>/`, Claude Code può chiamare `read_note("Valori-fondamentali")` via MCP e restituirmi il contenuto senza averlo caricato nel CLAUDE.md.

> [!warning] Follow-up aperti (non bloccanti)
> - **Delta file filesystem vs indicizzati — chiuso 2026-04-15**: 71 `.md` nel vault, 50 `.md` + 3 `.base` indicizzati da BM. I 21 non indicizzati sono tutti dentro `.claude/` (20 skill-file + 1 agent-file): BM esclude i dotfolder per default, è il comportamento corretto — sono istruzioni framework Claude Code, non contenuto second brain.
> - **Cleanup completato 2026-04-15**: backup pre-BM rimosso (test e2e OK), progetto BM residuo `main` rimosso dal config (resta solo `key-path` default). Sandbox `/tmp/bm-sandbox/` rimosso (sia dir che progetto BM).

### Step B — Struttura `.brain/` di prova su Football Trading

**Obiettivo**: creare la prima istanza di brain locale in un repo reale per validare la struttura.

**Stato**: ✅ completato 2026-04-15. Scaffold vuoto committato in `~/projects/ai-football-trading/` (commit `2fa13b7`), test end-to-end passato (Claude Code nel repo legge `MAP.md` e pesca dal vault via MCP). Popolamento iper-preciso rinviato alle prossime sessioni.

**Sotto-task**:
- [x] Scelto repo: `~/projects/ai-football-trading/` (committato 2fa13b7)
- [x] Creata struttura cartelle (MECE rivista in sessione con founder): `.brain/{architecture,state,decisions,debug,metrics,planning}/`. Cartelle `debt/sprint/meetings/people/` escluse in favore di tipologie emerse dai buchi reali di sessione (feature fantasma, deriva storica, perimetro incompleto, metriche complete).
- [ ] Definire template frontmatter minimo per ciascuna tipologia → rinviato al popolamento iper-preciso
- [x] Creato `.brain/MAP.md` **curato a mano** (analogo L1 a scala repo)
- [x] `CLAUDE.md` di progetto esteso (non sovrascritto): aggiunta sezione *Brain locale e vault globale* con 5 regole operative (planning persistente via ExitPlanMode, lookup vault via MCP, feature-level vs code-level, stato vs codice, perimetro completo)
- [ ] Migrare 2-3 note tecniche dal vault al `.brain/` → **skippato**: popolamento iper-preciso nelle prossime sessioni, migrazioni cieche rischiano di rompere `.base`/wikilinks
- [x] MOC globale `Football Trading.md` verificata: livello business OK (menzioni tecniche pertinenti al racconto prodotto, non estraibili)
- [x] Aggiunti `repo_path: ~/projects/ai-football-trading` e `brain_path: ~/projects/ai-football-trading/.brain` al frontmatter della MOC
- [x] Hook `~/.claude/hooks/vault-write-guard.sh` esteso a pattern `*/.brain/*`. CLAUDE.md globale aggiornato per riflettere la regola path-based estesa ai brain locali.

**Criterio di successo**: apro Claude Code in `~/projects/football-trading/`. Claude vede il `CLAUDE.md` di progetto, legge `.brain/MAP.md`, risponde a "cosa abbiamo deciso sul broker" pescando dal `.brain/decisions/`.

### Step C — Stesura nuovo `~/.claude/CLAUDE.md`

**Obiettivo**: riscrivere il CLAUDE.md globale secondo il nuovo indice MECE, preservando tutto ciò che di buono c'è oggi.

**Stato**: ✅ completato 2026-04-15. CLAUDE.md globale sostituito (backup in `~/.claude/CLAUDE.md.bak-20260415-190109`). Skill `iterate` creata in `~/.claude/skills/iterate/SKILL.md` per assorbire il workflow del ciclo iterativo. Slash command `~/.claude/commands/iterate.md` ridotto a thin wrapper sulla skill. Review blocco-per-blocco eseguita con il founder.

#### Indice del nuovo CLAUDE.md globale (13 sezioni)

| # | Sezione | Fonte / Natura |
|---|---|---|
| 1 | **Chi sono** | fusione di profilo utente esistente + L0 nuovo (identità + preferenze interazione) |
| 2 | **Mappa del vault (L1)** | nuova — hub curati con 1 riga di descrizione |
| 3 | **Memoria vault — lookup MCP** | nuova — quando/come interrogare Basic Memory |
| 4 | **Filing globale vs locale** | nuova — regola canonica + promozione autonoma (rimando a [[Strumenti-Filing-Brain-Globale-Locale]]) |
| 5 | **Stile di comunicazione** | fusione di 3 blocchi: stile risposte esistente + segnalazioni tecniche non-tecniche + effetto sul prodotto |
| 6 | **Anti-overengineering** | invariato |
| 7 | **Quando hai dubbi** | invariato |
| 8 | **Sicurezza** | invariato |
| 9 | **Sandbox bash** | invariato |
| 10 | **Workflow** | ridotto: solo regola piano 3-5 punti + rimando a skill UPS per diagnosi fallimenti. Regola "niente celebrazione finale" assorbita in Stile di comunicazione |
| 11 | **Troubleshooting UPS** | invariato (rimando alla skill) |
| 12 | **Ciclo iterativo execute → review → decisione** | ridotto a rimando alla skill `/iterate`, con solo il principio-cardine "non auto-approvarti mai" mantenuto inline |
| 13 | **Esclusioni per vault Obsidian** | invariato + chiarimento: la regola di filing si applica anche dentro il vault (è organizzazione della conoscenza, non regola di codice) |

**Sezione eliminata**: "Scelta del modello" (Sonnet vs Opus).

**Sotto-task**:
- [x] Scrivere il blocco L0 (Chi sono — identità operativa) — ~200 token
- [x] Scrivere il blocco L1 (Mappa del vault) — ~300-400 token, hub curati a mano
- [x] Scrivere blocco "Memoria vault — lookup MCP" (regole quando/come chiamare)
- [x] Scrivere blocco "Filing globale vs locale" (sintesi + rimando a [[Strumenti-Filing-Brain-Globale-Locale]])
- [x] Scrivere blocco "Stile di comunicazione" completo (generale + segnalazioni tecniche + effetto prodotto)
- [x] Ridurre sezione "Workflow" (mantenere solo regola 1, sostituire regola 2 con rimando UPS, eliminare regola 3)
- [x] Ridurre sezione "Ciclo iterativo" a rimando skill `/iterate` + principio "non auto-approvarti"
- [x] Estendere "Esclusioni vault Obsidian" con il chiarimento sul filing
- [x] Eliminare sezione "Scelta del modello"
- [x] Review finale di tutto il CLAUDE.md per verificare MECE reale e assenza di contraddizioni

**Criterio di successo**: il nuovo CLAUDE.md globale pesa ~800-1000 token totali di contenuto nuovo, non contraddice le sezioni mantenute, e fornisce a Claude tutto il necessario per operare con il brain globale+locale.

## Mitigazioni cross-step

> [!warning] Prima dell'installazione Basic Memory sul vault reale
> Le 3 mosse di mitigazione Rischio 1 (test sandbox + ispezione codice + backup) vanno fatte **prima** di puntare Basic Memory al vault vero. Non negoziabili.

> [!warning] Durante Step B
> Se la migrazione di note tecniche esistenti dal vault al `.brain/` rischia di rompere `.base` o wikilinks esistenti, **rimandare la migrazione** e iniziare il `.brain/` solo con note nuove. La migrazione massiva può essere una fase separata, non bloccante.

> [!warning] Durante Step C
> Il CLAUDE.md attuale contiene regole testate. Non sostituire brutalmente: scrivere il nuovo in un file temporaneo, fare un diff con il vecchio, validare blocco per blocco che nulla di valore si perde.

## Domande aperte

> [!question] Da risolvere strada facendo
> - Dove vive il repo `.brain/` di Football Trading? Path esatto da confermare.
> - Il CLAUDE.md di progetto va committato nel repo o resta locale? (Probabile committato, ma da confermare.)
> - Come si gestisce il caso "lavoro sul laptop A, devo clonare su laptop B": il vault è su WSL, il repo va su GitHub, il `.brain/` viaggia col repo — ma il vault no. Scenario cross-macchina è marginale oggi.

## Next action immediata (prossima sessione)

**Popolamento cartelle di dominio**: via skill `/interview`, strutturare la conoscenza attuale in `30-Dominio/33-Prodotto-e-Tecnologia/`, `30-Dominio/36-Vendite-e-Crescita/` e `30-Dominio/39-Relazioni-e-Network/` (oggi quasi vuote, inserite come pointer anticipato nella mappa L1 del CLAUDE.md). Si sblocca dopo l'esame studio giuridico del 2026-04-17.




## Roadmap per funzionamento pieno (post-Step C)

Step A/B/C chiusi = **pipeline funzionante**. Per arrivare a **risultato funzionante** (Claude da un progetto risponde davvero alle domande ICP/value-prop/feature pescando dal vault e dal brain locale, invece di "cartella vuota"), restano 7 attività ordinate per priorità. Definite il 2026-04-15 dopo inventario empirico del vault e dei repo.

### 1. Interview del vault

Via skill `/interview`, popolare le aree di conoscenza oggi vuote o sotto-popolate:
- `30-Dominio/33-Prodotto-e-Tecnologia/` (2 note)
- `30-Dominio/34-Persone-e-Leadership/` (0)
- `30-Dominio/35-Finanza/` (0 — critica per un futuro consulente del lavoro)
- `30-Dominio/36-Vendite-e-Crescita/` (0)
- `30-Dominio/37-Operazioni/` (2 note)
- `30-Dominio/38-Crescita-Personale/` (0)
- `30-Dominio/39-Relazioni-e-Network/` (0)
- `40-Conoscenza/` (cartella intera vuota: concetti, fonti, mappe, persone)
- `20-Iniziative/♻️-Ricorrenti/` (0 — nessun processo ciclico catturato: daily/weekly/monthly review, studio giuridico, ecc.)

Sblocco: post-esame studio giuridico 2026-04-17.

> [!success] Stato 2026-04-26 — chiuso
> Punto chiuso. **5/9 aree mappate via `/interview`** (`33`, `35`, `36`, `37`, `38`); **3 aree popolate per assorbimento** dal lavoro pillar (`39` via [[Relazioni-Pillar-Network-Target]] + [[Relazioni-Network-Mappa-Bootstrap]]; `40-Conoscenza` via 8 note di concetti/entità accumulate; `33` arricchito da [[Prodotto-Pillar-Delivery-Piloti]] + [[Decisione-Soglie-Pilot-AIOS]]).
>
> Aree residue (`34-Persone-e-Leadership`, `♻️-Ricorrenti`): non più presidiate via `/interview` dedicata — verranno popolate **per assorbimento** nel proseguo del lavoro sui pillar (es. `34` quando si aprirà la deputazione esterna in Stability del pillar Leadership Strategica; `♻️-Ricorrenti` man mano che le review periodiche e i sistemi canonici della mappa pillar↔sistemi maturano).
>
> Il punto 1 di questo framework è quindi **chiuso**: cessato il bisogno di sessioni `/interview` dedicate al vault globale come work-stream autonomo.

### 2. Spezzare le 2 MOC di progetto in note atomiche

Oggi [[Sistema-Agentico-Studio]] (186 righe) e [[Football-Trading]] (197 righe) sono **monolitiche**: contengono ICP, value-prop, pricing, pain point, roadmap, rischi in un unico file. Il grafo wikilink non è navigabile — da progetto Claude può solo caricare la MOC intera (anti-scoping rispetto alla regola della sezione 3 del CLAUDE.md globale).

Estrarre note atomiche per aspetto (es. `AIOS-ICP-Studi-Medio-Piccoli.md`, `AIOS-Pricing-Strategia.md`, `FT-Pain-Point-Retail.md`) linkate dalla MOC. La MOC diventa hub navigabile, non contenitore.

> [!success] Stato 2026-04-26 — chiuso
> Split eseguito: **8 note atomiche AIOS** + **8 note atomiche FT** create con frontmatter pillar-allocato. Le due MOC ridotte da 217/215 → 88/83 righe, mantengono `tipo: progetto` (per `cockpit.base`), `repo_path`/`brain_path`, hub navigabile, stato vivo, log sessioni, debito tecnico, loss chiuse. Pulizia stato bug FT (tutti chiusi) + `prossima_azione` aggiornata a "fase di apprendimento — accumulo trades paper mode per training modelli". Wikilink section-level entranti riparati (3 occorrenze).

### 3. Revisione skill e scaffold Claude Code globale

> [!success] Stato 2026-04-26 — chiuso (round 1)
> Audit eseguito non come check semantico tradizionale ma come **misurazione skill-creator 2.0** (skill-creator ufficiale Anthropic, plugin già installato). Setup pipeline `~/.claude/evals/` con eval-set (routing trigger) + rubric (output quality) + wrapper `bin/run-eval-isolated.sh` (swap-and-restore per non collidere con skill globali esposte al sub-claude). Round 1 chiuso su **5 skill globali** (`troubleshooting-ups`, `iterate`, `quality-pillar`, `sprint` + `dashboard` esclusa) e **pilota cluster A vault** (`brainstorm`). Verdetti: tutte **HOLD** — il loop di tuning automatico non batte la baseline con `--max-iterations 2 --runs-per-query 1`. Pattern: description già robuste, noise stocastico domina con quei parametri.
> 
> **Integrazione Review Cadence (Fase 3)**: `weekly/SKILL.md` aggiornato con blocco "Skill globali — check re-eval" (cadenza settimanale, scan modifiche `~/.claude/skills/` ultimi 7gg + check uscita nuovo modello), `monthly/SKILL.md` con "Blocco 5ter — outgrowth check >60gg".
> 
> **7 loop vault residui sospesi**: artefatti pronti (eval-set + rubric committati in `~/.claude/evals/`) per `daily`, `decision`, `session-close`, `meeting`, `weekly`, `interview`, `monthly`. Lancio spalmato su weekend successivi per non saturare la finestra Max. Round 2 (`--max-iterations 5 --runs-per-query 3`, ~7-8× più chiamate `claude -p`) post go-live AIOS 2026-05-10.

Audit di `~/.claude/` (skill, agents, commands, hooks, settings). Verifiche:
- Le skill esistenti sono ancora coerenti con il CLAUDE.md globale riscritto?
- Ci sono duplicazioni o sovrapposizioni tra skill?
- Hook e `settings.json` riflettono lo stato attuale (deny-rules MCP Basic Memory, `vault-write-guard` esteso a `.brain/`)?
- Skill mancanti emerse dall'uso?

### 4. Revisione artefatti e file della repo globale `~/.claude/`

Pulizia strutturale: backup vecchi, file temporanei, hook orfani, documentazione disallineata. Complementare al punto 3 (che è semantico): questo è igiene.

### 5. Brainstorming + seed `.brain/` di Football Trading

Prima un brainstorming mirato per catturare esigenze business/corporate/strategiche del progetto, poi popolare le 6 cartelle `.brain/{architecture,state,decisions,debug,metrics,planning}/` con 2-3 note reali per cartella, estratte dal codice e dalla storia del progetto. Oggi lo scaffold è vuoto → lookup locale da `ai-football-trading/` restituisce nulla.

### 6. Review `.brain/MAP.md`

Rivedere il MAP.md di Football Trading, oggi curato a mano. Capire se ha senso mantenerlo manuale o se va generato/aggiornato automaticamente (es. script che scansiona `.brain/`). Decisione dipende dal tasso di crescita del brain locale.

### 7. Completare AIOS Studio al pari di Football Trading

> [!warning] Priorità rivista 2026-04-15 — anticipato a "in questi giorni"
> Originariamente in fondo (post-go-live) per non sottrarre tempo a Phase 10 GBSoftware. Revisione presa nel brainstorming [[AIOS-Brainstorm-Audit-Primitive-Agentiche]]: il punto 7 è anticipato perché la nota di audit primitive agentiche va agganciata al seed `.brain/architecture/` AIOS, non rinviata a Phase 11 (che resta solo feature di prodotto).
>
> **Budget duro**: max 3h totali (scaffold minimo + seed essenziale, no popolamento iper-preciso). Oltre la soglia, si rivaluta per non erodere Phase 10 GBSoftware.

- Scaffold `.brain/` in `~/projects/AIOS Studio/` (già presente: `.brain/` con 9 cartelle + `.knowledge/` con 5 — verificare allineamento col pattern canonico `architecture/state/decisions/debug/metrics/planning` di FT).
- Frontmatter `repo_path` + `brain_path` in [[Sistema-Agentico-Studio]] (oggi assenti — disallineato vs FT).
- Seed iniziale 2-3 note per cartella.
- **Seed `.brain/architecture/Audit-Primitive-Agentiche-AIOS.md`** con tabella ~12 primitive agentiche (Supervisor, sub-agent, skill-as-procedure, hook/guardrail, MCP/tool frontier, memoria per-cliente, memoria globale, reasoning trace, pseudonymizer, validation indipendente, human review, self-evolution governata) da compilare a giugno post-stabilizzazione go-live.
- `CLAUDE.md` di progetto con le 5 regole operative già applicate a FT.

## Collegamenti

- [[Decisione-Framework-Brain-Globale-Locale]] — decisione architetturale con alternative valutate
- [[Strumenti-Filing-Brain-Globale-Locale]] — regola canonica di filing
- [[Sistema-Agentico-Studio]] — bet principale da non sottrarre tempo
- [[Football-Trading]] — candidato primo brain locale di prova
- [[OKR-Correnti]] — ambiente di trade-off su tempo
- [[Dashboard]] — cockpit che andrà aggiornato quando lo stato cambia
