---
tipo: decisione
creato: 2026-04-18
aggiornato: 2026-04-18
stato: attivo
tags:
  - decisione/processo
  - strumenti/claude-code
  - processo/quality
area: strumenti
---

# Decisione — Quality Pillar come gate di pianificazione

> [!info] In una frase
> La skill [[Processo-Quality-Pillar-Coding|`quality-pillar`]] si attiva anche *mentre si scrive un piano* e ad ogni ingresso in **plan mode** di Claude Code, non solo durante l'implementazione di feature/bugfix.

## Contesto

Durante una sessione plan mode sul progetto [[Football-Trading]] (pre-partita 2026-04-18), Claude Code ha generato un piano di verifica runtime (`~/.claude/plans/per-favore-rivedi-il-structured-bubble.md`) con **OSS tecnici** — query SQL, chiavi Redis, nomi colonna — invece che acceptance criteria in linguaggio prodotto. La skill `quality-pillar` non si è attivata.

Un UPS di processo ha identificato la root cause:

1. La description della skill elencava come trigger solo tipi di task **implementativi** (feature nuova, bugfix, integrazione, cambio configurazione).
2. L'esclusione "read-only" catturava erroneamente i piani di osservazione/verifica che dichiarano "non-goal: modificare codice".
3. Nessun trigger nominava esplicitamente "scrivere un piano" o "plan mode".

Conseguenza: tutti i piani di *osservazione*, *verifica runtime*, *quality gate pre-match*, *dry-run*, *diagnosi strutturata* nascevano fuori dal controllo della skill — esattamente nel momento in cui Gate 1 (linguaggio prodotto) e Gate 2 (acceptance criteria) sarebbero più utili.

## Decisione

**Quality Pillar è gate di pianificazione prima ancora che di implementazione.** Si attiva:

- Ad ogni ingresso in plan mode di Claude Code (artefatto destinato a `~/.claude/plans/`).
- Ad ogni richiesta di "scrivere un piano" — di qualunque tipo (implementazione, verifica, osservazione runtime, quality gate, deploy, diagnosi).
- Per qualunque piano salvato in `<repo>/.brain/planning/**`.

Un piano che dichiara "non-goal: modificare codice" **non** è read-only ai fini di questa skill: è scrittura di un artefatto che definisce il comportamento atteso del prodotto.

## Alternative considerate

| Opzione | Valutazione | Esito |
|---|---|---|
| **A. Estendere description di `quality-pillar`** + CLAUDE.md globale | Attacca la root cause (la description è ciò che il modello legge per decidere attivazione). Zero overhead runtime. | ✅ **Scelta** |
| **B. Hook `PreToolUse` su `ExitPlanMode`** che blocca piani senza AC | Backstop deterministico coerente col pattern `vault-write-guard.sh`. Ma appesantisce il flusso di Claude Code e introduce una barriera in più da mantenere. | ❌ Scartata — il founder preferisce evitare hook non indispensabili |
| **C. Riga nel CLAUDE.md globale sez. 13** | Ridondante con A, ma il CLAUDE.md è sempre in contesto → rinforza il trigger anche se la skill description viene scrollata. | ✅ Scelta come complemento di A |

## Rationale

- **Perché A invece di B**: il founder ha esplicitato la preferenza per non appesantire Claude con hook quando il comportamento può essere ottenuto via description testuale. Coerente con il principio che gli hook sono paracadute deterministici da usare solo quando la description da sola non basta (cfr. `vault-write-guard.sh` che protegge il vault dalla scrittura via Edit, dove il rischio di perdita è alto e la dimostrazione empirica era già avvenuta).
- **Perché A+C invece di solo A**: la sezione 13 del CLAUDE.md globale è sempre in contesto di sistema; la skill description è caricata dinamicamente. Avere il trigger in entrambi i posti riduce il rischio che il modello in plan mode non lo "veda" al momento giusto.
- **Perché non cambiare il **flusso interno** della skill**: Gate 1 e Gate 2 della skill sono già formulati correttamente per la pianificazione (*"Piano in linguaggio prodotto"* + *"Acceptance criteria"*). Il problema era esclusivamente di **attivazione**, non di contenuto — quindi la correzione si concentra sulla description e sulla tassonomia di trigger.

## Implementazione

Tre file toccati il 2026-04-18:

- `~/.claude/skills/quality-pillar/SKILL.md` — description estesa, sezione "Quando applicare" con "scrivere un piano" e "plan mode" come trigger espliciti, esclusione "read-only" ristretta, callout-warning aggiunto nel corpo.
- `~/.claude/CLAUDE.md` (sez. 13) — paragrafo aggiunto che dichiara esplicitamente la skill come gate di pianificazione, non solo di implementazione.
- [[Processo-Quality-Pillar-Coding]] — nota canonica vault allineata in 4 punti: frontmatter, callout dopo Gate 1, sezione "Implementazione come Skill", callout "Comportamento atteso di Claude Code" con nuovo step 0 sul plan mode.

## Verify (come sapremo che la decisione funziona)

Alla prossima sessione plan mode su qualunque progetto, osservare:

1. La skill `quality-pillar` viene invocata (marker visibile nella chat).
2. Il piano prodotto contiene una sezione *Acceptance criteria* in linguaggio prodotto (forma *"Il sistema garantisce che…"*, AC-01/AC-02 numerati) **prima** delle sezioni tecniche.
3. Se un piano nasce senza AC: il fix ha fallito → riaprire UPS e rivalutare l'alternativa B (hook su `ExitPlanMode`).

## Reversibilità

**Alta.** Revert possibile con 3 edit (SKILL.md + CLAUDE.md + nota vault). Nessun cambio strutturale a codice o infrastruttura. Se il Verify fallisce ripetutamente, si può passare al Fix B senza costi sommersi.

## Collegamenti

- [[Processo-Quality-Pillar-Coding]] — processo esteso
- [[Troubleshooting-UPS-Coding]] — metodo usato per l'UPS di processo che ha prodotto questa decisione
- [[Decisione-Adozione-Quality-Pillar-Coding]] — adozione originaria del framework
- [[Valori-Fondamentali#Efficacia]] — un piano in linguaggio tecnico non è efficace: non colpisce il bersaglio (decisioni del founder in linguaggio prodotto)
