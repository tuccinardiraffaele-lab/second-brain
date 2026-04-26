---
tipo: processo
creato: 2026-04-17
aggiornato: 2026-04-17
stato: attivo
tags:
  - processo/interruzioni
  - processo/miglioramento
  - operazioni
area: operazioni
---

# Processo di gestione interruzioni e errori

> [!info] In una frase
> Come reagisco a ciò che non era pianificato — interruzioni, bug, errori di processo — con un **framework decisionale unico**: valuto l'impatto sul funzionamento del core e la risposta è proporzionale.

## Gestione interruzioni non pianificate

Quando qualcosa di inatteso interrompe un blocco di lavoro, la risposta dipende dalla matrice **impatto × urgenza**:

| Impatto | Urgenza | Risposta |
|---|---|---|
| Alto | Alta | Agisci subito — interrompi il lavoro corrente |
| Alto | Bassa | Rischedula a breve |
| Basso | Qualsiasi | Delega o rischedula con periodo ampio |

### Delega sui filoni personali

Sui filoni personali (AIOS, FT, studio giuridico) la delega vera **non esiste**: o lo faccio io, o lo faccio dopo. Unica eccezione: il padre su task concettuali AIOS (non tecnici).

"Delego al mio futuro" = rischedulo.

Nel contesto corporate [[Angelini-Pharma]], la delega funziona normalmente.

## Bug triage — 3 livelli di priorità

Quando durante una sessione di lavoro trovo un bug non cercato, lo classifico per impatto sul core:

| Livello | Criterio | Risposta |
|---|---|---|
| 1 — Critico | Rompe il core, non genera il valore atteso | Fix immediato |
| 2 — Bloccante | Non rompe il core ma impedisce la messa in produzione | Fix subito dopo i critici |
| 3 — Estetico | Impatto su UX, leggibilità codice, efficienza computazionale | Posticipabile |

> [!example] Caso concreto — Football Trading
> UI SaaS finale esclusa dall'MVP (livello 3 — non serve a validare il core). UI operativa minima inclusa perché necessaria a visualizzare se la pipeline funziona secondo le aspettative (strumento di validazione, non feature di prodotto).

## Confine MVP — regola implicita

La stessa logica si applica alle decisioni di perimetro MVP:

> [!tip] Regola
> **Entra ciò che serve a produrre evidenza che il core funziona. Esce tutto ciò che serve solo all'utilizzatore finale.** Coerente con la regola-gate di [[Processo-Validazione-Pilot]].

## Miglioramento di processo

Il miglioramento è **reattivo e proporzionale all'impatto**: il dolore è il trigger.

- Se l'errore fa **male abbastanza** → fix strutturale (es. scadenze finanziarie dimenticate → reminder nel calendario con cadenze).
- Se l'impatto è **basso** → lascio correre, non rianaalizzo il processo.

Non c'è una retrospettiva periodica sistematica sugli errori operativi.

> [!example] Caso concreto
> Il plugin per l'esame università, riemerso solo il giorno prima → impatto sufficiente → ha portato alla costruzione della v2 della [[Processo-Pianificazione-Giornaliera|pianificazione giornaliera]].

## Il framework decisionale unico (pattern trasversale)

> [!tip] Regola unificante
> Attraverso tutti i contesti operativi — prioritizzazione, interruzioni, bug triage, miglioramento di processo — la regola è la stessa: **valuto l'impatto sul funzionamento del core e la risposta è proporzionale**. Non è istinto: è un framework implicito coerente.

## Collegamenti

- [[Processo-Prioritizzazione-Operativa]] — come decido cosa fare quando nulla interrompe
- [[Processo-Validazione-Pilot]] — la regola-gate MVP è un'istanza di questo framework
- [[Processo-Pianificazione-Giornaliera]] — il miglioramento di processo reattivo ha generato la v2
- [[Valori-Fondamentali]] — velocità (regola-gate), efficacia (colpire il bersaglio vero), affidabilità
- [[Processo-Cattura-E-Retrieval-Informazioni]] — il retrieval è il problema, non la cattura
- [[OKR-Correnti]]
