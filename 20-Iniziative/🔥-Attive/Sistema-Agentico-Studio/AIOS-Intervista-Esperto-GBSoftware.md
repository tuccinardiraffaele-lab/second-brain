---
tipo: progetto
creato: 2026-04-20
aggiornato: 2026-04-28
stato: attivo
tags:
  - progetto/sistema-agentico
  - azione-aperta
  - intervista
  - aios/kb
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
prossima_azione: "Confermare con l'esperto la disponibilità per giovedì 2026-04-30 (era 2026-05-01, spostata per festivo)"
blocco: ""
---

# Intervista esperto GBSoftware — dominio di processo

> [!info] Contesto
> Complemento all'[[AIOS-Intervista-Padre-Domande-KB|intervista al titolare]]: quella ha mappato studio, clientela, pain e soglie pilot, ma ha **escluso esplicitamente** l'operatività di inserimento/lettura fatture su GBSoftware, perimetro coperto da una persona dedicata.
> Questa intervista chiude il gap di **dominio di processo** su GBSoftware. **Non copre** la parte di integrazione tecnica: quella è oggetto di una ricerca separata da convalidare (vedi sotto).

## Profilo intervistato

- **Ruolo**: addetto alla **supervisione della contabilità dei clienti** dello studio.
- **Competenza**: supervisiona i flussi su GBSoftware per garantire che le **riclassificazioni delle fatture** siano fatte correttamente.
- **Fuori scope**: integrazioni tecniche con GBSoftware (non è esperto di questo).

## Calendario

| Data | Attività |
|---|---|
| **Settimana 2026-04-27 → 2026-04-30** | Confermare disponibilità con l'esperto |
| **2026-04-30 (giovedì, da confermare)** | Esecuzione intervista — spostata da 2026-05-01 (festivo) |

## Perché serve ora

KR di riferimento: [[KR1.1 — Phase 10 GBSoftware completata]] — **deadline 2026-05-03**, gate vincolante per il go-live AIOS del 2026-05-10. Senza la mappa dei flussi di processo non si può progettare correttamente l'integrazione né validare che AIOS gestisca la classificazione voci con accuratezza ≥ 80% (soglia 2 di [[Decisione-Soglie-Pilot-AIOS]]).

## Temi da coprire

### 1. Flusso supervisione end-to-end
- Dal momento in cui una fattura entra in GBSoftware al momento in cui è classificata e validata: quali sono i passi?
- Chi fa cosa (addetto inserimento, supervisore, titolare)?
- Quali controlli scattano automaticamente in GBSoftware e quali sono manuali?

### 2. Riclassificazione fatture — il pain centrale
- Quali sono le **regole di riclassificazione** ricorrenti che applichi?
- Su quali tipologie di fattura sbaglia di più chi inserisce? Perché?
- Quanto tempo dedichi ogni settimana alla correzione di classificazioni errate?

### 3. Casi edge e ambiguità
- Quali fatture richiedono **giudizio professionale** e non sono classificabili in modo deterministico?
- Esempi concreti di fatture "ambigue" su cui hai dovuto decidere caso per caso.
- Quali decisioni passano obbligatoriamente dal titolare?

### 4. Errori, scadenze e segnalazioni
- Quali errori di classificazione hanno generato in passato **segnalazioni AdE** (collegamento alla soglia 3 del pilot)?
- Quali scadenze fiscali sono più sensibili a errori di classificazione?

### 5. Aspettative su AIOS
- Cosa ti farebbe dire "AIOS sta riclassificando bene"? Cosa "sta sbagliando"?
- C'è un sotto-perimetro su cui ti sentiresti **sicuro** a far partire AIOS subito, e uno su cui **non lo lasceresti decidere mai**?

## Criterio di chiusura

L'intervista si considera chiusa quando nel vault esistono:

- Una nota o sezione **flusso di supervisione GBSoftware** con passi, attori, controlli automatici/manuali
- Una nota **regole di riclassificazione** con casi standard, casi edge e regole di escalation
- Una mappa dei **rischi di errore** con link alla soglia 2 (classificazione ≥ 80%) e soglia 3 (segnalazioni AdE ≥ 95%)

## Open question — integrazione tecnica

> [!question] Da convalidare separatamente
> Esiste una **ricerca preliminare sull'integrazione GBSoftware** già fatta dal founder, da convalidare. Tracciare dove vive (vault o repo AIOS) e pianificarne la validazione prima del 2026-05-03 ([[KR1.1 — Phase 10 GBSoftware completata]]).

## Collegamenti

- [[AIOS-Intervista-Padre-Domande-KB]] — intervista parallela al titolare (perimetro escluso GBSoftware)
- [[AIOS-Intervista-Padre-Follow-Up]] — secondo round col padre, parallelo a questo
- [[KR1.1 — Phase 10 GBSoftware completata]] — KR bloccante che questa intervista sblocca
- [[Decisione-Soglie-Pilot-AIOS]] — soglie 2 e 3 dipendono dalla qualità di riclassificazione
- [[Sistema-Agentico-Studio]]
- [[OKR-Correnti]]
