---
tipo: concetto
creato: 2026-04-26
aggiornato: 2026-04-26
stato: attivo
progetto: "[[Football-Trading]]"
tags:
  - ft/kpi
  - ft/metriche
area: prodotto
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari: []
forma_aggancio: input
sistema_owner: "[[Processo-Validazione-Pilot]]"
---

# FT — KPI monitorati

> [!info] In una frase
> Due livelli di monitoraggio: report strutturato di `metrics_analyzer.py` (12 blocchi A→L) per analisi e gate, monitoraggio operativo quotidiano (bankroll + P&L) per pilotaggio.

## Report strutturato (`scripts/metrics_analyzer.py`)

Blocchi:
- **A. Model Calibration** — Log Loss, Brier Score + decomposizione, XGB-DC Delta
- **B. Edge Quality** (BR-indipendenti) — Yield%, Edge Realization Ratio, Profit Factor, Hit Rate, Avg Win/Loss
- **C. Risk** (BR-indipendenti) — Sharpe, Sortino, Max Drawdown, Calmar
- **D-F.** Analisi temporale (per-window, trend cross-window, decay intra-window)
- **G-J.** Breakdown per lega / selection / mode / exit condition
- **K-L.** Storico retraining XGBoost + analisi Odds Expectation Model

## Monitoraggio operativo quotidiano

- bankroll
- andamento bankroll nel tempo
- P&L daily e totale

## Azione aperta

Vedi [[FT-Chiarire-KPI-Metrics-Analyzer]] e [[KR2.3 — KPI metrics_analyzer chiariti con AI]] per la sessione di chiarimento + definizione threshold esplicite.

## Collegamenti

- [[Football-Trading]] — MOC del progetto
- [[FT-Gate-Promozione-Fasi]] — KPI usati nei gate
- [[FT-Chiarire-KPI-Metrics-Analyzer]] — azione aperta
