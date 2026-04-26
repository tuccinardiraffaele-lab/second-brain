---
tipo: processo
creato: 2026-04-26
aggiornato: 2026-04-26
stato: attivo
tags:
  - processo/routine
  - pillar/p1
  - strumenti/claude-code
area: strumenti
pillar_primario: "[[Strategia-Pillar-Leadership-Strategica]]"
pillar_secondari:
  - "[[Prodotto-Pillar-Delivery-Piloti]]"
  - "[[Strategia-Pillar-Monitoraggio-Regolatorio]]"
forma_aggancio: sistema
sistema_owner: "[[Strategia-Mappa-Pillar-Sistemi]]"
---

# Studio AI Quotidiano

> [!info] In una frase
> Routine cloud schedulata che fa scouting giornaliero su fonti AI accreditate focalizzate su Claude/Anthropic, genera un digest nel vault e notifica su Slack.

## Scheda sistema

| Campo | Valore |
|---|---|
| **Input** | 6 fonti AI accreditate (vedi sotto) |
| **Output** | Nota in `00-Inbox/` + notifica Slack #second-brain |
| **Owner** | Routine cloud (claude.ai/code/routines) |
| **Frequenza** | Giornaliera alle 12:00, 7/7 |
| **Agganci** | **P1 primario**, S su P2 (opportunità tecniche piloti), S su P7 (segnali competitivi) |

## Fonti monitorate

| Fonte | Tipo | URL/Handle |
|---|---|---|
| Anthropic Blog + Research | Blog/Paper | https://www.anthropic.com/research |
| Simon Willison | Blog | https://simonwillison.net |
| Claude Code changelog | Docs | https://docs.anthropic.com/en/docs/claude-code |
| Hacker News (filtro Claude) | Community | https://hn.algolia.com/?query=claude%20anthropic |
| @AnthropicAI | X/Twitter | https://x.com/AnthropicAI |
| Dario/Amanda Amodei | X/Twitter | https://x.com/DarioAmodei, https://x.com/AmandaAmodei |

## Configurazione Routine

### Trigger

```
daily at 12:00 Europe/Rome
```

### Prompt

```markdown
# Studio AI Quotidiano — Scouting Claude/Anthropic

## Obiettivo
Fai scouting sulle fonti AI elencate, filtrando solo contenuti relativi a Claude, Claude Code, Anthropic. Ignora altri modelli/provider a meno che non si intersechino con Claude.

## Fonti da scansionare
1. Anthropic Blog + Research (https://www.anthropic.com/research)
2. Simon Willison blog (https://simonwillison.net) — ultimi 24h
3. Claude Code changelog/docs — nuove release/breaking changes
4. Hacker News — search "claude" OR "anthropic" ultimi 24h
5. X/Twitter: @AnthropicAI, @DarioAmodei, @AmandaAmodei — ultimi 24h

## Output richiesto

### Nota Markdown
Scrivi una nota in `00-Inbox/Studio-AI-YYYY-MM-DD.md` con:

```yaml
---
tipo: digest
creato: YYYY-MM-DD
stato: attivo
tags:
  - digest/ai
  - fonte/claude
area: strumenti
---
```

Struttura del body:
1. **TL;DR** — 2-3 bullet con gli highlight del giorno (o "Niente di rilevante oggi")
2. **Per fonte** — sezione per ogni fonte con contenuti trovati
3. **Action items** — se qualcosa impatta [[Sistema-Agentico-Studio]] o [[Football-Trading]], evidenzialo esplicitamente con callout `[!warning]`

### Stile
- Tecnico ma digeribile — il lettore è un PM/ingegnere, non un ML engineer
- Traduci concetti research in termini di impatto pratico
- Wikilinks a note esistenti nel vault se pertinenti

### Slack
Post summary su #second-brain:
- Titolo: "📡 Studio AI — YYYY-MM-DD"
- Body: il TL;DR + link al commit

## Commit
Committa la nota su branch `main` con messaggio:
```
chore(vault): studio AI quotidiano YYYY-MM-DD
```

## Guardrail
- NON creare PR, committa direttamente su main
- Se tutte le fonti sono vuote, scrivi comunque la nota con "Niente di rilevante oggi"
- NON modificare altre note del vault
```

## Setup su claude.ai/code/routines

1. Vai a **https://claude.ai/code/routines**
2. Clicca **New Routine**
3. **Nome**: `Studio AI Quotidiano`
4. **Repository**: `tuccinardiraffaele-lab/second-brain`
5. **Trigger**: `Daily` → `12:00` → Timezone `Europe/Rome`
6. **Prompt**: copia il prompt sopra
7. **Slack integration**: abilita, seleziona `#second-brain`
8. **Save**

## Dipendenze

- **Obsidian Git plugin**: deve essere attivo con auto-pull per sincronizzare le note dal repo al vault locale
- **Slack integration**: deve essere configurata su claude.ai/code/routines

## Health check

| Check | Frequenza | Azione se fail |
|---|---|---|
| Nota generata? | Daily (verifica in 00-Inbox) | Controlla logs Routine su claude.ai |
| Slack notification? | Daily | Verifica integration settings |
| Obsidian sync? | Daily | Verifica Obsidian Git plugin |

## Collegamenti

- [[Strategia-Mappa-Pillar-Sistemi]] — sistema P1 #4
- [[Strategia-Pillar-Leadership-Strategica]] — pillar owner
- [[Sistema-Agentico-Studio]] — beneficiario action items
- [[Football-Trading]] — beneficiario action items
- [[Processo-Cattura-E-Retrieval-Informazioni]] — sistema gemello (cattura manuale vs automatica)
