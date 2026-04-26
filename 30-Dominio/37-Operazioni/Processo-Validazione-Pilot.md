---
tipo: processo
creato: 2026-04-13
aggiornato: 2026-04-13
stato: attivo
tags:
  - processo/pilot
  - processo/validazione
  - operazioni
area: operazioni
---

# Processo di validazione e go-live di un pilot

> [!info] In una frase
> Il processo che porta un pilot dall'idea al go-live, passando per un gate "debug pre-prod esaustivo" e metriche di validazione co-definite con l'utilizzatore finale — progettato per non ripetere l'errore di fretta di [[Football-Trading]].

## Il principio fondante

> [!tip] Regola-gate (da [[Valori-Fondamentali#Velocità|Velocità]])
> *"Cosa mi aspetto che succeda in produzione, e il pilot lo riproduce fedelmente sulle dimensioni che contano?"* Se non so rispondere, non sto andando veloce — sto consegnando un esperimento incapace di produrre imparamento utile.

Questa domanda **è già codificata a monte** nella definizione MVP: l'MVP viene definito includendo le feature che mi aspetto siano vive in produzione. Non è un controllo separato al momento del deploy.

## Il processo in 7 step

### 1. Definizione MVP
L'MVP è il set minimo di feature che mi aspetto siano presenti in produzione. Include implicitamente le "dimensioni che contano" del valore velocità.

### 2. Implementazione assistita
- [[Strumenti-Claude-Code]] produce il **piano di implementazione** prima di scrivere codice.
- Implementa.
- Io **verifico l'esaustività del piano** rispetto a quanto dichiarato.

### 3. Debug pre-prod — gate principale
- **≥2 cicli di review** fatti eseguire a Claude Code **senza contesto**, dopo l'implementazione.
- Valuto le risposte per decidere se passare alla fase successiva o scavare ancora.

> [!warning] Trigger per approfondire (NON passare oltre)
> - Claude **si contraddice** tra una review e l'altra.
> - Claude **non mostra evidenza** di aver considerato tutta la pipeline del prodotto, o le parti della pipeline impattate dall'implementazione/debug appena fatti.

La soglia è "sensazione informata", non tempo o copertura numerica. Limite onesto: non sono un esperto di coding, mi appoggio al giudizio del tool.

### 4. Dry run (ove possibile)
Simulazione su dati/documenti che rappresentano il comportamento atteso in produzione:
- [[Football-Trading]] → dry run su **dati storici**.
- [[Sistema-Agentico-Studio]] → dry run su **documenti datati** dello studio.

### 5. Definizione metriche di validazione
> [!danger] Regola non negoziabile
> Le metriche di validazione del pilot si definiscono **con l'utilizzatore finale**, non in solitudine.

Eccezione: se l'utilizzatore finale **sono io stesso**, posso simularlo (caso [[Football-Trading]]). Altrimenti l'utilizzatore finale deve essere on board *prima* del go-live (caso [[Sistema-Agentico-Studio]] → il padre).

Implicazione: un pilot senza utilizzatore finale on board **non può andare in produzione**, per definizione, perché non esistono metriche di validazione.

### 6. Go-live + monitoraggio metriche
Il pilot va in produzione e viene osservato rispetto alle metriche concordate.

### 7. Gestione esito
- **Metriche ok** → pilot validato, si passa a orbita/scale.
- **Metriche KO** → ritorno in fase development:
  1. Chiedo aspettative e feedback all'utilizzatore finale.
  2. Implemento migliorie.
  3. Ri-pilot → ri-verifica metriche.

Non c'è un orizzonte temporale oltre il quale dichiaro fallimento definitivo: il ciclo development ↔ pilot è iterativo.

## Lezione incorporata — Football Trading

> [!quote] Cosa è andato storto il 2026-04-12 circa
> Pilot deployato una settimana dopo l'inizio dello sviluppo. Bug review nel weekend con le partite (la finestra utile), pilot non funzionante proprio quando doveva produrre dati. **La fretta ha bruciato la finestra che volevo catturare.**

**Cosa sarebbe stato diverso con questo processo esplicito:**
- Step 3 probabilmente non era esaustivo — mancava evidenza che Claude avesse coperto tutta la pipeline in produzione.
- Step 4 (dry run su dati storici) fatto, ma non sufficiente a scoprire i bug emersi solo in flusso live — segnale che il dry run deve coprire *anche condizioni di stress* più vicine al comportamento prod.

## Confine del processo — cosa NON è un bug da risolvere pre-prod

Alcuni comportamenti emergono **solo in produzione** (es. comportamenti del pilot Football Trading con dati live). Questi sono esclusi dal gate "debug pre-prod": andarli a cercare pre-prod è perdita di tempo, perché non sono scopribili offline.

Il gate è: *"tutti i bug scopribili senza andare in produzione sono stati trovati e fissati"*.

## Collegamenti

- [[Football-Trading]] — pilot che ha generato questa lezione
- [[Sistema-Agentico-Studio]] — pilot che applica questo processo con utilizzatore esterno
- [[Valori-Fondamentali]] — velocità, efficacia, produttività
- [[OKR-Correnti]] — KR1.2 (metriche AIOS con padre), KR2.1 (paper trading debuggato), KR2.2 (≥30gg profitto)
- [[Strategia-Attuale]]
