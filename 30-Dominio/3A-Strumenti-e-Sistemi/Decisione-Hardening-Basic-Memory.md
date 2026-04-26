---
tipo: decisione
creato: 2026-04-15
aggiornato: 2026-04-15
stato: attivo
tags:
  - decisione/strumenti
  - basic-memory
  - claude-code
area: strumenti
reversibilità: alta
impatto: medio
scadenza-revisione: 2026-07-15
---

## Contesto

Dopo la decisione architetturale [[Decisione-Framework-Brain-Globale-Locale]] di usare Basic Memory MCP come layer di lookup sul vault Obsidian, il test in sandbox ha riprodotto empiricamente il **Rischio 1**: al reindex, BM riformatta l'indentazione YAML dei tag, aggiunge un campo proprietario `permalink: <project>/<slug>` e rimuove la riga vuota finale delle note. Questo rompe le convenzioni di `obsidian-markdown` e altera byte-per-byte i file del vault, fonte unica di verità.

Servono mitigazioni che permettano a BM di indicizzare il vault **senza toccare i file** e che siano stabili nel tempo (un `uv tool upgrade` non deve resettare silenziosamente la protezione).

## Decisione

**Hardening di Basic Memory via tre flag nel config utente di BM:**

- `ensure_frontmatter_on_sync: false` — BM non tocca frontmatter esistente.
- `disable_permalinks: true` — BM non aggiunge il campo `permalink:`.
- `auto_update: false` — BM non aggiorna se stesso (né il config) in modo opaco: gli upgrade passano da decisione esplicita dell'utente.

Ruota la mitigazione su **config**, non su fork del codice né su wrapper MCP.

## Alternative considerate

1. **Fork di Basic Memory con patch sul writer YAML** — scartata: alto costo di manutenzione continuo, bisogno di riallinearsi a ogni upstream release, incompatibile con `uv tool install` vanilla.
2. **Wrapper MCP read-only davanti a BM** — scartata: ridondante rispetto alle deny-rules già presenti nei settings utente di Claude per i tool di scrittura (`write_note`, `edit_note`, `delete_note`, `move_note`, `canvas`, `project_management`), e aggiunge un layer da mantenere.
3. **Accettare la mutazione e versionare il vault su git** — scartata: rompe le convenzioni sintattiche che la skill `obsidian-markdown` pretende (indentazione tag, riga vuota finale) e introduce rumore nei diff del vault ad ogni reindex.
4. **Pin di versione senza altre mitigazioni** — scartata da sola: riduce il rischio ma non lo elimina se domani decido di fare un upgrade intenzionale.

## Rationale

- **Zero codice custom**: la mitigazione sta in 3 righe di config, nessuna divergenza da upstream.
- **Reversibile**: togliere i tre flag ripristina il comportamento di default.
- **Validata empiricamente**: test su 20 note sample del vault vero, **20/20 hash identici** post-reindex con i flag attivi.
- **Difesa in profondità**: combinata con le 6 deny-rules sui tool di scrittura BM (che ne impediscono l'esposizione a Claude), il vault risulta immutabile da parte di BM sia via sync automatico sia via tool call.
- **`auto_update: false` è il lucchetto temporale**: un upgrade dell'MCP potrebbe cambiare il default dei primi due flag o introdurne di nuovi che mutano i file. Disabilitando l'auto-update, ogni release successiva passa da un `uv tool upgrade` esplicito, preceduto da verifica dei changelog e nuovo test in sandbox.

## Rischi e trade-off

- **Release futura di BM cambia il nome o la semantica dei flag** → mitigazione: `auto_update: false` + pin implicito via `uv tool install basic-memory` oggi a **v0.20.3**; prima di qualsiasi upgrade, rieseguire il test 20-note in sandbox.
- **Trade-off accettato — niente permalinks**: perdo la feature nativa di BM per linkare note via permalink stabile. Non è un problema nel mio uso: uso `search_notes` e `read_note("Title")`, non permalink.
- **Trade-off accettato — niente frontmatter auto-gestito**: se in futuro volessi che BM mantenga il frontmatter, dovrei riabilitare il flag e accettare le mutazioni (o spostare la logica sull'editor Obsidian).

## Revisione

Rivedere entro [[Scadenziere#2026-07-15]] — criteri di successo:
- Il vault non ha subito mutazioni byte-level attribuibili a BM in tutto il periodo (spot check su 20 note random).
- Nessun upgrade di BM è stato fatto senza test in sandbox precedente.
- Il lookup da progetti esterni (`search_notes`, `read_note`) continua a funzionare end-to-end.

Se uno dei tre criteri fallisce, rivalutare: forse conviene spostare BM dietro un wrapper o cambiare strategia di indicizzazione.

## Note collegate

- [[Decisione-Framework-Brain-Globale-Locale]] — decisione architetturale di cui questa è la mitigazione operativa
- [[Brain-Framework-Implementazione]] — Step A dove questa decisione è stata applicata
- [[Strumenti-Filing-Brain-Globale-Locale]] — regola di filing che il vault integro abilita
