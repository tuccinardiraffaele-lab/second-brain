---
tipo: decisione
creato: 2026-04-27
aggiornato: 2026-04-27
stato: attivo
tags:
  - decisione/strumenti
  - tooling/agenti
  - claude-code
area: strumenti
reversibilità: media
impatto: medio
scadenza-revisione: 2027-04-27
---

## Contesto

Il progetto AIOS Studio era stato bootstrappato con **due agenti AI in parallelo**: Claude Code (`.claude/` directory + `CLAUDE.md`) e Codex (`.codex/` directory con `ROUTING.md`, 9 personas, 14 skill operative + `AGENTS.md` root). I due sistemi erano scaffolded come pari grado: stessa idea di routing per task surface, stesse skill backend (`aios-backend-implementation`, `aios-contract-review`, ecc.), stessa policy `Skill-Authority-Policy.md`. Nel tempo Claude Code è diventato l'unico agente effettivamente usato per lo sviluppo, mentre i file Codex restavano come residuo passivo. La conferma della contaminazione è emersa durante il redesign del brain locale del 2026-04-27: `Codex-Manual.md` e `Rules.md` contenevano riferimenti a contesti di altri progetti game-dev (`Fire-Red`, `pokeplatinum`) mai puliti. Mantenere doppio scaffold significa mantenere doppia manutenzione, drift di routing, e divergenza silenziosa tra i due sistemi di skill.

## Decisione

**Codex è dismesso completamente come agente di sviluppo. Vale per AIOS Studio oggi e per ogni futuro progetto: solo Claude Code.**

## Alternative considerate

1. **Tenere Codex parallelo per opzionalità** — scartata: il costo di manutenzione doppia non è giustificato dal valore di una opzionalità che non sto esercitando. Opzione che non eserciti = costo senza ritorno.
2. **Archiviare i file Codex invece di eliminarli** — scartata: il git history conserva già lo snapshot pre-dismissione (commit `64db257` + tag prima della rimozione). Tenere artefatti morti nel working tree è rumore puro che inquina il routing degli agenti vivi.
3. **Migrare le 14 skill Codex a `.claude/skills/`** — scartata: le skill Codex erano ottimizzate per il runtime Codex (formato YAML frontmatter Codex-specifico, riferimenti a `.codex/personas/` come lens). La migrazione richiederebbe riscrittura completa, non porting. Se in futuro emergerà l'esigenza di skill backend AIOS modulari per Claude Code, le scriverò ex-novo.

## Rationale

Il ragionamento è netto: **Codex era un agente che ora non utilizziamo più**. Quando uno strumento smette di essere usato, la pulizia è preferibile alla conservazione "in caso serva". Tre conferme operative dietro la decisione:

- **Single-agent = chiarezza di routing.** Un solo `CLAUDE.md`, un solo `.claude/`, un solo set di skill, un solo flusso di apprendimento. Il founder non deve più chiedersi "quale dei due capisce meglio questa cosa".
- **Eliminare residui di contaminazione.** I riferimenti `Fire-Red`/`pokeplatinum` in `Codex-Manual.md` erano sintomo di una manutenzione non avvenuta. Lasciar vivere file non manutenuti = entropia che cresce nel tempo.
- **Coerenza con [[Valori-Fondamentali#Velocità]]:** opzionalità non esercitata appartiene alla categoria "non sto andando veloce, sto trascinando peso morto".

## Rischi e trade-off

- **Rischio**: emergesse in futuro un caso d'uso dove Codex serve davvero (es. agente specifico per OpenAI ecosystem) → mitigazione: il rebootstrap parte dal git history (tag pre-dismissione), niente è perduto definitivamente, ma costa tempo. Reversibilità reale, non immediata.
- **Trade-off accettato**: rinuncio all'opzionalità multi-agente per il vantaggio della semplicità single-agent. Decisione coerente con il pattern del founder di concentrare focus piuttosto che diversificare strumenti.

## Revisione

Rivedere entro [[2027-04-27]] — criteri di successo: nessun rimpianto operativo (zero momenti in cui "se avessi tenuto Codex…"), Claude Code copre il 100% dei casi d'uso AIOS e dei progetti aperti nel frattempo. Se emergono casi d'uso non coperti da Claude Code, valutare strumento alternativo (non necessariamente Codex).

## Note collegate

- [[Valori-Fondamentali]] — coerenza con principio velocità × efficacia
- [[Sistema-Agentico-Studio]] — progetto su cui la decisione è stata applicata operativamente
- [[Strumenti-Dashboard-Auto-Generata-Via-Bases]] — altre decisioni sul tooling del vault
