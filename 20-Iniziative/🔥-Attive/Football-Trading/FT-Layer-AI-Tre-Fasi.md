---
tipo: architettura
creato: 2026-04-26
aggiornato: 2026-04-26
stato: attivo
progetto: "[[Football-Trading]]"
tags:
  - ft/architettura
  - ft/ai
  - prodotto/roadmap
area: prodotto
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari: []
forma_aggancio: asset
sistema_owner: "[[Processo-Validazione-Pilot]]"
---

# FT — Layer AI: stato critico e tre fasi

> [!info] In una frase
> Oggi pipeline statistica completa e funzionante orchestrata agent-like, ma **layer Gen AI non ancora addestrato**. Architettura a tre fasi (paper → live proprietario → mercato) per addestrare l'AI sui risultati del rule-based già profittevole.

## Stato del layer AI (critico)

Oggi il prodotto ha una **pipeline statistica completa e funzionante** (Poisson + Dixon-Coles + XGBoost + Odds Expectation Model) orchestrata con architettura **agent-like** — agenti diversi con responsabilità diverse nella stessa pipeline — ma tutta la logica di strategia, risk management e disambiguazione ambiguità è **rule-based in codice**, non governata da un modello Gen AI.

Il **modello Gen AI non è ancora addestrato**. I ganci architetturali sono pronti; manca il training.

## Scelta architetturale: AI come amplificatore

L'AI viene addestrata **sui risultati** del sistema rule-based già profittevole, non al posto di esso. Ragione: se la Gen AI venisse addestrata in parallelo al rule-based, rischierebbe di **appiattire le potenzialità della pipeline quant** durante la sua fase di training (il gradiente dell'AI ancora scadente degraderebbe l'output del rule-based già buono). Meglio: prima stabilizzare il rule-based come fonte di verità, poi usare l'AI per amplificarne l'edge.

## Tre fasi (non due)

| Fase | Modalità | Capitale | Scopo |
|---|---|---|---|
| **1. Paper trading** (oggi) | Rule-based, no AI | Zero | Validare profittabilità rule-based + accumulo trades per training |
| **2. Live trading proprietario** | Rule-based, no AI | Capitale del founder | Generare dati reali su cui addestrare il layer Gen AI |
| **3. Apertura al mercato** | Rule-based + Gen AI addestrata | Capitale clienti | Go-to-market high-ticket |

Il **pitch commerciale non cambia** — la soluzione viene venduta come "AI football trading system" perché al mercato ci si apre **solo in fase 3**, quando la Gen AI è addestrata. Non c'è gap tra narrativa e prodotto al momento della vendita.

## Collegamenti

- [[Football-Trading]] — MOC del progetto
- [[FT-Edge-Tecnico-Ensemble]] — pipeline rule-based di base
- [[FT-Gate-Promozione-Fasi]] — gate tra le tre fasi
