---
tipo: progetto
creato: 2026-04-13
aggiornato: 2026-04-19
stato: completato
tags:
  - progetto/sistema-agentico
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
prossima_azione: ""
blocco: ""
---

# Chiarire metriche pilot AIOS

> [!success] Chiusa il 2026-04-19
> Soglie fissate in sessione di intervista col padre ([[AIOS-Intervista-Padre-Domande-KB]], domanda G26). Chiude [[KR1.2 — Metriche pilot fissate con padre]] con 8 giorni di anticipo sulla deadline del 2026-04-27.

## Soglie di successo del pilot (versione definitiva)

| # | Metrica | Soglia **teniamolo** | Ambito |
|---|---|---|---|
| 1 | **Quadratura trimestrale** — completata entro la fine del mese successivo al trimestre | ≥ target su contabilità ordinarie | Solo contabilità ordinarie |
| 2 | **Accuratezza classificazione voci** — % di classificazioni automatiche corrette | ≥ **80%** | Tutte le fatture processate |
| 3 | **Scadenze senza segnalazioni AdE** — % di scadenze gestite senza segnalazione | ≥ **95%** | Tutte le scadenze nel periodo pilot |
| 4 | **Costo AI mensile** | ~50 € non-picco, 150-200 € pre-scadenza | Infrastruttura |

Se una delle soglie 1–3 non è raggiunta alla data di valutazione, il pilot si ferma.

## Vincoli di processo (da G27)

- Per **dichiarativi** e **bilanci**: obbligatorio colloquio cliente + firma prima di proseguire. AIOS istruisce, non conclude.
- **Conferma risultati contabili** per bilanci e dichiarativi resta decisione del titolare (F23).

## Cosa è cambiato rispetto al piano originale

Le due metriche aperte del 2026-04-13 erano:
- Accuratezza classificazione → **diventa soglia 2 con valore 80%**
- Tempo risparmiato al dipendente → **sostituita dalla soglia 1 (quadratura trimestrale entro fine mese successivo)**, che cattura il risparmio come **outcome** (quadratura per tempo) invece che come input (ore risparmiate)

La sostituzione è voluta: il padre ha scelto una metrica osservabile e oggettiva (rispetto della scadenza) invece di una stima soggettiva (ore risparmiate).

## Follow-up aperto

- [ ] Definire il **periodo di osservazione** del pilot (30/60/90 giorni dopo go-live?) — non emerso dall'intervista
- [ ] Definire **cosa conta come "classificazione corretta"** per misurare l'80% (campione, revisore, frequenza di campionamento)
- [ ] Approfondire il **processo di quadratura trimestrale** con il padre: oggi è il pain #1 dichiarato (E17, E18, E19) ma non è stato mappato nei passi operativi — senza quella mappa non sappiamo quale porzione del processo AIOS può automatizzare

## Collegamenti

- [[Sistema-Agentico-Studio]] — contesto del pilot
- [[AIOS-Intervista-Padre-Domande-KB]] — fonte delle soglie (G26)
- [[Valori-Fondamentali#Velocità]] — la regola-gate "il pilot riproduce fedelmente le dimensioni che contano?"
- [[Football-Trading]] — precedente dove la fretta ha bruciato la finestra utile
