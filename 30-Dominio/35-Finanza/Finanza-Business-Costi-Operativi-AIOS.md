---
tipo: concetto
creato: 2026-04-15
aggiornato: 2026-04-15
stato: attivo
tags:
  - finanza
  - dominio/business
  - aios
area: finanza
---

# Costi operativi AIOS

> [!info] In una frase
> Voci di costo ricorrenti per far girare AIOS: oggi dominate dall'API LLM, con infra on-prem già disposta dallo studio. Stato: **stima qualitativa founder 2026-04-15, pre-go-live**.

## Costi diretti AIOS

### API LLM Anthropic — voce dominante

- **Uso normale**: ~€50/mese
- **Uso di picco**: ~€200/mese
- **Range implicito**: **€50–200/mese**, variabilità 4x.

> [!question] Da chiarire
> Cosa qualifica un "mese di picco" (volume pratiche? fase di sviluppo? retraining?) — serve per stimare la distribuzione effettiva a regime post-go-live.

### Compute

- **Stato attuale**: nessun deployment attivo.
- **Piano go-live**: i server sono già **disposti dallo studio di papà** → costo incrementale **€0** per il pilot.
- **Implicazione**: niente bolletta cloud per l'MVP, il costo è assorbito dall'infra esistente.

### Storage — Postgres + Redis

- **Stato MVP**: self-hosted sui server dello studio → costo incrementale **€0**.
- **Evoluzione possibile**: migrazione a **Supabase** da valutare post-MVP (trade-off gestione vs spesa mensile, decisione rinviata).

### Integrazioni

- GBSoftware, SDI, altre: **€0** (integrazioni native / gratuite).

## Costi trasversali allocabili (non solo AIOS)

Questi tool servono l'intero ecosistema di lavoro del founder, non solo AIOS. Vanno allocati in **quota** al progetto, non imputati per intero.

| Tool | Costo totale | Allocazione AIOS |
|---|---|---|
| [[Strumenti-Claude-Code]] | €100/mese | Quota da definire (usato anche per Football Trading, vault, framework) |
| Obsidian (Sync) | €8/mese | Quota da definire (vault è multi-dominio) |

> [!question] Da definire
> Criterio di allocazione — per tempo speso? Per numero di progetti? Ad ora si può stimare **~50% Claude Code su AIOS** e **~30% Obsidian su AIOS** come prima approssimazione, da validare.

## Sintesi — costo mensile AIOS a regime (prima stima)

Diretti: **€50–200/mese** (API LLM, tutto il resto €0).
Trasversali allocati (ipotesi 50% + 30%): **~€52/mese** (€50 Claude Code + €2.40 Obsidian).

**Totale indicativo**: **€100–250/mese**, dominato da Anthropic API e dalla quota Claude Code.

> [!tip] Implicazione business case
> Confronto con [[Finanza-Business-Economics-Studio]]: la **leva C** (taglio costi personale) deve battere €100–250/mese anche nello scenario peggiore. Qualunque costo persona contabile a tempo pieno è di un ordine di grandezza superiore al costo AIOS, quindi il **break-even tecnico è qualitativamente banale**; il vincolo vero è **eseguire la riduzione** (trade-off outplacement/turnover), non giustificarla economicamente.

## Collegamenti

- [[Finanza-Business]] — hub L2
- [[Finanza-Business-Economics-Studio]] — lato ricavi/leve
- [[Sistema-Agentico-Studio]] — il sistema il cui costo questa nota misura
- [[Studio-Del-Padre-Piattaforma]] — fornitore infra on-prem
