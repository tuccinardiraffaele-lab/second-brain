---
tipo: processo
creato: 2026-04-13
aggiornato: 2026-04-13
stato: attivo
tags:
  - processo/coding
  - debug
  - pipeline
area: prodotto
---

# Best practice — Logging e debug log nelle pipeline

> [!info] Principio
> Quando si **costruisce** una pipeline nuova o si **debugga** una pipeline esistente, il codice deve essere **riempito di log e debug log** in ogni punto significativo del flusso. Il debug deve poggiare su **evidenze nei log**, non su ipotesi o interpretazioni di cosa "probabilmente" sta succedendo.

## Perché

Il debug della sessione paper trading [[Football-Trading]] del 2026-04-13 ha mostrato il costo di log insufficienti:

- **Bug 1** (mercati sospesi tradati a prezzo differito) è stato identificato solo perché il comportamento anomalo era grande. Un bug più sottile sullo stesso meccanismo sarebbe passato inosservato.
- **Bug 2** (regressione analytic agent che non processa più i segnali) oggi è diagnosticabile solo *con partite live*, perché mancano log che mostrino cosa l'agent riceve, cosa decide, dove si ferma. Senza log adeguati, il debug è vincolato alla finestra temporale delle partite — vincolo che **moltiplica il tempo totale di chiusura del debug** e mette a rischio [[KR2.1 — Paper trading debuggato]].

In generale, senza log:
- il debug diventa interpretativo → più cicli di ipotesi sbagliate prima di arrivare alla causa vera
- alcuni bug sono **invisibili** senza evidenza nei log (es. segnali ricevuti ma scartati silenziosamente)
- il costo di riprodurre il bug (richiedere partite live, stato specifico, ecc.) si paga a ogni ciclo di debug

## Cosa loggare (default, non negoziabile in pipeline)

Per ogni **step** della pipeline:

1. **Input ricevuto** — payload, dimensioni, identificatori chiave (non dump completi se enormi: campi rilevanti).
2. **Decisione presa** — quale branch eseguito, quale filtro attivato, quale soglia superata/non superata e **con quale valore vs threshold**.
3. **Output prodotto** — cosa passa allo step successivo, cosa viene scartato e **perché** (motivo esplicito, non "filtered out").
4. **Stato rilevante** — valori di configurazione/stato che influenzano la decisione (es. mercato aperto/sospeso, bankroll, timestamp ultimo dato ricevuto).
5. **Errori ed eccezioni** — **sempre** con stack trace e contesto, mai `except: pass`.

## Livelli di log (convenzione)

- `INFO` — eventi di business rilevanti (segnale generato, ordine piazzato, retraining avviato)
- `DEBUG` — flusso interno dettagliato (ogni decisione per ogni step)
- `WARNING` — condizioni anomale ma recuperate (dato mancante sostituito con default, segnale scartato per filtro)
- `ERROR` — fallimenti che interrompono il flusso

In **fase di debugging** il livello default deve essere `DEBUG`. In produzione si può alzare a `INFO`, ma i `DEBUG` devono restare nel codice, non essere rimossi.

## Quando applicare

- **Sempre** alla costruzione di una pipeline nuova → i log entrano contestualmente al codice, non dopo.
- **Sempre** prima di iniziare a debuggare una pipeline esistente che non ne ha abbastanza → **primo step del debug = aggiungere log**, non ipotizzare cause. Se il bug richiede condizioni rare per manifestarsi (es. partite live in [[Football-Trading]]), questo principio è ancora più stringente: si ha una sola finestra per osservare, non va sprecata.

## Cosa NON fare

- Non rimuovere i `DEBUG` "perché il bug è risolto". Il prossimo bug nello stesso punto arriverà a codice muto.
- Non usare `print()` al posto del logger (no filtro per livello, no timestamp, non disattivabile).
- Non loggare segreti, token, dati personali grezzi.
- Non loggare in modo così verboso da rendere i log illeggibili — meglio strutturati (JSON / chiave-valore) che prosa.

## Conseguenze operative

- Nei prossimi sprint su [[Football-Trading]] e [[Sistema-Agentico-Studio]], questa best practice è **vincolante**. Il codice senza log adeguati è codice incompleto.
- Nei review di codice (ciclo `execute → reviewer → decisione` definito nel `CLAUDE.md` globale), l'assenza di log nelle pipeline è un **punto bloccante**, non un nitpick.

## Collegamenti

- [[Football-Trading]] — origine operativa del principio (sessione paper trading 2026-04-13)
- [[Processo-Validazione-Pilot]] — il logging entra già nelle fasi di debug pre-prod
- [[Valori-Fondamentali#Efficacia]] — colpire il bersaglio vero richiede evidenze, non interpretazioni
- [[Valori-Fondamentali#Velocità]] — log adeguati accorciano i cicli di debug, difendendo la velocità reale
