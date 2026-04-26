---
tipo: processo
creato: 2026-04-17
aggiornato: 2026-04-17
stato: attivo
tags:
  - processo/prioritizzazione
  - metodo/iws
area: strumenti
---

# Cost Deployment

> [!info] In una frase
> Adattamento del **Cost Deployment** e della **Loss Tree** di [[Procter-And-Gamble|P&G IWS]] al contesto personale: un sistema che traduce le perdite (tempo, cicli, rework) in **costo annualizzato** così che la prioritizzazione dei trade-off aperti diventi un output deterministico, non un'opinione.

## Origine

Derivato dal Cost Deployment di [[Procter-And-Gamble|P&G IWS]], un processo in 7 step con 5 matrici (A-E) che:
1. Identifica e quantifica le perdite fisiche (Matrice A)
2. Stabilisce relazioni causa-effetto tra perdite causali e risultanti (Matrice B)
3. Collega le perdite ai costi di trasformazione (Matrice C)
4. Mappa le perdite causali ai framework di miglioramento appropriati (Matrice D)
5. Calcola costo-beneficio e stabilisce la prioritizzazione (Matrice E)

In P&G il meccanismo è industriale: chiavi di conversione che traducono "se perdo tot tempo causa inefficienza, a fine anno avrò tot soldi persi". La prioritizzazione non è opinione del manager — è output della matrice.

## Problema che risolve

Copre un tipo di perdita identificato nella loss map di [[Processo-Quality-Pillar-Coding]]:

| # | Perdita | Sintomo concreto |
|---|---------|-----------------|
| 8 | **Costo trade-off invisibile** | Il founder sa che rimandare i brain locali costa cicli di debugging in più, ma non sa *quanto* costa. Senza il numero, la prioritizzazione non si corregge — il trade-off resta aperto finché non esplode |

### La catena di failure

1. Il founder prende un trade-off consapevole: "so che dovrei fare X, ma ora faccio Y perché è più urgente"
2. Il costo di non fare X si accumula silenziosamente (ore di debugging, risposte incoerenti, rework)
3. Nessuno misura il costo cumulato → il trade-off resta aperto perché sembra "gratuito"
4. A un certo punto il costo esplode — ma il founder non ha il dato per dimostrare che avrebbe dovuto intervenire prima

## Il sistema: chiavi di conversione + registro trade-off

### Chiave di conversione

Ogni tipo di perdita ricorrente ha una **chiave di conversione** che traduce la perdita fisica in costo stimato:

| Perdita fisica | Unità | Chiave di conversione |
|---|---|---|
| Tempo di debugging evitabile | ore/settimana | ore × valore-ora founder |
| Cicli di rework | occorrenze/mese | occorrenze × costo medio per ciclo (ore × valore-ora) |
| Sessioni Claude Code sprecate | sessioni/mese | sessioni × costo medio sessione (token + tempo) |
| Risposte incoerenti da Claude Code | occorrenze/settimana | occorrenze × tempo medio di correzione |

> [!tip] Precisione vs utilità
> Le chiavi non devono essere precise al centesimo — devono essere **abbastanza precise da cambiare la prioritizzazione**. "~2 ore/settimana di debugging evitabile × €X/ora = ~€Y/mese" è sufficiente. L'ordine di grandezza è ciò che conta.

### Registro trade-off aperti

Un registro nel brain locale che traccia i trade-off consapevoli con il costo stimato:

```
<repo>/.brain/
  cost-deployment/
    trade-off-aperti.md
```

Struttura del registro:

```markdown
| # | Trade-off | Data apertura | Costo stimato/settimana | Costo cumulato | Soglia intervento | Stato |
|---|-----------|---------------|------------------------|----------------|-------------------|-------|
| 1 | Brain locale FT non implementato | 2026-04-01 | ~2h debugging | ~16h (8 sett.) | 20h | Aperto |
```

### Meccanismo di auto-correzione

> [!danger] Regola
> Quando il **costo cumulato** di un trade-off supera il **costo stimato di intervento**, la prioritizzazione si corregge automaticamente: quel trade-off diventa la prossima azione, indipendentemente da cosa era pianificato.

Flusso:
1. Al momento del trade-off, il founder o Claude Code stima il costo ricorrente e il costo di intervento
2. Il trade-off viene registrato con data di apertura
3. Ad ogni review (settimanale — vedi [[Processo-Review-Cadence]]), il costo cumulato viene aggiornato
4. Quando costo cumulato ≥ costo di intervento → il trade-off viene escalato a priorità

**Domanda-test per il founder quando prende un trade-off**: *"Quanto mi costa ogni settimana non fare questa cosa? E quanto mi costerebbe farla?"*. Se non sai rispondere, il trade-off è cieco — stima prima di rimandare.

## Quando applicare

- **Ogni volta che si rimanda consapevolmente** un'attività che ha un costo ricorrente (brain locale, refactor, documentazione, aggiornamento dipendenze)
- **Alla review settimanale**: aggiornare il costo cumulato dei trade-off aperti
- **Non applicare** a decisioni strategiche irreversibili (quelle vanno in `/decision`) né a task operativi senza costo ricorrente

## Anti-pattern da evitare

- **"Lo faccio dopo" senza stimare il costo** — un trade-off senza numero è un trade-off cieco
- **Precisione eccessiva** — non serve il costo al centesimo, serve l'ordine di grandezza per prioritizzare
- **Ignorare il registro** — se non lo aggiorni alla review settimanale, è come non averlo
- **Confondere trade-off con debito tecnico** — il trade-off è una scelta consapevole con costo noto; il debito tecnico (perdita #5) è una scelta con impatto invisibile, coperto dal Gate 0 del [[Processo-Quality-Pillar-Coding|Quality Pillar]]

## Collegamenti

- [[Procter-And-Gamble]] — origine: Cost Deployment e Loss Tree di IWS
- [[Processo-Quality-Pillar-Coding]] — loss map (perdita #8)
- [[Processo-Review-Cadence]] — la review settimanale aggiorna il costo cumulato
- [[Valori-Fondamentali#Efficacia]] — "colpire il bersaglio vero"
- [[Dashboard]]
