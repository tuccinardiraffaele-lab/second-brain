---
tipo: architettura
creato: 2026-04-26
aggiornato: 2026-04-26
stato: attivo
progetto: "[[Football-Trading]]"
tags:
  - ft/architettura
  - ft/modelli
area: prodotto
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari: []
forma_aggancio: asset
sistema_owner: "[[Processo-Quality-Pillar-Coding]]"
---

# FT — Edge tecnico (ensemble di modelli)

> [!info] In una frase
> Ensemble statistico (Dixon-Coles + Poisson + XGBoost custom + Odds Expectation Model) con embedding contestuale live calcolato minuto per minuto, che converge su un singolo segnale di trade.

## Componenti dell'ensemble

- **Dixon-Coles** / **Poisson** — probabilità di evento di base
- **XGBoost custom** con vettore **embedding contestuale live** calcolato minuto per minuto su snapshot dell'evento
- **Layer AI** che:
	- impara nuovi pattern
	- chiarifica ambiguità di contesto live (evita mercati non liquidi / chiusi)
	- si riaddestra periodicamente per adattarsi alla **varianza stagionale** del calcio
- **Odds Expectation Model** per price prediction / mispricing detection

## Stato del layer AI

Vedi [[FT-Layer-AI-Tre-Fasi]] per il piano di addestramento e perché il layer AI non è ancora attivo.

## Collegamenti

- [[Football-Trading]] — MOC del progetto
- [[FT-Layer-AI-Tre-Fasi]] — layer AI: stato critico e tre fasi
- [[FT-KPI-Monitorati]] — metriche su cui si misura l'edge
