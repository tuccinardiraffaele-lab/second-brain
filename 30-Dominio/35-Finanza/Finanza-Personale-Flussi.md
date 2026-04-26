---
tipo: concetto
creato: 2026-04-15
aggiornato: 2026-04-15
stato: attivo
tags:
  - finanza
  - dominio/personale
  - flussi
area: finanza
---

# Finanza — Personale — Flussi

> [!info] In una frase
> Cash flow mensile personale: **entrata unica = stipendio Angelini**; uscite non-viveri con **viveri a carico famiglia** (leva strutturale sul [[Finanza-Personale-Runway-Transizione|runway]]).

## Entrate

| Voce | Natura | Stato in transizione |
|---|---|---|
| Stipendio [[Angelini-Pharma]] | Unica fonte | Si estingue al T0 di uscita |

Nessuna micro-entrata collaterale oggi (no consulenze spot, no rendite, no dividendi). FT paper trading è ancora in debug — non contribuisce a flussi.

## Uscite mensili

### Viveri
A carico famiglia. **Non compaiono nel cash flow personale**. È la leva più grande sul runway: azzera la voce di costo tipicamente dominante.

### Uscite fisse non-viveri (non comprimibili)

| Voce | Comprimibile |
|---|---|
| Abbonamento [[Strumenti-Claude-Code]] | No |
| Auto (assicurazione, bollo, carburante, manutenzione) | No |
| Telefono / connettività | No |

### Uscite comprimibili

| Voce | Contesto |
|---|---|
| Stack [[Football-Trading]] (API Sportmonks + infra paper trading) | Sospendibile se FT non passa i gate di validazione ([[KR2.1 — Paper trading debuggato]], [[KR2.2 — Paper trading in profitto 30 giorni]]) |

### Ritenute payroll (non uscite volontarie)

- **Fondo pensione** — alimentato solo da ritenuta sullo stipendio, **nessun versamento volontario aggiuntivo**. Si interrompe automaticamente con la cessazione del rapporto Angelini. Vedi [[Finanza-Personale-Patrimonio]].

## Comportamento al T0 di uscita (inizio tirocinio CdL)

- **Entrate**: stipendio Angelini → 0; compenso tirocinio → **simbolico / rimborso spese** (atteso, non quantificato).
- **Uscite fisse**: invariate (Claude Code, auto, telefono).
- **Uscite comprimibili**: decisione caso per caso (lo stack FT va valutato rispetto allo stato di validazione del pilota a quel momento).
- **Ritenute pensione**: si fermano (non più stipendio su cui trattenere).
- **Viveri**: restano a carico famiglia (assunzione operativa corrente, da riverificare al T0).

> [!question] Domande aperte
> - Quantificazione uscite fisse mensili (Claude Code + auto + telefono) — propedeutico al calcolo runway numerico.
> - Ammontare del compenso simbolico tirocinio — già tracciato in [[Finanza-MOC]] come domanda da portare al padre.

## Collegamenti

- [[Finanza-Personale]] · [[Finanza-MOC]]
- [[Finanza-Personale-Patrimonio]] — dove i flussi accumulati si depositano
- [[Finanza-Personale-Runway-Transizione]] — come flussi + patrimonio determinano il runway
- [[Angelini-Pharma]] — unica fonte di entrate oggi
- [[Football-Trading]] — voce comprimibile
