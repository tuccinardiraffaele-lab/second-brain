---
tipo: decisione
creato: 2026-04-17
aggiornato: 2026-04-17
stato: attivo
tags:
  - decisione/strumenti
  - claude-code
  - metodo/iws
  - processo/quality
area: strumenti
reversibilità: alta
impatto: alto
scadenza-revisione: 2026-07-17
---

# Decisione — Adozione Quality Pillar P&G IWS per il coding

> [!info] In una frase
> Adottato un sistema a gate derivato dal Quality Pillar e dall'Autonomous Maintenance di [[Procter-And-Gamble|P&G IWS]] come processo standard per ogni task di coding che impatta il comportamento del prodotto.

## Contesto

Il costo del gap tra code correctness e outcome correctness emerge solo in produzione — quando il prodotto dovrebbe funzionare e non si comporta come previsto. Caso concreto: [[Football-Trading]], dove i difetti vengono scoperti in fase di utilizzo reale del paper trading, al massimo costo di rework.

La catena di failure identificata:
1. Il founder descrive un comportamento desiderato con esempi concreti
2. Claude traduce in piano tecnico → il founder non può validarlo (linguaggio di codice, non di prodotto)
3. Claude implementa → verifica solo code correctness ("i test passano")
4. Gli esempi originali non vengono mai riusati come acceptance criteria
5. Il gap emerge in produzione → massimo costo, minimo tempo per correggere

Tre tipi di perdita coperti: **wrong target** (requisito ambiguo), **feature gap non dichiarato** (prodotto all'80% senza dichiarare il 20%), **code vs outcome correctness** (codice corretto, prodotto sbagliato).

## Decisione

**Adotto il Quality Pillar di P&G IWS — dettagliato in [[Processo-Quality-Pillar-Coding]] — come processo standard per ogni task che può impattare il comportamento del prodotto.** Il flusso a gate (Gate 1 piano in linguaggio prodotto → Gate 2 acceptance criteria → implementazione → Gate 3 verifica outcome → ciclo CI fino a ≥99% similarità) garantisce che la verifica sia sempre sulla conformità del prodotto ai requirement, non sulla correttezza del codice.

## Alternative considerate

1. **Continuare con il flusso attuale** (implementa → test → "fatto") — scartata: l'esperienza Football Trading dimostra che il gap emerge troppo tardi.
2. **Aggiungere solo acceptance criteria senza gate strutturati** — scartata: senza il Gate 1 (piano in linguaggio prodotto) e il Gate 3 (verifica outcome), gli AC diventano documentazione inerte che nessuno verifica.
3. **Quality gate solo su richiesta esplicita** — scartata: il bias è sempre verso "procediamo, poi vediamo" — il gate deve essere il default, non l'eccezione.

## Rationale

- **Evidenza empirica**: Football Trading dimostra il costo di scoprire i difetti in produzione.
- **Modello validato**: il Quality Pillar P&G IWS è usato su 120+ siti interni e 400+ esterni con risultati documentati (defect rate −80-90%, ROI 3-5x).
- **Coerente con i valori**: [[Valori-Fondamentali#Efficacia|efficacia]] ("colpire il bersaglio vero") e [[Valori-Fondamentali#Velocità|velocità]] ("velocità senza efficacia è rumore") sono protette solo se la verifica è sull'outcome, non sul codice.
- **Complementare a UPS**: [[Troubleshooting-UPS-Coding|UPS]] copre i runtime failure (perdita #1); il Quality Pillar copre wrong target, feature gap, e outcome correctness (perdite #3, #6, #7). Insieme coprono il 58% dei tipi di perdita identificati.
- **Continuous improvement integrato**: il ciclo CI (iterazione fino a ≥99%) elimina il pattern "dichiarare fatto e passare avanti" — il feature gap diventa trigger di iterazione, non disclosure.

## Rischi e trade-off

- **Rischio: overhead percepito** — mitigazione: il Gate 1 è l'unico punto di stop esplicito; il resto è autonomo. Il tempo speso sui gate è quasi sempre inferiore al tempo di rework in produzione.
- **Rischio: AC troppo granulari rallentano** — mitigazione: gli AC descrivono comportamenti osservabili, non dettagli tecnici. Meno AC ma più significativi.
- **Trade-off accettato**: alcune sessioni di implementazione diventeranno più lunghe in wall-clock, ma il prodotto arriva in produzione conforme ai requirement.

## Revisione

Rivedere entro 2026-07-17 — criteri di successo:

- I difetti scoperti in produzione calano rispetto al baseline pre-adozione (Football Trading è il benchmark).
- Il founder percepisce di avere più controllo sulla conformità del prodotto senza dover leggere codice.
- Il ciclo CI converge in ≤3 iterazioni nella maggioranza dei task.
- Il defect register in `.brain/autonomous-maintenance/defects/` viene effettivamente utilizzato e i difetti vengono chiusi.

## Note collegate

- [[Processo-Quality-Pillar-Coding]] — il processo operativo
- [[Procter-And-Gamble]] — origine: Quality Pillar e AM di IWS
- [[Decisione-Adozione-UPS-Coding]] — precedente: stessa logica di trasferimento P&G → coding
- [[Decisione-Skill-vs-CLAUDE-md]] — pattern Skill-vs-CLAUDE.md applicato
- [[Troubleshooting-UPS-Coding]] — framework complementare per runtime failures
- [[Valori-Fondamentali]]
- [[Football-Trading]] — caso concreto che ha evidenziato il problema
