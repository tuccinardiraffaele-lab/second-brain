---
tipo: problema-risolto
creato: 2026-04-13
aggiornato: 2026-04-13
stato: completato
tags:
  - football_trading
  - bug/risolto
  - paper-trading
area: prodotto
progetto: "[[Football-Trading]]"
---

# Bug — Mercati sospesi tradati sull'ultimo prezzo (differito)

> [!bug] Sintomo
> In paper trading live, il sistema generava **profit artificiale** su operazioni che in produzione reale non sarebbero mai state eseguibili. Il P&L paper divergeva da quello teoricamente ottenibile in live.

## Causa

Il sistema, quando il **mercato Betfair era sospeso** (pausa, evento live non piazzabile), continuava a **tradare sull'ultimo prezzo ricevuto prima della sospensione**, in modo differito rispetto allo stato reale del mercato.

In produzione reale quelle operazioni:
- **non sarebbero state accettate** da Betfair (mercato sospeso = no matching)
- oppure, se accettate alla riapertura, lo sarebbero state a **un prezzo diverso** (post-evento), tipicamente peggiore

Risultato: **profit paper irrealizzabile** in live. Il pilot stava misurando un edge che non esiste.

## Impatto

- **Diagnostico**: P&L paper non affidabile come proxy del P&L live → metriche di validazione del gate paper→live (≥1 mese in green, ROI ≥8-10%, vedi [[FT-Gate-Promozione-Fasi]]) potenzialmente inquinate per tutto il periodo precedente al fix.
- **Strategico**: se non fosse stato intercettato, il passaggio a live trading proprietario sarebbe avvenuto su una base di evidenza falsa.

## Fix

Escluse le operazioni su mercati in stato **sospeso**: check dello stato del mercato prima di valutare il segnale e prima di piazzare il trade. Segnali che arrivano mentre il mercato è sospeso vengono **scartati**, non differiti.

## Effetto collaterale

Il fix ha introdotto una **regressione** (Bug 2): l'analytic agent non processa più i segnali che riceve. Debug aperto, bloccato fino alla prossima finestra di partite live (vedi [[Football-Trading#Log sessioni]]).

## Lezioni

1. **Stato del mercato è un input di primo livello**, non un dettaglio da assumere. Ogni decisione della pipeline deve leggere lo stato corrente, non l'ultimo cached.
2. **Log insufficienti hanno ritardato la scoperta**: il profit artificiale era visibile nei report ma le cause (trade su mercati sospesi) non erano esplicite nei log. Da qui nasce [[Tecnologia-Best-Practice-Logging-Pipeline]] — ogni step deve loggare input, decisione, stato rilevante.
3. **Validare il fix, non solo celebrarlo**: questo fix ha rotto l'analytic agent. Morale: dopo ogni fix in pipeline serve un **passaggio end-to-end** che dimostri che il flusso a valle è ancora integro, non solo che il bug originale è chiuso.

## Collegamenti

- [[Football-Trading]] — MOC del pilot
- [[Tecnologia-Best-Practice-Logging-Pipeline]] — principio nato da questa sessione
- [[KR2.1 — Paper trading debuggato]] — OKR impattato
