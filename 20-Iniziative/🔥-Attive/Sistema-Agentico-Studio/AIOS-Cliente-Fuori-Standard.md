---
tipo: concetto
creato: 2026-05-03
aggiornato: 2026-05-03
stato: attivo
tags:
  - progetto/sistema-agentico
  - knowledge-studio
  - cliente-fuori-standard
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari: []
forma_aggancio: input
sistema_owner: "[[Sistema-Agentico-Studio]]"
fonte: "[[AIOS-Intervista-Padre-Follow-Up]]"
---

# Cliente fuori standard — 3 archetipi nel pilot AIOS

> [!info] In una frase
> Lo studio ha tre archetipi di cliente che non rientrano nel cliente tipo (commercio dettaglio + impiantistica) e assorbono tempo sproporzionato: edilizia, notaio, farmacia. Tutti e tre sono **dentro il pilot al go-live** — niente v2, niente semplificazioni di scope.

> [!danger] Vincolo di scope: pilot stressa il sistema in produzione
> Il pilot AIOS al go-live 10/05/2026 include i fuori standard fin dall'inizio. **Non si differiscono branch a una "v2"**. Il pilot serve a stressare il sistema in condizioni reali: differire un branch significa rinviare il rischio, non gestirlo. Vedi memoria globale `feedback_pilot_no_semplificazioni`.

## I 3 archetipi (in ordine di pesantezza relativa)

### 1. Edilizia (peso 1°)

- **Cosa lo rende fuori standard**:
	- **Mole di movimenti contabili** elevata.
	- **Classificazione delicata** delle registrazioni: SAL (stati avanzamento lavori), ritenute, reverse charge, split payment.
- **Implicazione AIOS**:
	- PDC custom edilizia (vedi [[AIOS-Gate-GBSoftware-Dossier#5.4 PDC e causali]]).
	- Modulo classificazione registrazioni con regole specifiche per SAL/ritenute/reverse charge/split payment.
	- AIOS in modalità **assistenza** sui passi di giudizio (classificazione), automazione sui passi meccanici (registrazione massiva).

### 2. Notaio (peso 2°)

- **Cosa lo rende fuori standard**:
	- **Spese anticipate** (somme che il notaio anticipa per conto del cliente — fuori dal volume d'affari ma dentro la cassa).
	- **Fatturazione attiva particolare** (struttura specifica delle prestazioni notarili).
	- **Costi non sempre deducibili**.
- **Implicazione AIOS**:
	- PDC custom notaio.
	- Distinzione automatica tra costi deducibili e non deducibili in fase di registrazione.
	- Gestione separata anticipazioni vs prestazioni.

### 3. Farmacia (peso 3°)

- **Cosa lo rende fuori standard**:
	- **Ricavi da SSN** (Sistema Sanitario Nazionale) — flussi distinti dai ricavi commerciali.
	- **Magazzino** (gestione inventariale specifica del farmaceutico).
	- **Crediti verso ASL**.
- **Implicazione AIOS**:
	- PDC custom farmacia.
	- Modulo gestione crediti SSN/ASL con scadenziario specifico.
	- Integrazione gestione magazzino (potenzialmente fuori MVP, da verificare).

## Ranking di pesantezza relativa

> [!info] "Quale ti mangia più tempo a parità di compenso del cliente?"
> Il founder ha ranked: **Edilizia (1°) ≫ Notaio (2°) ≫ Farmacia (3°)**.

Il ranking guida la priorità di copertura AIOS al go-live: il branch edilizia deve essere il più rifinito, perché è quello dove la liberazione di tempo per il contabile è massima. Notaio segue a stretta distanza. Farmacia è terza ma comunque dentro pilot.

## Distribuzione nei 10 clienti pilot

I 10 clienti del pilot **includono** clienti dei 3 archetipi (la composizione esatta cliente per cliente va estratta dalla lista pilot). AIOS al go-live deve gestire tutti i branch.

## Mappa PDC

Vedi [[AIOS-Gate-GBSoftware-Dossier#5.4 PDC e causali]]: lo studio usa PDC misto (default + 3 PDC custom per i fuori standard). AIOS ha quindi 4 PDC base da gestire.

## Collegamenti

- [[AIOS-Intervista-Padre-Follow-Up]] — fonte (tema 2)
- [[AIOS-Bus-Factor-Studio]] — il titolare nei picchi è SPOF, AIOS deve coprire anche redazione bilanci/dichiarazioni di edilizia/notaio/farmacia
- [[AIOS-Processo-Quadratura-Trimestrale]] — la quadratura ordinaria diventa più complessa per i fuori standard
- [[AIOS-Gate-GBSoftware-Dossier]] — PDC custom + tracciati per i 3 archetipi
- [[Sistema-Agentico-Studio]]
- [[Prodotto-Pillar-Delivery-Piloti]]
