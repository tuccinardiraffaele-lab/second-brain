---
tipo: concetto
creato: 2026-05-03
aggiornato: 2026-05-03
stato: attivo
tags:
  - progetto/sistema-agentico
  - knowledge-studio
  - bus-factor
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari: []
forma_aggancio: input
sistema_owner: "[[Sistema-Agentico-Studio]]"
fonte: "[[AIOS-Intervista-Padre-Follow-Up]]"
---

# Bus-factor studio del padre — mappa persona → impatto

> [!info] In una frase
> Lo studio del padre poggia su 4 posizioni con bus-factor differenziato: il titolare è SPOF stagionale, il contabile privati è SPOF specialistico solo sul 730, il contabile società è tamponabile ma con perdita di conoscenza tacita per cliente, la segreteria è SPOF parziale solo sul "rapporto enti".

## Le 4 posizioni

### Titolare (padre)

- **Tipo bus-factor**: SPOF **stagionale**, non costante.
- **Picchi**: bilanci da depositare (apr–mag), dichiarativi (giu–nov: 730, dichiarazioni società).
- **Fuori stagione**: lo studio gira autonomo.
- **Modalità di lavoro nei picchi**: il titolare **redige materialmente** bilanci, 730, dichiarazioni società dall'inizio alla fine. Non è (b) "i contabili preparano bozza, lui valida": è (a) "fa lui tutto".
- **Implicazione AIOS**: backup di **competenza tecnica** (assistenza alla redazione bilanci/730/dichiarazioni), non solo accelerazione di review. Nei picchi, AIOS deve poter mantenere il flusso di output anche in caso di indisponibilità del titolare.

### Contabile società

- **Tipo bus-factor**: tamponabile via **ridistribuzione interna** del lavoro tra i presenti.
- **Avvertenza**: la ridistribuzione è un **tampone** — regge la continuità apparente, ma gli altri non hanno la conoscenza tacita per cliente (storico decisioni, classificazioni atipiche, scelte fiscali pregresse). Al rientro il contabile titolare del cliente trova errori da correggere.
- **Implicazione AIOS**: **memoria condivisa per cliente** — storico decisioni, classificazioni override, prassi specifiche. AIOS rende esplicita la conoscenza tacita così la ridistribuzione non degrada qualità.

### Contabile privati

- **Tipo bus-factor**: SPOF **specialistico** solo sul **730**.
- **Stagionalità**: vincolante in stagione 730 (mag–lug), durante la quale le assenze devono essere limitate al minimo.
- **Le altre dichiarazioni redditi privati** sono distribuite tra i componenti dello studio, quindi **tamponabili** come per il contabile società.
- **Natura del SPOF**: (a) **competenza tecnica specialistica** sul 730 (deduzioni, detrazioni, coerenza dati anno precedente), non (b) relazione personale col cliente. La materia 730 la padroneggia solo lui.
- **Implicazione AIOS**: backup di competenza **mirato al 730** (suggerimento deduzioni/detrazioni, check coerenza con anno precedente, segnalazione anomalie). Fuori dal 730, nessuna esigenza specifica.

### Segreteria

- **Tipo bus-factor**: SPOF **parziale** — solo su un sotto-cappello.
- **Cappello "segreteria classica"** (PEC, mail, gestione clienti, appuntamenti): **assorbibile** dagli altri.
- **Cappello "rapporto con enti e uffici"** (CCIAA, AdE, INPS, comuni, SUAP): SPOF reale.
- **Natura del SPOF rapporto enti**: **mix** competenza + relazione. La segreteria conosce come funziona ogni ufficio (modulistica, tempi, prassi specifica), e i funzionari/sportelli la riconoscono e collaborano.
- **Implicazione AIOS**: AIOS può supplire la **parte competenza** (knowledge base procedurale per ente: modulistica, tempi, prassi, scadenze). La **parte relazione** non è sostituibile.

## Sintesi tabellare

| Posizione | Tipo bus-factor | Stagionalità | AIOS può fare |
|---|---|---|---|
| **Titolare** | SPOF stagionale | apr–mag bilanci, giu–nov dichiarativi | Backup competenza tecnica (redazione assistita) |
| **Contabile società** | Tamponabile, ma con perdita conoscenza tacita | Costante | Memoria condivisa storico cliente |
| **Contabile privati** | SPOF specialistico | mag–lug solo per 730 | Backup competenza 730 |
| **Segreteria** | SPOF parziale (solo "rapporto enti") | Costante | KB procedurale enti; relazione resta umana |

## Implicazioni cumulative per AIOS

1. **Memoria per cliente** non opzionale: classificazioni override, decisioni prassi, scelte fiscali pregresse devono essere esplicite e riusabili da chiunque sostituisca il contabile assegnato.
2. **Capability di redazione assistita** in stagione (bilanci, 730, dichiarazioni società) come backup del titolare.
3. **Modulo specialistico 730** con knowledge base deduzioni/detrazioni/anomalie a supporto del contabile privati e di chi tampona durante 730.
4. **KB procedurale enti** (per la segreteria), strutturata per ufficio/Comune con modulistica, tempi, prassi.

## Collegamenti

- [[AIOS-Intervista-Padre-Follow-Up]] — fonte (tema 1)
- [[AIOS-Cliente-Fuori-Standard]] — combinato con bus-factor titolare nei picchi
- [[AIOS-Processo-Quadratura-Trimestrale]] — il modello "1 cliente = 1 operatore" interagisce con bus-factor
- [[AIOS-Firma-Deleghe-Procure-Cliente]] — AIOS forza compliance dove c'è gap (es. antiriciclaggio)
- [[Sistema-Agentico-Studio]]
- [[Prodotto-Pillar-Delivery-Piloti]]
