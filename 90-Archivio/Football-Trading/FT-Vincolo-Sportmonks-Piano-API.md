---
tipo: architettura
creato: 2026-04-14
aggiornato: 2026-04-14
stato: attivo
tags:
  - football_trading
  - vincoli/api
  - sportmonks
area: prodotto
progetto: "[[Football-Trading]]"
---

# Vincolo — Piano API Sportmonks non copre UEFA CL/EL

> [!warning] Scoperta 2026-04-14
> Il piano corrente dell'API **Sportmonks** non include **UEFA Champions League** né **UEFA Europa League**. Le partite di coppa europea non sono quindi utilizzabili come finestre di debug del sistema di football trading.

## Conseguenza operativa

- Finestre di debug limitate alle competizioni **incluse nel piano** (Serie A e altre leghe domestiche coperte).
- La finestra di debug serale del 2026-04-14 su partita UCL è **annullata**.
- Prossima finestra utile: **venerdì 2026-04-17 ore 18:30**, prima partita di Serie A disponibile.

## Impatto sugli OKR

- [[KR2.1 — Paper trading debuggato]]: perso uno slot di debug. Deadline chiusura Bug 2 entro 2026-04-26 resta, ma il margine si stringe.
- Serve censire in anticipo quali partite nelle prossime 2 settimane rientrano nel piano API per non incorrere di nuovo in slot "vuoti".

## Decisione aperta

> [!question] Upgrade del piano?
> Valutare se il costo di upgrade a un piano Sportmonks con copertura UEFA CL/EL è giustificato dalla maggiore densità di finestre di debug nella fase pilot. Da riprendere dopo chiusura debug Bug 2.

## Collegamenti

- [[Football-Trading]] — MOC del pilot
- [[KR2.1 — Paper trading debuggato]]
- [[FT-Bug-Mercati-Sospesi-Prezzo-Differito]] — bug da cui è nato Bug 2 in debug
