---
tipo: concetto
creato: 2026-04-15
aggiornato: 2026-04-15
stato: attivo
tags:
  - strumenti/claude-code
  - ai/agenti
area: strumenti
aliases:
  - Claude Code
  - CC
---

# Claude Code

> [!info] In una frase
> CLI agentico di Anthropic che uso come **cervello operativo** del mio setup: vive in `~/.claude/`, legge il vault come conoscenza di lungo periodo via [[Decisione-Framework-Brain-Globale-Locale|Basic Memory MCP]], e opera nei repo locali tramite brain locali `.brain/`.

## Come ci sono arrivato

Primo utilizzo: **sistema di sub-agenti per l'implementazione del codice in [[Sistema-Agentico-Studio|AIOS Studio]]**. Venivo da **Codex di OpenAI** e non ero soddisfatto.

Il click — due cose concrete:

- **Contesto consumato molto più lentamente.** Le sessioni durano, non devo ricominciare ogni poco.
- **Sub-agenti nativi + orchestrazione end-to-end.** Con Codex dovevo frammentare i task a mano fino al livello microtask per arrivare al risultato. Con Claude Code basta una **pianificazione dettagliata della feature**: lui orchestra l'implementazione dal piano fino al codice funzionante.

Il valore non è "scrive codice", è che **toglie il costo cognitivo della frammentazione**. In termini di [[Valori-Fondamentali]]: è l'unico strumento testato finora che moltiplica velocità × efficacia senza costringermi a fare da traffic controller.

## Dove lo uso oggi

Tre territori distinti:

1. **Vault Obsidian** (`~/Second Brain/`) — scrittura strutturata di identità, strategia, decisioni, processi. Sintassi via skill `obsidian-markdown`, scrittura via `Bash` (vedi [[Decisione-Paracadute-Vault-Write-Guard]]).
2. **Repo di progetto** — [[Sistema-Agentico-Studio|AIOS Studio]] e [[Football-Trading]]: coding, debug, refactor, sprint con brain locale `.brain/`.
3. **Meta-livello** — manutenzione dello stesso framework Claude Code (skill, hook, settings, CLAUDE.md globale).

## Pattern da migliorare

Due bug ricorrenti emersi dal brainstorming del 2026-04-15.

### Bug 1 — Fix miopi multi-sessione su Football Trading (pre-UPS, da rivalidare)

Pattern osservato in sessioni di debug FT **prima** dell'adozione della skill `troubleshooting-ups` (2026-04-14): un bug richiedeva più sessioni per chiudersi, i fix introducevano regressioni. Si patchava il sintomo invece di risalire alla causa radice.

**Stato**: **non validato post-UPS**. Dall'introduzione della skill non è ancora stato fatto un run di debug su FT — prima finestra utile: 2026-04-17 sera (Serie A). Rivalutare il pattern dopo quella sessione: se UPS si attiva correttamente e i fix vanno alla radice, il bug è risolto; se persiste, si apre thread diagnostico dedicato.

### Bug 2 — Assumo l'intento su task a scope largo

Esempio diagnostico: chiedo a Claude di "pulire i segnali in DB e Redis" nella pipeline FT. Dopo l'esecuzione trovo sempre segnali appesi al restart. Tre ipotesi indistinguibili: prompt incompleto, Claude ha dimenticato un posto, bug del sistema. Zero chiusura del loop.

**Stato**: **fixato il 2026-04-15** estendendo `~/.claude/CLAUDE.md` sezione 10 (Workflow) con la regola per operazioni a scope largo/distruttive — enumerazione del perimetro prima, evidenza con conteggi dopo. Da verificare nelle prossime sessioni di cleanup.

## Architettura attuale

### Framework `~/.claude/` globale

- `CLAUDE.md` — istruzioni globali utente a **13 sezioni MECE** (identità, mappa vault L1, memoria MCP, filing globale/locale, stile, anti-overengineering, sicurezza, sandbox bash, workflow, UPS, iterate, esclusioni vault).
- `skills/` — procedure riutilizzabili caricate on-demand. Regola: fatti identitari → `CLAUDE.md`; procedure → skill (vedi [[Decisione-Skill-vs-CLAUDE-md]]).
- `hooks/` — paracadute deterministici: `vault-write-guard.sh`, `block-sensitive.sh`, `user-prompt-guard.sh`, `config-change-guard.sh`.
- `settings.json` — permissions, hook, sandbox bash, deny-rules MCP.

### Brain globale ↔ brain locale

Modello A (brain locale `.brain/` indipendente per repo, non sincronizzato con Obsidian) + **Basic Memory MCP** sul vault in sola lettura. Regola di filing: *"vale solo qui / vale anche altrove"* — astrazione trasferibile nel vault, dettaglio implementativo nel `.brain/`. Vedi [[Strumenti-Filing-Brain-Globale-Locale]].

### Lookup vault

Via Basic Memory MCP, **scoping semantico via grafo wikilink** — stop su "background del background", niente filtri sintattici (tag/area/depth fisso). Vedi [[Decisione-Lookup-MCP-Scoped-Semantico]].

### Stile di lavoro

Ogni cambio tecnico tradotto in **effetto sull'utilizzatore finale**: *"se modifico X, il prodotto passa da A a B"*. Vedi [[Decisione-Stile-Tecnico-Effetto-Prodotto]].

## Hub — note collegate

### Decisioni architetturali

- [[Decisione-Framework-Brain-Globale-Locale]] — scelta Modello A + Basic Memory MCP
- [[Decisione-Paracadute-Vault-Write-Guard]] — hook PreToolUse per scritture vault/brain
- [[Decisione-Skill-vs-CLAUDE-md]] — quando skill, quando CLAUDE.md
- [[Decisione-Hardening-Basic-Memory]] — config flag per preservare byte-identity note
- [[Decisione-Lookup-MCP-Scoped-Semantico]] — scoping via grafo, non sintassi
- [[Decisione-Stile-Tecnico-Effetto-Prodotto]] — forma canonica spiegazione
- [[Decisione-Adozione-UPS-Coding]] — metodo di troubleshooting evidence-based

### Framework e processi

- [[Strumenti-Filing-Brain-Globale-Locale]] — regola canonica di filing + promozione pattern
- [[Brain-Framework-Implementazione]] — roadmap 3 step (A/B/C chiusi) + 7 punti post-Step C
- [[Troubleshooting-UPS-Coding]] — metodo UPS nel codice (skill `troubleshooting-ups`)

### Identità e strategia

- [[Identità]] · [[Valori-Fondamentali]] · [[Strategia-Attuale]]
