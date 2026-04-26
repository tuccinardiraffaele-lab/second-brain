---
tipo: decisione
creato: 2026-04-15
aggiornato: 2026-04-15
stato: attivo
tags:
  - strumenti/claude-code
  - strumenti/basic-memory
  - knowledge-management
  - decisione/architettura
area: strumenti
---

# Decisione — Lookup MCP con scoping semantico via grafo

> [!info] In una frase
> Il lookup del vault via Basic Memory MCP è **sempre attivo ma mai totale**: si espande sul grafo wikilink seguendo la **catena causale della risposta** alla query specifica, e si ferma quando il nodo successivo è "background del background". Il criterio di stop è **semantico**, non sintattico.

## Contesto

Con la chiusura di Step B del framework brain (2026-04-15), Basic Memory MCP è installato sul vault in sola lettura ed esposto globalmente a Claude Code. La domanda aperta nello Step C era: **quando Claude da una cwd esterna al vault ha bisogno di contesto business, quanta memoria deve caricare?**

Due estremi entrambi sbagliati:
- **Troppo poco**: carica solo una singola nota → risposta amputata, la catena causale completa non viene restituita.
- **Troppo**: carica l'intero dominio di progetto → scoping fallisce, il contesto è rumoroso, i token esplodono.

Il caso d'uso che ha chiarito il problema: query *"descrivi come viene costruito il modello XGBoost in Football Trading"*. Risposta corretta: snapshot temporali live (XGBoost online) + retraining offline + come tutto converge nel `context_threshold_filter` usato durante il trading. Ma `context_threshold_filter` vive sotto il signal-agent, non sotto XGBoost. Un filtro sintattico (tag/area) avrebbe tagliato via un pezzo **necessario** della risposta.

## Decisione

Regola operativa integrata nella **sezione 3** del CLAUDE.md globale:

1. **Parti da una nota-seme** pertinente alla query (`search_notes` se il nome non è noto, `read_note` se lo è).
2. **Espandi il grafo** via `build_context` seguendo i wikilinks.
3. **Dopo ogni hop**, prima di caricare il nodo successivo, chiediti: *"questa nota è parte della catena causale della risposta, o è background del background?"*. Se la seconda, stop su quel ramo — ma continua sugli altri.
4. **Niente filtri sintattici** (tag, area, depth fisso) come criterio di stop.

Il criterio è un **giudizio semantico**, non un'automazione. Dev'essere così perché ogni query ha una catena causale diversa e le etichette del vault non sono perfettamente allineate alla domanda.

## Alternative valutate e scartate

- **Depth fisso** (es. `build_context(depth=1)` sempre): semplice ma cieco — tronca rami che sono a 2 hop ma centrali, carica rami a 1 hop che sono tangenziali.
- **Filtro per tag o area**: taglia via contesto cross-dominio necessario. L'esempio `context_threshold_filter` è il caso d'uso killer.
- **Hard cap su token caricati**: restrittivo ma arbitrario. Una query complessa con catena causale lunga richiede più contesto di una semplice — il cap uniforme non distingue.
- **Caricamento totale del dominio del progetto**: il pattern più grossolano — rompe la logica di scoping in modo sistematico, consuma token senza controllo.

## Conseguenze

**Positive:**
- Le domande ICP/value-prop/feature trovano la catena causale completa, anche quando attraversa più etichette del vault.
- Il sistema tollera un vault MECE ma non perfettamente categorizzato (realtà: le note vivono sotto una cartella, ma la conoscenza fluisce tra cartelle).

**Negative / rischi:**
- Il giudizio semantico è **soggettivo** — due run sulla stessa query possono espandere rami diversi. Accettabile finché non emerge un caso in cui questa variabilità produce risposte significativamente diverse.
- Nessun cap oggettivo → potenziale rischio di espansione su grafi grandi. Mitigazione: il founder può sempre interrompere e chiedere di restringere.

## Come si misura se funziona

Test di validazione end-to-end (punto 7 della Roadmap post-Step C in [[Brain-Framework-Implementazione]]): da `~/projects/ai-football-trading/` chiedere *"questa feature è cutting-edge per l'ICP?"* → verificare che Claude (a) parta dalla MOC FT come seme, (b) incroci con [[Strategia-Attuale]] come filtro di priorità, (c) **non carichi tutta la cartella `20-Iniziative/🔥-Attive/`** né tutto il dominio.

## Collegamenti

- [[Decisione-Framework-Brain-Globale-Locale]] — decisione architetturale madre
- [[Brain-Framework-Implementazione]] — Step C chiuso, roadmap post
- [[Strumenti-Filing-Brain-Globale-Locale]] — regola canonica di filing (complementare)
