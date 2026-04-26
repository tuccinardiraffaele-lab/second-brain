---
tipo: processo
creato: 2026-04-17
aggiornato: 2026-04-20
stato: attivo
tags:
  - processo/review
  - metodo/iws
area: strumenti
---

# Review Cadence

> [!info] In una frase
> Adattamento della **Layered Process Audit**, della **DMS Review Cadence** e del **Phase Assessment** di [[Procter-And-Gamble|P&G IWS]] al contesto personale: un sistema di review prescrittive a tre livelli (settimanale/mensile/trimestrale) che forza la revisione strategica senza dipendere dalla memoria del founder.

## Origine

Derivato da tre meccanismi IWS di [[Procter-And-Gamble]]:

- **DMS Review Cadence**: review a cadenza fissa — giornaliera (DDS), settimanale (backlog e prioritizzazione), mensile (ricorrenze e root cause), trimestrale (allineamento strategico). La cadenza è strutturale, non discrezionale.
- **Layered Process Audit (LPA)**: audit stratificato su tre livelli — Layer 1 operatore (giornaliero), Layer 2 middle management (settimanale), Layer 3 dirigenza (mensile/trimestrale). Ogni livello verifica che gli standard del livello sottostante siano rispettati.
- **Phase Assessment**: gate esterni con exit criteria codificati. Il sito non può auto-promuoversi — serve validazione esterna. Una volta raggiunta Phase 4, l'assessment si ripete ogni 3 anni.

In P&G, i DMS hanno impatto operativo; i process audit sui pilastri hanno impatto strategico, verificando come il pilastro contribuisce alla strategia complessiva.

## Problema che risolve

Copre un tipo di perdita identificato nella loss map di [[Processo-Quality-Pillar-Coding]]:

| # | Perdita | Sintomo concreto |
|---|---------|-----------------|
| 12 | **Assenza di CI strategico** | Le review strategiche dipendono dalla memoria del founder. Non c'è un trigger che dica "è il momento di rivisitare la strategia di FT" o "ripensa l'architettura AIOS". Le decisioni restano congelate finché qualcosa non va storto |

### La catena di failure

1. Il founder prende decisioni strategiche sui piloti (architettura, roadmap, priorità)
2. Le decisioni funzionano nel contesto in cui sono state prese
3. Il contesto cambia (nuovi dati, nuove competenze, nuovi vincoli) ma nessuno rivede le decisioni
4. Il founder sa che dovrebbe rivedere — "vorrei migliorare la strategia di FT" — ma non ha un trigger
5. La review strategica avviene solo quando qualcosa si rompe → massimo costo di correzione

## Il sistema: tre livelli di review prescrittiva

### Livello 1 — Review operativa (settimanale)

**Quando**: durante la `/weekly` review del diario settimanale.
**Owner**: founder.
**Cosa si verifica**:

- **Backlog trade-off aperti** — aggiornare il costo cumulato nel registro di [[Processo-Cost-Deployment|Cost Deployment]]. Se un trade-off ha superato la soglia di intervento, escalarlo.
- **Brain locale** — ci sono OPL o CBA mancanti emersi durante la settimana? (vedi [[Processo-Knowledge-Management-Coding]])
- **Difetti aperti** — review del defect register del [[Processo-Quality-Pillar-Coding|Quality Pillar]]. Ci sono difetti aperti non risolti?
- **Metriche operative** — i piloti stanno producendo i dati attesi? Gap analysis se no.
- **Review pillar settimanale** (cadenza superficiale da [[Pillar-Doppio-Livello]]): per ciascuno dei 7 pillar strategici, cattura in una riga le evidenze di attività + loss catturate nella settimana. Non è valutazione di Health check — è capture per alimentare la review mensile.

> [!tip] Analogia P&G
> Equivale alla DMS review settimanale: visualizzare i backlog aperti per prioritizzazione. Impatto operativo.

### Livello 2 — Review di ricorrenze e assunzioni (mensile)

**Quando**: durante la chiusura del diario mensile.
**Owner**: founder.
**Cosa si verifica**:

- **Pattern sui difetti** — ci sono difetti ricorrenti dello stesso tipo? Se sì, la root cause non è stata risolta — escalare a UPS.
- **Pattern sui trade-off** — ci sono trade-off che vengono rimandati da più di un mese? Il costo cumulato giustifica l'intervento?
- **Stato dei KR** — i Key Result del trimestre sono on track? Se no, gap analysis: cosa sta bloccando?
- **Processo che funziona/non funziona** — i processi codificati (Quality Pillar, UPS, Knowledge Management) vengono applicati? Dove si è saltato un gate, e perché?
- **Assunzioni strategiche di progetto** — per ogni pilota attivo: le assunzioni che hanno portato a investirci sono ancora vere? Il mercato è cambiato? Sono emersi nuovi rischi? C'è evidenza che qualcosa stia invalidando la tesi iniziale? Se sì, trigger `/brainstorm` per approfondire.
- **Review pillar mensile** (Health check oggettivi da [[Pillar-Doppio-Livello]]): per ogni pillar, verifica quali Health check della fase corrente sono soddisfatti. Se tutti gli HC della fase sono chiusi → proponi avanzamento `pillar-fase-num`. Se aperti → elenca gap e registra azione per il mese prossimo. Decisione di avanzamento: founder.

> [!tip] Analogia P&G
> Equivale alla DMS review mensile: cercare ricorrenze per risolvere alla causa base. La verifica delle assunzioni strategiche anticipa il pillar audit — non aspettare il trimestre se qualcosa cambia.

### Livello 3 — Review strategica (trimestrale)

**Quando**: alla chiusura del trimestre, prima di scrivere i nuovi OKR.
**Owner**: founder.
**Cosa si verifica**:

- **Solidità della strategia** — la strategia dichiarata in [[Strategia-Attuale]] porta al successo? Le assunzioni fondanti (mercato, timing, competenze, risorse) sono ancora valide? Ci sono segnali deboli che le invalidano? L'output desiderato è uno: **assicurarsi che la strategia porti effettivamente ad avere successo**.
- **Contributo dei piloti** — ogni pilota sta contribuendo alla strategia? Se no, perché? È cambiato il contesto, è cambiata la strategia, o il pilota è disallineato?
- **Rischi da mitigare** — ci sono rischi nuovi emersi durante il trimestre? I rischi noti (endogeno/esogeno da [[Strategia-Attuale#Rischi strategici]]) sono cambiati di probabilità o impatto?
- **Decisioni da rivisitare** — ci sono decisioni prese più di 3 mesi fa che non sono mai state riviste? Sono ancora valide dato il contesto attuale?
- **Loss map** — la mappa delle perdite in [[Processo-Quality-Pillar-Coding]] è aggiornata? Ci sono nuovi tipi di perdita emersi?
- **Framework assessment** — i framework adottati (Quality Pillar, UPS, Knowledge Management, Cost Deployment, questa stessa Review Cadence) funzionano? Dove hanno fallito, e perché?
- **Roadmap pillar** (da [[Pillar-Doppio-Livello]]): verifica coerenza delle roadmap pillar con la strategia attuale; ridisegno eventuale degli end-state di fase se il contesto cambia.
- **Brainstorming strategico** — trigger esplicito per `/brainstorm` su: validità della tesi imprenditoriale, posizionamento competitivo, timing di apertura filoni rimandati (es. marketing/sales)

> [!tip] Analogia P&G
> Equivale al pillar audit annuale: verificare come il pilastro contribuisce alla strategia complessiva. Impatto strategico puro. In P&G i pilastri venivano auditati dai pillar owner — qui il founder è sia owner che auditor, il che rende ancora più importante che la cadenza sia prescrittiva e che il `/brainstorm` forzi il confronto strutturato.

## Cadenza prescrittiva

> [!danger] Regola
> Le review **non sono opzionali**. Sono nel calendario del founder con cadenza fissa. Se una review salta, il motivo viene registrato nel diario e la review viene recuperata entro la settimana successiva.

| Livello | Cadenza | Trigger | Skill |
|---------|---------|---------|-------|
| 1 — Operativa | Settimanale | `/weekly` | weekly |
| 2 — Ricorrenze | Mensile | Chiusura diario mensile | — |
| 3 — Strategica | Trimestrale | Chiusura trimestre, prima dei nuovi OKR | brainstorm |

## Come si integra con gli altri processi

```
Review settimanale (L1)
  ├── Aggiorna registro trade-off → Processo-Cost-Deployment
  ├── Verifica brain locale → Processo-Knowledge-Management-Coding
  └── Review difetti aperti → Processo-Quality-Pillar-Coding

Review mensile (L2)
  ├── Pattern difetti ricorrenti → Troubleshooting-UPS-Coding
  ├── Stato KR → OKR-Correnti
  └── Compliance processi → tutti i processi

Review trimestrale (L3)
  ├── Contributo alla strategia → Strategia-Attuale
  ├── Framework assessment → tutti i processi
  └── Brainstorming → /brainstorm
```

## Anti-pattern da evitare

- **"Faccio la review quando ho tempo"** — se non è in calendario, non esiste. La cadenza è prescrittiva.
- **"La review settimanale è sufficiente"** — la review settimanale è operativa. Senza la review mensile (ricorrenze) e trimestrale (strategia), i pattern e le decisioni obsolete restano invisibili.
- **Auto-approvazione** — il founder rivede il proprio lavoro, il che rende facile saltare le domande scomode. Il trigger `/brainstorm` nella review trimestrale forza il confronto strutturato.
- **Review senza azione** — una review che identifica un problema ma non genera un'azione è rumore. Ogni finding deve diventare un task, un trade-off registrato, o una decisione.

## Collegamenti

- [[Procter-And-Gamble]] — origine: DMS Review Cadence, Layered Process Audit, Phase Assessment di IWS
- [[Processo-Quality-Pillar-Coding]] — loss map (perdita #12) + difetti da revisionare
- [[Processo-Cost-Deployment]] — trade-off da aggiornare alla review settimanale
- [[Processo-Knowledge-Management-Coding]] — brain locale da verificare alla review settimanale
- [[Troubleshooting-UPS-Coding]] — escalation per difetti ricorrenti alla review mensile
- [[OKR-Correnti]] — stato KR alla review mensile
- [[Strategia-Attuale]] — contributo alla strategia alla review trimestrale
- [[Dashboard]]
