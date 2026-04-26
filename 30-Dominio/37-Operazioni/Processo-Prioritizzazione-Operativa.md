---
tipo: processo
creato: 2026-04-17
aggiornato: 2026-04-17
stato: attivo
tags:
  - processo/prioritizzazione
  - operazioni
  - produttività
area: operazioni
---

# Processo di prioritizzazione operativa

> [!info] In una frase
> Come decido **cosa fare adesso** — una gerarchia a 4 livelli basata su vincoli bloccanti e costo dell'attesa, eseguita senza modulazione di energia e senza attrito nel passaggio tra filoni.

## La gerarchia decisionale (4 livelli)

Quando finisco un blocco di lavoro e devo decidere cosa fare dopo, applico questi livelli in ordine di precedenza:

### 1. Vincolo bloccante nella catena di dipendenze

Identifico il vincolo che blocca le fasi successive e lavoro su quello. Il ragionamento è da **critical path**: sbloccarlo ha l'effetto a cascata maggiore.

> [!example] Caso concreto
> Costruire il second brain globale prima dei brain locali AIOS/FT, perché questi dipendono dal framework globale. I brain locali a loro volta sbloccano feature e debugging a cascata.

### 2. Costo dell'attesa asimmetrico (vincoli concorrenti)

Quando due vincoli bloccanti competono, scelgo quello dove **aspettare costa di più** — il filone con il costo del ritardo irrecuperabile.

> [!example] Caso concreto
> Debug FT (accumula dati storici col tempo — ogni giorno perso è irrecuperabile) vs call col padre per KB AIOS (rischedulabile con meno danno). Il costo dell'attesa su FT è asimmetrico → FT ha la precedenza.

### 3. Chiudere il backlog

Se non ci sono vincoli bloccanti evidenti, chiudo le attività rimaste indietro.

### 4. Avanzare sul filone a payoff più rapido

Se il backlog è pulito, avanzo sul filone che potrebbe darmi risultati nel più breve tempo possibile.

## Gestione dell'energia

Il modello è **binario**: seguo la gerarchia finché reggo, quando sono cotto mi fermo. Non c'è modulazione intermedia — non esiste "faccio qualcosa di più leggero". O lavoro sul vincolo bloccante, o chiudo la giornata.

La qualità del lavoro non risente delle energie basse: il degrado non è graduale, è un interruttore.

## Context switch tra filoni

Il passaggio da un filone all'altro (corporate → studio giuridico → coding AIOS → debug FT) avviene **senza attrito**: nessun buffer, nessun rituale, nessun tempo di rientro. Entro diretto nel contesto successivo.

## Pattern trasversale

> [!tip] Regola unificante
> La gerarchia è interamente orientata all'**output** — cosa produce il risultato maggiore. L'energia non è un input della scelta, è solo un vincolo di stop.

## Collegamenti

- [[Valori-Fondamentali]] — produttività = velocità × efficacia; questa gerarchia è l'implementazione operativa
- [[Processo-Pianificazione-Giornaliera]] — la pianificazione definisce i MIT, questa gerarchia decide l'ordine di esecuzione in tempo reale
- [[Processo-Gestione-Interruzioni-E-Errori]] — cosa succede quando il piano viene interrotto
- [[Processo-Cattura-E-Retrieval-Informazioni]] — come mantengo il contesto tra sessioni di lavoro
- [[Strategia-Attuale]] — i quattro filoni paralleli che questa gerarchia ordina
- [[OKR-Correnti]]
