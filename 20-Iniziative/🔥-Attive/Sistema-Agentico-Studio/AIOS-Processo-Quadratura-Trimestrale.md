---
tipo: processo
creato: 2026-05-03
aggiornato: 2026-05-03
stato: attivo
tags:
  - progetto/sistema-agentico
  - knowledge-studio
  - quadratura
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari: []
forma_aggancio: input
sistema_owner: "[[Sistema-Agentico-Studio]]"
fonte: "[[AIOS-Intervista-Padre-Follow-Up]]"
---

# Processo quadratura trimestrale — sequenza, attori, blocchi

> [!info] In una frase
> Per ogni cliente la quadratura è eseguita end-to-end da **un solo operatore** assegnato (modello "1 cliente = 1 operatore"). Il processo si articola in **8 passi** sequenziali; i colli di bottiglia reali sono al **passo 5** (registrazione movimenti banca) e al **passo 7** (verifica conti + bilancio).

> [!tip] Pain di riferimento
> La quadratura trimestrale è il pain emerso 3 volte nella prima intervista (E17, E18, E19). La **soglia 1 del pilot** dice che AIOS deve aiutare proprio qui: "quadratura trimestrale entro fine mese successivo" (vedi [[Decisione-Soglie-Pilot-AIOS]]).

## Modello operativo: 1 cliente = 1 operatore

Ogni cliente è assegnato a un **operatore unico** (titolare, contabile società, contabile privati o segreteria a seconda del cliente). L'operatore esegue **tutti** i passi del processo dall'inizio alla fine. Niente handoff multi-persona, niente coordinamento intra-flusso.

**Implicazione AIOS**: AIOS conosce la **mappatura cliente → operatore** e dialoga con quell'unico operatore per ogni cliente. Il pain non è di sincronizzazione tra persone, è di complessità intrinseca del processo + gestione documenti del cliente.

## La sequenza degli 8 passi

| # | Passo | Tipo | Candidato AIOS |
|---|---|---|---|
| 1 | Scarica documenti contabili dal portale **Fatture e Corrispettivi** AdE | Meccanico | **Automazione** (AIOS lo fa) |
| 2 | Registra **fatture passive** in GB | Meccanico | **Automazione** (AIOS propone, contabile valida) |
| 2bis | Verifica fatture da **professionisti** → compilazione **F24 per ritenuta d'acconto** se presente | Giudizio leggero | **Assistenza** (AIOS segnala + precompila F24) |
| 3 | Registra **fatture attive** in GB | Meccanico | **Automazione** |
| 4 | Controlla **liquidazione IVA + LIPE** | Giudizio | **Assistenza** (AIOS calcola e propone, contabile valida) |
| 5 | Registra **movimenti bancari** dall'estratto conto del cliente (cartaceo; quando possibile import xls via app GB) | **Misto** (digitazione + classificazione) | **Automazione** sulla digitazione, **assistenza** sulla classificazione |
| 6 | **Riconcilia banca** | Meccanico se i dati sono puliti | **Automazione** |
| 7 | Controlla **conti contabili utilizzati + verifica bilancio/situazione contabile** | Giudizio puro | **Assistenza** (check preventivo anomalie, contabile decide) |

## Colli di bottiglia (cause primarie)

### Passo 5 — Registrazione movimenti banca

**Cause primarie del blocco**:
- (a) **Estratto conto in ritardo dal cliente** — il cliente non lo porta in tempo.
- (c) **Classificazione movimenti richiede giudizio** — questo bonifico cos'è, a quale fattura corrisponde.

**Mossa AIOS**:
- Workflow **richiesta documenti** tracciato con scadenza + reminder automatici al cliente (taglia (a)).
- Proposta **classificazione movimenti** basata su pattern storici (questo bonifico ricorrente verso fornitore X = pagamento fattura X), il contabile conferma o corregge (taglia (c)).
- Pre-registrazione **F24 home banking**: AIOS estrae l'F24 dal canale home banking autorizzato o da scansione cliente e lo pre-registra **prima** che il contabile arrivi al passo 5. Quando il contabile registra i movimenti banca trova l'F24 già lì, niente digitazione manuale.

### Passo 7 — Verifica conti + bilancio

**Causa primaria del blocco**:
- (e) **Attività di giudizio**, richiede tempo e concentrazione, viene rinviata "a mente fresca" e si accumula.

**Mossa AIOS**:
- **Check preventivo automatico** sui conti (alert anomalie: saldo negativo, conto inutilizzato, scostamenti vs anno precedente).
- Quando il contabile arriva al passo 7 trova **già la lista delle anomalie** da risolvere → riduce il "tempo di concentrazione" necessario perché entra subito sul concreto invece di scandagliare a tappeto.

## Variazioni per cliente fuori standard

I 3 archetipi fuori standard ([[AIOS-Cliente-Fuori-Standard]]) introducono complessità aggiuntiva sui passi 2, 3, 5, 7:

- **Edilizia**: passo 2/3 con classificazione delicata (SAL, ritenute, reverse charge, split payment); passo 5 con volumi di movimenti elevati.
- **Notaio**: passo 3 con fatturazione attiva particolare; passo 7 con distinzione costi deducibili/non deducibili.
- **Farmacia**: passo 3 con ricavi SSN distinti; passo 7 con crediti verso ASL.

AIOS deve far convivere il flusso standard con i branch dei 3 PDC custom (vedi [[AIOS-Gate-GBSoftware-Dossier#5.4 PDC e causali]]).

## Collegamenti

- [[AIOS-Intervista-Padre-Follow-Up]] — fonte (tema 3)
- [[AIOS-Bus-Factor-Studio]] — modello "1 cliente = 1 operatore" implica che la sostituibilità dell'operatore = bus-factor
- [[AIOS-Cliente-Fuori-Standard]] — i 3 archetipi modificano il flusso ai passi 2, 3, 5, 7
- [[AIOS-Gate-GBSoftware-Dossier]] — passi 1, 2, 3, 5, 6 dipendono dall'integrazione con GB
- [[Decisione-Soglie-Pilot-AIOS]] — soglia 1 (quadratura entro fine mese successivo) misura il valore di AIOS su questo processo
- [[Sistema-Agentico-Studio]]
- [[Prodotto-Pillar-Delivery-Piloti]]
