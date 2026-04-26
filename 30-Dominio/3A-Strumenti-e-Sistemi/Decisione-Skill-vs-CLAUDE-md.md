---
tipo: decisione
creato: 2026-04-14
aggiornato: 2026-04-14
stato: attivo
tags:
  - decisione/strumenti
  - strumenti/claude-code
  - metodo/skill
area: strumenti
---

# Decisione — Skill Claude Code come pattern standard per processi operativi

> [!info] In una frase
> I processi operativi ricorrenti (troubleshooting, review cycle, validazione pilot, ecc.) vanno implementati come **Skill** di Claude Code, non scritti come testo procedurale nel `CLAUDE.md` globale.

## Contesto

Il giorno precedente (2026-04-13) il metodo [[Troubleshooting-UPS-Coding]] era stato formalizzato scrivendone l'intera procedura dentro `~/.claude/CLAUDE.md`. Approccio funzionale ma non allineato alle best practice ufficiali Anthropic.

## La decisione

**I processi procedurali vivono come Skill in `~/.claude/skills/<nome>/SKILL.md`. Il `CLAUDE.md` globale contiene solo fatti identitari e principi-cardine, non playbook.**

Prima applicazione concreta: [[Troubleshooting-UPS-Coding]] → skill `troubleshooting-ups` in `~/.claude/skills/troubleshooting-ups/SKILL.md`. Il `CLAUDE.md` globale ora contiene solo il principio "niente azioni su supposizioni" + puntatore alla skill.

## Perché (evidenza da docs Anthropic)

Citazione letterale dalla documentazione ufficiale ([docs.anthropic.com/en/docs/claude-code/skills](https://docs.anthropic.com/en/docs/claude-code/skills)):

> *"Create a skill when a section of CLAUDE.md has grown into a procedure rather than a fact. Unlike CLAUDE.md content, a skill's body loads only when it's used, so long reference material costs almost nothing until you need it."*

Tre vantaggi concreti:

1. **Economia di contesto** — il `CLAUDE.md` è sempre in contesto in ogni sessione; una skill si carica solo quando serve. Processi lunghi non bruciano token inutilmente.
2. **Attivazione mirata** — la `description` nel frontmatter della skill filtra quando attivarsi, riducendo misfire (attivazione automatica solo su task pertinenti, più invocazione esplicita con `/<nome-skill>`).
3. **Scope globale automatico** — le skill in `~/.claude/skills/` sono disponibili in ogni progetto (vault, AIOS Studio, Football Trading) senza duplicazione. Precedenza Anthropic: Enterprise > Personal > Project.

## Regola operativa

| Cosa | Dove vive |
|---|---|
| Identità, valori, preferenze, principi-cardine | `CLAUDE.md` |
| Processi multi-step, playbook, checklist | Skill |
| Processo di dominio (es. `/daily`, `/decision`, `/sprint`) | Skill nel vault (`.claude/skills/`) |
| Processo di coding/tooling universale | Skill globale (`~/.claude/skills/`) |

**Test di discriminazione**: se il contenuto risponde alla domanda *"chi sei / cosa preferisci"* → `CLAUDE.md`. Se risponde a *"come si fa X"* → Skill.

## Formato ufficiale

- File: `SKILL.md` (maiuscolo, estensione `.md`) — **non** `skill.yml`.
- Frontmatter YAML: `name` (opzionale, default = nome cartella) + `description` (raccomandato, usato per l'attivazione automatica).
- Body: Markdown, <500 righe; risorse pesanti in `references/` o `scripts/` (progressive disclosure).

## Anti-pattern da evitare

- **Description troppo larga** → misfire: la skill si attiva anche quando non serve. Scrivere sempre cosa NON deve triggerarla.
- **Duplicare il processo** in `CLAUDE.md` + skill. Lasciare il puntatore nel `CLAUDE.md`, il contenuto solo nella skill.
- **Skill locale che duplica una globale** senza vera variante di contesto.

## Applicazioni del pattern

1. **[[Troubleshooting-UPS-Coding]]** → skill `troubleshooting-ups` (2026-04-14)
2. **[[Processo-Quality-Pillar-Coding]]** → skill `quality-pillar` (2026-04-17)

## Collegamenti

- [[Troubleshooting-UPS-Coding]] — primo processo migrato a skill
- [[Decisione-Adozione-UPS-Coding]] — decisione che ha generato il processo UPS
- [[Strumenti-Claude-Code]]
- [[Anthropic]]
