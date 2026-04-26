---
tipo: progetto
creato: 2026-04-19
aggiornato: 2026-04-19
stato: attivo
tags:
  - progetto/sistema-agentico
  - azione-aperta
  - intervista
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
prossima_azione: "Pianificare la seconda intervista con padre il 2026-04-25"
blocco: ""
---

# Seconda intervista padre — follow-up KB

> [!info] Contesto
> La prima intervista ([[AIOS-Intervista-Padre-Domande-KB]]) del 2026-04-19 ha chiuso le metriche pilot (vedi [[KR1.2 — Metriche pilot fissate con padre]]) ma ha lasciato tre aree sotto-approfondite che servono prima del go-live del ~10 maggio 2026.

## Calendario

| Data | Attività |
|---|---|
| **2026-04-25** | Pianificare la sessione: fissare orario, confermare con padre, preparare domande specifiche |
| **2026-04-26** | Esecuzione seconda intervista |

## Temi da approfondire

### 1. Bus-factor per singola persona

Prima intervista (D15) ha risposto in modo generico ("il contatto con la clientela e la contabilità periodica"). Serve mappare il rischio persona per persona sulle **quattro posizioni** ([[AIOS-Intervista-Padre-Domande-KB|D14]]):

- **Titolare** — se salta 1 settimana, cosa si blocca? 1 mese?
- **Contabile società** — stessa domanda
- **Contabile privati** — stessa domanda
- **Segreteria** — stessa domanda

Obiettivo: identificare i **single point of failure** e capire dove AIOS può fungere da backup di competenza.

### 2. Cliente "fuori standard" che dà più lavoro

Prima intervista (A2) ha mappato il cliente tipo (commercio al dettaglio medio + impiantistica) ma non ha isolato il cliente **anomalo** che assorbe tempo sproporzionato. Serve per capire se il pilot deve progettarsi sul caso standard o prevedere branch per casi particolari.

Domande:
- Chi è (o che profilo ha) il cliente fuori standard tipico?
- Cosa lo rende faticoso (volumi, documenti caotici, richieste ad hoc, settore normato)?
- Quanto tempo assorbe in proporzione al peso economico?

### 3. Processo di quadratura trimestrale (pain #1) — MECE

È il pain emerso **tre volte** (E17, E18, E19) e la soglia 1 del pilot ("quadratura trimestrale entro fine mese successivo") dice che AIOS deve aiutare proprio lì. Oggi nel vault la quadratura è una black box: servono **i passi operativi**.

Domande (stile mappatura Lean):
- Per una contabilità ordinaria tipo, qual è la **sequenza di passi** dalla ricezione documenti del trimestre fino alla quadratura chiusa?
- Chi fa ciascun passo (titolare, contabile, segreteria, cliente)?
- Quanto dura tipicamente ciascun passo?
- Dove si **blocca** di solito (attesa documenti cliente, dubbio di classificazione, confronto con GBSoftware, conferma titolare)?
- Quali passi sono **meccanici** (candidati automazione) vs **di giudizio** (candidati assistenza)?

Obiettivo: distinguere ciò che AIOS può automatizzare da ciò che può solo accelerare con assistenza, evitando di sovrastimare o sottostimare il valore del sistema al go-live.

## Criterio di chiusura

La seconda intervista si considera chiusa quando nel vault esistono:

- Una nota o sezione **bus-factor studio** con mappa persona→impatto
- Una nota su **cliente fuori standard** con profilo e peso operativo
- Una nota (o aggiornamento CBA) sul **processo quadratura trimestrale** con passi, attori, durate, punti di blocco

## Collegamenti

- [[AIOS-Intervista-Padre-Domande-KB]] — prima intervista (fonte dei gap)
- [[AIOS-Chiarire-Metriche-Pilot]] — soglia 1 quadratura, dipende dal processo mappato qui
- [[Sistema-Agentico-Studio]]
- [[OKR-Correnti]]
