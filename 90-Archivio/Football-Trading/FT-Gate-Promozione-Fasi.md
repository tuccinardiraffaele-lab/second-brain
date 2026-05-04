---
tipo: concetto
creato: 2026-04-26
aggiornato: 2026-04-26
stato: attivo
progetto: "[[Football-Trading]]"
tags:
  - ft/gate
  - ft/pilot
area: prodotto
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari: []
forma_aggancio: policy
sistema_owner: "[[Processo-Validazione-Pilot]]"
---

# FT — Gate di promozione tra le tre fasi

> [!info] In una frase
> Due gate sequenziali: paper → live proprietario (≥1 mese green + KPI sopra threshold + ROI ≥8-10%) e live proprietario → mercato (training + validazione layer Gen AI). Timing dei due gate **indipendente**.

## Gate 1 — paper trading → live trading proprietario

> [!warning] Condizioni tutte necessarie
> 1. ≥1 mese **in green** continuativo in paper trading (rule-based)
> 2. Tutti i KPI interni **sopra threshold** (da definire — vedi [[FT-Chiarire-KPI-Metrics-Analyzer]])
> 3. Performance che **batte il benchmark di mercato** su una parte significativa dei KPI
> 4. **ROI atteso netto commissioni**: ≥8-10%
>
> Principio sottostante: **risk-adjusted return equo** — a parità di rischio, il sistema deve rendere almeno quanto alternative comparabili.

## Gate 2 — live trading proprietario → apertura al mercato

Il secondo gate è **l'addestramento e la validazione del layer Gen AI** sui dati generati in fase 2. Il timing dei due gate è **indipendente**: si può entrare in live proprietario senza aver ancora addestrato l'AI.

## Verifica garanzia di rimborso

- Cliente dichiara **un solo account Betfair** al primo login
- Log dell'account fanno fede per verifica P&L sui 3 mesi

## Collegamenti

- [[Football-Trading]] — MOC del progetto
- [[FT-Layer-AI-Tre-Fasi]] — le tre fasi
- [[FT-KPI-Monitorati]] — KPI su cui misurare i gate
- [[FT-Chiarire-KPI-Metrics-Analyzer]] — azione aperta su threshold
- [[FT-Pricing-Model]] — garanzia di rimborso linkata al gate
- [[KR2.1 — Paper trading debuggato]]
- [[KR2.2 — Paper trading in profitto 30 giorni]]
