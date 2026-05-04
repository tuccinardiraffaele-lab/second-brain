---
tipo: progetto
creato: 2026-04-13
aggiornato: 2026-04-13
stato: attivo
tags:
  - football_trading
  - kpi
  - competenze/gap
area: prodotto
progetto: "[[Football-Trading]]"
prossima_azione: "Sessione con EI per chiarire KPI del metrics_analyzer"
blocco: ""
---

# Chiarire KPI metrics_analyzer con EI

> [!info] In una frase
> Alcuni KPI usati da `scripts/metrics_analyzer.py` per misurare le performance del sistema [[Football-Trading]] sono stati co-decisi con EI e non ne padroneggio il significato. Rischio: prendo decisioni di gate produttivo (passaggio da paper a live trading reale) su metriche che non interiorizzo.

## Perché è importante

Il [[FT-Gate-Promozione-Fasi|gate per passare al trading reale]] richiede che tutti i KPI interni siano **sopra threshold** e battano un benchmark di mercato. Se non capisco cosa misura una metrica, non posso:
- giudicare se la threshold scelta è sensata
- spiegarla in fase di vendita (leva commerciale del pilota)
- diagnosticare un KPI che peggiora

## KPI tracciati da `metrics_analyzer.py`

Struttura del report (da `scripts/metrics_analyzer.py`):

### A. Model Calibration
- Log Loss (DC, Bayesian, XGBoost)
- Brier Score + decomposizione: reliability, resolution, uncertainty
- XGB-DC Delta (media, stddev)

### B. Edge Quality (BR-independent)
- Yield %
- Edge Realization Ratio
- Profit Factor
- Hit Rate
- Avg Win/Loss Ratio

### C. Risk (BR-independent)
- Sharpe Ratio (annualizzato)
- Sortino Ratio (annualizzato)
- Max Drawdown % (su cum PnL)
- Max Drawdown in return points
- Calmar Ratio

### D-F. Analisi temporale
- Per-window (finestre di retraining XGBoost o mensili)
- Cross-window trends
- Intra-window decay (degradazione del modello tra retraining)

### G-J. Breakdown
- Per lega, selection, mode, exit condition

### K-L. Modelli
- Storico retraining XGBoost
- Analisi Odds Expectation Model

## Azione

> [!todo] Prossimi passi
> - [ ] Sessione con EI per spiegazione puntuale di ogni KPI non chiaro (priorità: Brier decomposition, Edge Realization Ratio, Calmar)
> - [ ] Definire threshold esplicita per ciascun KPI del gate paper → live
> - [ ] Identificare benchmark di mercato per ciascuna famiglia (Calibration, Edge Quality, Risk) — oggi assente

## Collegamenti

- [[Football-Trading]]
- [[Strategia-Attuale]]
- [[Valori-Fondamentali#Efficacia]] — non presidiare il significato delle metriche = non colpire il bersaglio vero
