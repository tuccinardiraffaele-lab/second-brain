---
tipo: processo
creato: 2026-04-17
aggiornato: 2026-04-25
stato: attivo
tags:
  - processo/knowledge-management
  - pillar/leadership-strategica
  - strumenti/obsidian
  - strumenti/basic-memory
area: operazioni
---

# Cattura & Retrieval Info

> [!info] In una frase
> Sistema infrastrutturale del brain globale: garantisce che ogni insight, decisione, concetto, riferimento esterno **entri nel vault** al momento in cui emerge e sia **trovabile in contesto** quando serve, alimentando tutti i pillar senza dispersione.

## Forma canonica

| Campo | Valore |
|---|---|
| **Input** | (1) Insight/decisione/concetto emerso in conversazione o lavoro, (2) riferimento esterno (URL, fonte, persona), (3) microattività non urgente, (4) materiale di intervista o brainstorm, (5) richiesta di contesto da Claude Code o founder |
| **Output** | (a) Nota canonica nel territorio corretto del vault con frontmatter YAML + wikilinks bidirezionali; (b) risposta in contesto su richiesta retrieval (citazioni vault con path + sezione) |
| **Processo** | Tre fasi: **cattura** event-driven → **triage** in apertura sessione → **retrieval** on-demand via Basic Memory MCP con scoping CBA-first |
| **Owner operativo** | Founder (cattura), Claude Code (triage assistito + retrieval), skill di territorio (`/decision`, `/sprint`, `/meeting`, `/session-close`, `/brainstorm`, `obsidian-writer`) per promozione canonica |
| **Agganci pillar** | **P1 primario** ([[Strategia-Pillar-Leadership-Strategica]]), **S su tutti gli altri 6 pillar** ([[Prodotto-Pillar-Delivery-Piloti\|P2]], [[Vendite-Pillar-Governance-Reputazionale\|P3]], [[Vendite-Pillar-Sales-Positioning\|P4]], [[Crescita-Pillar-Studio-Giuridico\|P5]], [[Relazioni-Pillar-Network-Target\|P6]], [[Strategia-Pillar-Monitoraggio-Regolatorio\|P7]]) — perno cross-pillar simmetrico a [[Processo-Review-Cadence|Review Cadence]] |

## Origine

Il flusso `00-Inbox/` + skill di territorio + Basic Memory MCP esisteva come **somma di pratiche** già consolidate (regole in [[Naming-Convention-Vault]], strutture in `CLAUDE.md` del vault, processo MCP in `~/.claude/CLAUDE.md` sezione 3) ma **non era codificato come sistema unico** con I/O, processo, owner e agganci pillar.

Una prima fotografia descrittiva del problema era stata scritta il 2026-04-17 in questa stessa nota (sezione "Stato v0" sotto). La promozione a forma canonica è del **2026-04-25**, insieme a [[Processo-Pianificazione-Giornaliera]] e [[Processo-Validazione-Pilot]], per chiudere **HC-F4 Foundation** del pillar [[Strategia-Pillar-Leadership-Strategica]] dichiarato in [[Strategia-Mappa-Pillar-Sistemi]].

## Loss servita

> [!info] Loss primaria — #1 Finestra-competitiva-persa
> La perdita di velocità competitiva non passa solo dall'esecuzione tecnica: passa dal **costo di re-derivare** conoscenza già emersa o dalla **perdita silenziosa** di un insight strategico. Il rischio endogeno #1 in [[Strategia-Attuale#Rischi strategici]] si attenua proporzionalmente alla qualità del brain.

Loss adiacenti coperte per gli altri pillar via agganci S — ogni pillar consuma conoscenza dal vault per non re-imparare:
- **P2** — OPL/CBA del coding promosse al vault per pattern cross-progetto
- **P3, P4** — quote verbatim del padre, pain dichiarati, soglie pilot consultabili in tempo zero
- **P5** — concetti giuridici/giuslavoristici archiviati per ripasso e cross-reference
- **P6** — persone del network archiviate con segmentazione e contesto incontri
- **P7** — fonti regolatorie e segnali competitivi archiviati con datazione per trend analysis

## Architettura territoriale

> [!warning] Confine globale vs locale (regola path-based)
> Il **brain globale** vive in `~/Second Brain/`. Il **brain locale** vive in `<repo>/.brain/` di ciascun progetto. Confine in [[Filing-Brain-Globale-Locale]]: *vale solo qui = locale; vale anche altrove = globale*. Promozione automatica locale→globale sulla soglia di **≥2 occorrenze** dello stesso pattern.

Questo sistema presidia **solo il brain globale** (vault Obsidian). Il pendant per il brain locale è [[Processo-Knowledge-Management-Coding]], che opera con la stessa filosofia ma su `.brain/knowledge/` (OPL + CBA push-based).

## Il flusso a tre fasi

### Fase 1 — Cattura (event-driven)

> [!danger] Regola
> La cattura avviene **al momento in cui l'informazione emerge**, non a fine sessione. Differire = perdere.

Tre canali di ingresso:

| Canale | Quando | Destinazione |
|---|---|---|
| **Diretto in territorio** | Quando il tipo è chiaro al momento (decisione, riunione, sprint coding, riflessione giornaliera) | Skill di territorio (`/decision`, `/meeting`, `/sprint`, `/daily`, `/brainstorm`) → cartella corretta (`10/20/30/40`) |
| **Inbox** | Quando il tipo non è chiaro o serve smistare dopo | `00-Inbox/<titolo-rapido>.md` con frontmatter minimo |
| **Promozione brain locale** | Quando un pattern locale ricorre ≥2 volte tra progetti diversi | Skill `/sprint` produce nota gemella in dominio del vault |

Strumento di scrittura: **sempre via skill** (`obsidian-markdown` + skill di dominio), mai Markdown a mano. Backstop deterministico: hook `vault-write-guard.sh` blocca `Write/Edit` su path vault — l'unico tool ammesso è `Bash` heredoc/cat (la skill definisce sintassi, Bash è il tool).

### Fase 2 — Triage (apertura sessione)

> [!danger] Regola incondizionata
> Al **primo turno** di ogni sessione Claude, prima di qualunque altra risposta, controllare `00-Inbox/`. **Nessuna nota Inbox sopravvive tra sessioni**. Codificata nel callout di apertura del `CLAUDE.md` del vault.

Per ogni nota Inbox, una di quattro azioni:

| Azione | Quando | Destinazione |
|---|---|---|
| **Schedulare** | Attività con data | `10-Diario/Giornaliero/YYYY-MM-DD.md` (alimenta [[Processo-Pianificazione-Giornaliera]]) |
| **Pianificare** | Da agganciare a iniziativa | `20-Iniziative/<stato>/<progetto>/` |
| **Archiviare in dominio** | Conoscenza atemporale | `30-Dominio/<area>/` o `40-Conoscenza/` |
| **Scartare** | Capture sbagliato/duplicato | Rimozione |

### Fase 3 — Retrieval (on-demand)

> [!warning] Regola di scoping (da `~/.claude/CLAUDE.md` sezione 3)
> Non caricare interi domini. Partire da una **nota-seme** pertinente, espandere via wikilinks seguendo la **catena causale della risposta**, fermarsi sui rami "background del background". Niente filtri sintattici (tag/area/depth fisso) come stop — il criterio è semantico.

Strumenti di retrieval, in ordine:

1. **Basic Memory MCP** (sola lettura): `search_notes`, `read_note`, `build_context` per espansione grafo via wikilinks. Default per query strategiche.
2. **Skill `obsidian-reader`** in conversazione principale: per letture mirate in-context.
3. **Sub-agent `vault-explorer`**: per scansioni multi-file ampie con isolamento del contesto principale (off-loading). Le scritture dopo l'off-loading **tornano in conversazione principale** (i sub-agent non hanno accesso a `Skill`).
4. **`Glob` + `Grep` Bash** per lookup deterministici quando nome file/pattern è noto.

## Anti-pattern da evitare

- **Cattura "a fine sessione"** invece di event-driven — il dettaglio si erode in 30 minuti.
- **Memoria in testa di "cose da scrivere dopo"** — riapre il problema sostituito da [[Processo-Pianificazione-Giornaliera]].
- **Inbox come archivio permanente** — viola la regola di triage in apertura sessione, l'Inbox satura e perde funzione.
- **Markdown standard scritto a mano** in note vault (solo `#` e `[]()`) — viola la skill `obsidian-markdown`, perde wikilinks/callout/properties.
- **Caricamento di interi domini** in retrieval — viola lo scoping CBA-first, satura il contesto, riduce qualità della risposta.
- **Note senza wikilinks** — un nodo isolato è invisibile al grafo, retrieval lo perde anche se esiste.
- **Duplicazione di contenuto** invece di wikilink — viola [[Naming-Convention-Vault]] e principio MECE del vault `CLAUDE.md`.
- **Promozione locale→globale senza soglia ≥2 occorrenze** — riempie il vault di rumore di progetto.

## Health check del sistema

Coerente con [[Sistemi-Sotto-Pillar]], il sistema è "sano" se:

- ✅ **Inbox vuoto** — `00-Inbox/` vuoto a fine triage di ogni sessione (criterio binario, ground truth in `ls`).
- ✅ **Wikilinks non orfani** — ogni nota nuova ha ≥1 wikilink in entrata e ≥1 in uscita (review settimanale).
- ✅ **Frontmatter coerente** — `tipo`, `creato`, `aggiornato`, `stato`, `tags`, `area` presenti su ogni nota (validazione via `obsidian-cli` o grep).
- ✅ **Promozione locale→globale tracciata** — quando un pattern di brain locale supera ≥2 occorrenze, esiste la nota gemella nel vault wikilinkata.
- ✅ **Retrieval senza re-derivazione** — quando il founder chiede contesto strategico, Claude trova la risposta nel vault invece di re-derivarla.

Review periodica:
- **Settimanale** (in `/weekly`): scan wikilinks orfani e Inbox residuo.
- **Mensile**: scan promozioni locale→globale e duplicazioni eventuali.

## Implementazione come Skill Claude Code

Stack di skill che operano sotto questo sistema (definite globalmente in `~/.claude/skills/`):

| Skill | Fase del flusso | Funzione |
|---|---|---|
| `obsidian-markdown` | Cattura | Sintassi Obsidian (frontmatter, wikilinks, callout, embed, properties) |
| `obsidian-bases` · `json-canvas` · `obsidian-cli` | Cattura | Sintassi `.base`, `.canvas`, operazioni CLI multi-file |
| `obsidian-writer` | Cattura | Note generiche strutturate |
| `obsidian-reader` | Retrieval | Lettura mirata in-context |
| `daily` · `decision` · `meeting` · `sprint` · `weekly` · `monthly` · `brainstorm` · `interview` · `session-close` | Cattura specializzata | Skill di territorio con template e regole proprie |
| `defuddle` | Cattura da web | Estrazione markdown pulito da URL (sostituisce `WebFetch` per pagine web) |
| Sub-agent `vault-explorer` | Retrieval ampio | Off-loading di scansioni multi-file in sub-context isolato |
| Basic Memory MCP | Retrieval semantico | `search_notes`, `read_note`, `build_context`, `recent_activity` |

Backstop deterministico: hook `~/.claude/hooks/vault-write-guard.sh` blocca `Write/Edit/MultiEdit/NotebookEdit` su `~/Second Brain/**` e `**/.brain/**`. L'unico tool di scrittura ammesso è `Bash` (heredoc, cat, printf, sed). La skill **definisce la sintassi**, `Bash` **esegue la scrittura**.

## Stato v0 (sostituito il 2026-04-25)

Sezione storica — fotografia descrittiva del problema scritta il 2026-04-17, prima che il sistema fosse promosso a forma canonica.

### Stato attuale (al 2026-04-17) — sistema frammentato

| Contesto | Dove catturo | Tipo di cattura |
|---|---|---|
| Progetti personali (AIOS, FT) | File `.md` nelle cartelle progetto | Strutturata, persistente |
| Corporate ([[Angelini-Pharma]]) | Block notes fisici e digitali | Write-only — mai trasferiti altrove |
| Tutto il resto | Memoria | Volatile |

Il collo di bottiglia diagnosticato non era la cattura — era il **retrieval**: l'informazione veniva scritta da qualche parte ma non riemergeva quando serviva. Il flusso serale era *Obsidian + Claude Code → "dove eravamo rimasti?" → esecuzione*. Claude Code aveva sostituito il retrieval manuale con un retrieval conversazionale, ma il gap residuo era l'assenza di **risurfacing automatico**: l'informazione era nel vault ma doveva essere attivamente cercata.

I block notes Angelini (fisici e digitali) restano write-only per scelta — l'esperienza corporate non genera pattern trasferibili ai filoni personali.

La promozione a forma canonica del 2026-04-25 ha chiuso il gap di sistema (regole I/O+processo+owner+pillar) ma **non** il gap di risurfacing automatico — quello resta domanda aperta sotto continuous improvement del sistema.

## Collegamenti
- [[Processo-Allocazione-Conoscenza-Pillar]] — algoritmo di routing che raffina dove allocare ogni nota catturata

- [[Strategia-Mappa-Pillar-Sistemi]] — aggancio P1 primario, S su tutti gli altri 6 pillar
- [[Sistemi-Sotto-Pillar]] — forma canonica
- [[Filing-Brain-Globale-Locale]] — confine vault vs `.brain/`, regola promozione
- [[Processo-Knowledge-Management-Coding]] — pendant per il brain locale
- [[Naming-Convention-Vault]] — fonte unica di verità per naming
- [[Processo-Review-Cadence]] — review settimanale/mensile health check
- [[Processo-Pianificazione-Giornaliera]] — consumer della Fase 2 triage (schedule → diario)
- [[Strategia-Pillar-Leadership-Strategica]] — pillar primario
- [[Strumenti-Claude-Code]] — stack skill che opera il sistema
- [[Dashboard]]
