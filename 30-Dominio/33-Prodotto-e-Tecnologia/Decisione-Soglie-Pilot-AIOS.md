---
tipo: decisione
creato: 2026-04-19
aggiornato: 2026-04-19
stato: attivo
tags:
  - decisione/prodotto
  - progetto/sistema-agentico
area: prodotto
reversibilità: media
impatto: alto
scadenza-revisione: 2026-08-10
---

## Contesto

Il pilot [[Sistema-Agentico-Studio|AIOS]] va in go-live ~2026-05-10 presso lo studio del padre. Senza soglie numeriche pre-dichiarate, a fine pilot non si potrebbe dire "funziona" o "spegniamolo" in modo non soggettivo. [[Valori-Fondamentali#Velocità]] e il precedente [[Football-Trading]] insegnano che senza soglie il pilot diventa inconcludente.

La sessione di intervista del 2026-04-19 ([[AIOS-Intervista-Padre-Domande-KB]], domanda G26) ha chiuso questo gap con il titolare dello studio, che ha ownership sulle soglie.

## Decisione

**AIOS si considera "vinto" se rispetta tre soglie congiunte. Mancato raggiungimento di una sola soglia → pilot fermato.**

1. **Quadratura trimestrale** delle contabilità ordinarie completata entro la fine del mese successivo al trimestre.
2. **Accuratezza classificazione voci** ≥ **80%**.
3. **Scadenze senza segnalazioni AdE** ≥ **95%**.

## Alternative considerate

1. **Metriche input (ore risparmiate al dipendente)** — scartata: stima soggettiva, difficile da misurare senza baseline manuale oggi inesistente.
2. **Metrica singola (solo accuratezza classificazione)** — scartata: non cattura il value prop reale, che è rispetto scadenze e quadratura per tempo.
3. **Pilot senza soglie, decisione a sensazione a fine periodo** — scartata: precedente [[Football-Trading]] ha mostrato il costo di questa scelta.

## Rationale

Le tre metriche scelte sono:
- **Osservabili** — si leggono da evidenza esterna (scadenza rispettata sì/no, segnalazione AdE arrivata sì/no, voce classificata corretta sì/no).
- **Oggettive** — non dipendono da stima del titolare né da autodichiarazione.
- **Coprono i tre pain dichiarati tre volte** dal titolare in intervista (E17 top-3 attività da togliere, E18 errori ricorrenti, E19 cosa toglie il sonno).
- **Fissate dal titolare** — ha ownership del criterio di successo.

## Rischi e trade-off

- **Soglia 1 dipende dal processo di quadratura oggi non mappato** — mitigazione: seconda intervista 2026-04-26 per mapparlo ([[AIOS-Intervista-Padre-Follow-Up]]).
- **Periodo di osservazione non ancora definito** (30/60/90gg?) — mitigazione: da fissare prima del go-live, tracciato in [[AIOS-Chiarire-Metriche-Pilot]].
- **Definizione operativa di "classificazione corretta" non formalizzata** (campione, revisore, frequenza) — mitigazione: stesso follow-up.
- **Soglie fissate senza baseline manuale misurata** — accettiamo il rischio che si rivelino troppo facili o troppo severe; in quel caso si rivedono in corso di pilot (reversibilità media).

## Revisione

Rivedere entro [[2026-08-10]] (3 mesi post go-live). Criteri di successo: tutte e tre le soglie raggiunte sul periodo di osservazione → AIOS promosso oltre il pilot.

## Note collegate

- [[AIOS-Chiarire-Metriche-Pilot]] — dettaglio operativo delle soglie e follow-up aperti
- [[AIOS-Intervista-Padre-Domande-KB]] — fonte (G26)
- [[AIOS-Intervista-Padre-Follow-Up]] — mappatura processo quadratura (input alla soglia 1)
- [[KR1.2 — Metriche pilot fissate con padre]] — KR chiuso da questa decisione
- [[Sistema-Agentico-Studio]] — MOC progetto
- [[OKR-Correnti]] — O1 AIOS in produzione
- [[Valori-Fondamentali#Velocità]] — regola-gate "il pilot riproduce fedelmente le dimensioni che contano?"
- [[Football-Trading]] — precedente di pilot senza soglie
