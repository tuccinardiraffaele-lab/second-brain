---
tipo: progetto
creato: 2026-04-13
aggiornato: 2026-04-15
stato: attivo
tags:
  - progetto/sistema-agentico
  - azione-aperta
  - verifica-repo
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
prossima_azione: "Al prossimo sprint coding su AIOS Studio, verificare i 3 punti sotto"
blocco: ""
---

# Verifica roadmap agenti AIOS

> [!info] Azione di verifica sul repo
> Tre punti emersi in intervista che richiedono conferma nel codice/brain del progetto `~/projects/AIOS Studio/`. Non bloccanti per il pilot, ma vanno chiusi per avere una roadmap agenti coerente.

## Punti da verificare

### 1. Agente finanziario / advisory

**Intuizione originale del founder**: agente che, sulla base dei risultati dell'AccountingAgent, suggerisce al cliente finale leve fiscali e insight per migliorare la sua situazione finanziaria.

**Stato attuale dichiarato**: accorpato in parte in FiscalAgent e in parte in AccountingAgent.

**Da verificare**:

- È davvero accorpato (e come), o è stato droppato e dimenticato?
- Ha senso rifarlo come agente a sé post-MVP?
- Il nome "finanziario" è quello giusto? Advisory? Tax-planning?

**Quando**: deep dive post-MVP, al primo giro di consolidamento.

### 2. Agente consulenza del lavoro

**Intuizione del founder**: esiste un altro agente pensato per la gestione della consulenza lavorativa (busta paga, F24, dichiarazioni, adempimenti lavoristici).

**Stato attuale nel brain**: cercando `lavoro`, `labor`, `payroll`, `consulen.*lavor` nel `.brain/` → **nessuna menzione**. Il progetto nella sua descrizione ufficiale include "consulenza lavoro" come bounded context, ma non c'è un agente dedicato né nei file `agents/` né nel roadmap tracciato (Next-Steps.md fino a Phase 13+).

**Da verificare**:

- Esiste davvero in un documento che ho perso? Dove?
- Oppure è un agente pensato ma mai scritto nel brain?
- Se non c'è, va aggiunto formalmente alla roadmap.

### 3. "Roadmap ristrutturata" indicata dal founder

**Cosa è stato detto in intervista**: esiste una roadmap ristrutturata nel repo, "verso metà-fine file" di qualche documento.

**Cosa ho cercato**: `.brain/02-project/Next-Steps.md` (fine file = carryover Phase 10), `.brain/02-project/Overview.md`, `.brain/02-project/Current-State.md`, README, AGENTS.md, CLAUDE.md.

**Cosa ho trovato**: il Next-Steps elenca Phase 10..13+ ma nella parte alta; la parte media-finale è dedicata alle task Phase 9. Nessuna sezione chiamata "roadmap ristrutturata".

**Da verificare**:

- Path preciso del documento con la roadmap ristrutturata
- Se lì sono elencati agenti futuri non trovati nella mia ricerca

### 4. Copertura del flusso B — fatture via SDI direttamente in GBSoftware

**Emerso nel brainstorm del 2026-04-15** ([[AIOS-Brainstorm-Knowledge-Map-Padre]]): molte fatture non passano per il DocumentIntake di AIOS perché arrivano direttamente in GBSoftware via SDI/Agenzia Entrate. L'esperto le trova già lì da classificare.

**Da verificare**:

- Phase 10 GBSoftware copre la **lettura** di fatture già presenti (oltre alla scrittura di nuove)?
- Se no, quale meccanismo serve per triggerare l'AccountingAgent su queste fatture (polling, webhook, trigger manuale)?
- Quale % del volume sui 10 clienti pilot arriva via flusso B? (domanda per papà, Blocco 1 knowledge map)

Se il flusso B non è coperto al 10 maggio, il risparmio-tempo del dipendente sarà parziale → il pilot rischia di non convincere come blueprint.

### 5. Struttura del DB clienti — campi necessari per classificazione context-dependent

**Emerso nel brainstorm del 2026-04-15**: l'AccountingAgent pesca dal DB clienti per la classificazione context-dependent. Campi necessari:

- attività caratteristica (non solo ATECO, spesso generico)
- regime contabile (ordinario / semplificato / forfettario)
- forma giuridica (ss, snc, sas, srl, spa, sapa)

**Da verificare**:

- Il DB clienti supporta oggi questi tre campi?
- Per i 10 clienti pilot, il DB è popolato o i campi sono vuoti?
- Il **regime contabile** non è derivabile da documenti — serve popolamento a mano o da fonte esterna (cassetto fiscale). Chi lo fa e quando?

### 6. Retraining automatico del threshold di confidenza

**Emerso nel brainstorm del 2026-04-15**: il livello di confidenza è deciso, ma manca un meccanismo di **retraining automatico** che ottimizzi la soglia sulla base del feedback del commercialista.

**Candidato tecnico**: **Optuna** su feedback retrofeedback del commercialista.

**Da verificare**:

- È MVP o post-MVP? Senza retraining, l'accuratezza non migliora con l'uso → metrica #1 di [[KR1.2 — Metriche pilot fissate con padre]] stagna.
- Se post-MVP, quando entra in roadmap?

## Perché è importante

La **nota MOC [[Sistema-Agentico-Studio]]** descrive oggi solo 5 agenti MVP + 1 accorpato + 1 citato-ma-mancante. Se la roadmap ristrutturata contiene altri agenti pensati (es. ReconciliationAgent, SupervisionAgent dedicato, agenti B2C lato cliente finale), la descrizione del prodotto va aggiornata. È un debito informativo da chiudere.

## Azione concreta

- [ ] Al prossimo sprint coding su `~/projects/AIOS Studio/`, ripartire dal file che il founder indicherà
- [ ] Aggiornare [[Sistema-Agentico-Studio]] con eventuali agenti mancanti
- [ ] Decidere se l'agente consulenza lavoro merita un WS dedicato in una Phase futura
- [ ] Verificare copertura **flusso B** (lettura fatture da GBSoftware via SDI) in Phase 10
- [ ] Verificare struttura **DB clienti** (campi attività, regime contabile, forma giuridica) e stato di popolamento per i 10 clienti pilot
- [ ] Decidere se il **retraining threshold via Optuna** è MVP o post-MVP

## Collegamenti

- [[Sistema-Agentico-Studio]] — MOC prodotto
- [[Prodotto-Vault-Substrato-Di-Prodotto]] — architettura a 3 strati
- [[AIOS-Brainstorm-Knowledge-Map-Padre]] — fonte dei gap 4, 5, 6 sopra
