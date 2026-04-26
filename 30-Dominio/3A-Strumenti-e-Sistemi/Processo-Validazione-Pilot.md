---
tipo: processo
creato: 2026-04-25
aggiornato: 2026-04-25
stato: attivo
tags:
  - processo/validazione
  - pillar/delivery-piloti
  - metodo/iws
area: strumenti
---

# Validazione Pilot

> [!info] In una frase
> Sistema cross-pilota che converte un pilot in produzione in **verdetto pass/fail/inconclusive** entro una finestra di osservazione dichiarata, su soglie congiunte fissate prima del go-live dal proprietario del criterio di successo.

## Forma canonica

| Campo | Valore |
|---|---|
| **Input** | (1) Pilot in produzione, (2) set di **soglie congiunte** dichiarate prima del go-live (osservabili + oggettive + con owner del criterio), (3) finestra di osservazione fissata, (4) evidenza raccolta nella finestra |
| **Output** | Verdetto **pass / fail / inconclusive** documentato + decisione consequente (promozione, spegnimento, iterazione) + feed al [[Processo-Cost-Deployment\|Cost Deployment]] (registro rinunce/conferme con costo atteso) |
| **Processo** | Quattro fasi: (1) pre-go-live — dichiarazione soglie con ownership; (2) finestra di osservazione — raccolta evidenza misurabile; (3) chiusura — confronto soglie/evidenza → verdetto; (4) escalation P1 per riallocazione capacity |
| **Owner operativo** | Founder. Trigger **event-driven** sulla chiusura della finestra di osservazione (FT weekend, AIOS post-go-live, futuri piloti) |
| **Agganci pillar** | **P2 primario** ([[Prodotto-Pillar-Delivery-Piloti]]), **S su P1** ([[Strategia-Pillar-Leadership-Strategica]] — feed Cost Deployment per riallocazione capacity) |

## Origine

Sistema astratto dal precedente concreto AIOS — [[Decisione-Soglie-Pilot-AIOS]] del 2026-04-19 — e dal contro-esempio [[Football-Trading]] (pilot deployato senza soglie pre-dichiarate, ancora oggi inconcludente). La promozione a sistema generico chiude **HC-F4 Foundation** del pillar [[Strategia-Pillar-Leadership-Strategica]] insieme a [[Strategia-Mappa-Pillar-Sistemi]].

L'AIOS-specifico resta nel suo file di decisione; questo sistema codifica il **meccanismo riusabile** che ogni futuro pilot dovrà attraversare.

## Loss servita

> [!info] Loss primaria — #8 Maturità-piloti-non-in-tempo
> La causa di failure non è solo "il pilot non ce la fa": è che **il pilot non riesce a produrre un verdetto** — opera in zona grigia, brucia capacity, non dichiara né vinto né perso. Il costo lo paga la finestra competitiva del pillar P1.

> [!quote] Principio fondante
> *"Veloce ma non efficace = superfluo"* — [[Valori-Fondamentali#Efficacia]]. Un pilot senza criterio di chiusura è velocità senza efficacia: non produce imparamento utile, solo log da interpretare a posteriori.

## Il flusso a quattro fasi

### Fase 1 — Pre-go-live: dichiarazione soglie

> [!danger] Regola
> Nessun pilot va in produzione senza un set di soglie congiunte **fissate dal proprietario del criterio di successo** (founder per FT, titolare studio per AIOS B2C, eventuali futuri customer per altri piloti).

Le soglie devono soddisfare 4 proprietà — adattate dal precedente AIOS:

| Proprietà | Descrizione | Test |
|---|---|---|
| **Osservabili** | Si leggono da evidenza esterna, non da stima | "Posso fotografare il valore?" |
| **Oggettive** | Non dipendono da autodichiarazione né da sensazione | "Due persone diverse darebbero lo stesso verdetto?" |
| **Coperture pain dichiarati** | Mappano i pain emersi ≥3 volte in intervista al proprietario | "Il pain X dell'intervista è coperto da quale soglia?" |
| **Ownership** | Fissate dal proprietario del criterio | "Chi ha autorità di dichiarare vinto/perso?" |

Le soglie sono **congiunte**: il mancato raggiungimento di **una sola** soglia → pilot fermato. Niente sconti compensativi.

### Fase 2 — Finestra di osservazione

Prima del go-live va dichiarato:
- **Durata della finestra** (30/60/90gg per piloti business; weekend tematico per FT).
- **Cadenza di raccolta evidenza** (continuativa? campionata? a evento?).
- **Definizione operativa di ogni metrica** (es. "classificazione corretta" = quale campione, quale revisore, quale frequenza).

> [!warning] Anti-pattern
> Soglia fissata + finestra non fissata = la finestra slitta finché non si raggiunge la soglia. Il sistema fallisce silenziosamente.

### Fase 3 — Chiusura: verdetto

A finestra chiusa, confronto soglie ↔ evidenza con tre esiti possibili:

| Verdetto | Condizione | Decisione consequente |
|---|---|---|
| **Pass** | Tutte le soglie raggiunte sull'intera finestra | Pilot promosso oltre la fase pilot — feed a P4 (positioning) e P3 (governance output al cliente) |
| **Fail** | Almeno una soglia mancata | Pilot fermato — feed a Cost Deployment (rinuncia + costo atteso) e a P1 per riallocazione |
| **Inconclusive** | Evidenza insufficiente / definizione operativa rotta a posteriori | Estensione finestra **una volta sola** con definizione operativa corretta — alla seconda inconclusive si converte in Fail |

### Fase 4 — Escalation a P1

Verdetto Pass o Fail genera un input strutturato per P1:
- **Pass** → capacity liberata (pilot in autonomia/promosso) → riallocabile su altri filoni.
- **Fail** → capacity bruciata → registrare nel [[Processo-Cost-Deployment]] come trade-off chiuso, aggiornare la guidance in [[OKR-Correnti]].

## Anti-pattern da evitare

- **Pilot senza soglie pre-dichiarate** — il precedente FT (deployato 2026-04-12 senza criteri) ha mostrato il costo: bug review nel weekend utile, certezza parziale ancora oggi, finestra di apprendimento bruciata. Vedi [[Valori-Fondamentali#Velocità]] regola-gate "il pilot riproduce le dimensioni che contano?".
- **Metriche di input invece che di output** — "ore risparmiate al dipendente" è stima soggettiva senza baseline. Sempre output osservabile.
- **Metrica singola** — non cattura il value prop reale. Per AIOS la metrica unica "accuratezza classificazione" sarebbe stata cieca su quadratura e scadenze AdE.
- **Soglie fissate da chi costruisce, non da chi consuma il pilot** — il founder che fissa le soglie del pilot da vendere al titolare studio rompe ownership. Il proprietario del criterio fissa.
- **Slittamento della finestra "per dare un'altra possibilità"** — converte la validazione in conferma motivata: non dichiari mai fail.
- **Verdetto a sensazione invece che vs evidenza** — riapre il problema di [[Football-Trading]].

## Health check del sistema

Coerente con [[Sistemi-Sotto-Pillar]], il sistema è "sano" se:

- ✅ **Copertura** — ogni pilot attivo ha soglie + finestra dichiarate prima del go-live (zero piloti senza criterio).
- ✅ **Tempestività verdetto** — verdetto emesso entro 7gg dalla chiusura finestra.
- ✅ **Feed al Cost Deployment** — ogni Fail produce una riga nel registro rinunce con costo atteso.
- ✅ **Definizione operativa stabile** — nessun verdetto Inconclusive per definizione rotta a posteriori (se accade, è bug del processo Fase 1, non del pilot).

Review: dentro [[Processo-Review-Cadence]] mensile, scan dei piloti attivi e verifica delle 4 spunte.

## Casi attivi

| Pilot | Soglie pre-dichiarate? | Finestra dichiarata? | Stato |
|---|---|---|---|
| [[Sistema-Agentico-Studio\|AIOS]] | ✅ in [[Decisione-Soglie-Pilot-AIOS]] (3 soglie congiunte) | ⚠️ periodo osservazione da fissare pre go-live ([[AIOS-Chiarire-Metriche-Pilot]]) | Pre-go-live, Fase 1 chiusa parzialmente |
| [[Football-Trading]] | ❌ assenti — debug in corso | ❌ assenti | Bug di Fase 1 retroattivo: criterio da fissare prima della pausa estiva ([[KR2.2 — Paper trading in profitto 30 giorni\|KR2.2]] è una soglia parziale ma non un set congiunto) |

## Collegamenti

- [[Decisione-Soglie-Pilot-AIOS]] — istanza concreta del sistema applicato ad AIOS (2026-04-19)
- [[AIOS-Chiarire-Metriche-Pilot]] — follow-up Fase 1 e Fase 2 per AIOS
- [[Football-Trading]] — contro-esempio: pilot senza Fase 1
- [[Strategia-Mappa-Pillar-Sistemi]] — aggancio P2 primario, S su P1
- [[Sistemi-Sotto-Pillar]] — forma canonica
- [[Prodotto-Pillar-Delivery-Piloti]] — pillar primario, loss #8
- [[Strategia-Pillar-Leadership-Strategica]] — pillar consumer via Cost Deployment
- [[Processo-Cost-Deployment]] — destinatario del feed al verdetto
- [[Processo-Review-Cadence]] — review mensile health check
- [[Valori-Fondamentali#Velocità]] — regola-gate "fedeltà di riproduzione"
- [[Valori-Fondamentali#Efficacia]] — "veloce ma non efficace = superfluo"
- [[KR1.2 — Metriche pilot fissate con padre]] · [[KR1.3 — Go-live studio padre]]
- [[Dashboard]]
