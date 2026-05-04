---
tipo: architettura
creato: 2026-05-03
aggiornato: 2026-05-03
stato: attivo
tags:
  - progetto/sistema-agentico
  - gate-gbsoftware
  - dossier
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari: []
forma_aggancio: input
sistema_owner: "[[Sistema-Agentico-Studio]]"
fonte: "[[AIOS-Intervista-Padre-Follow-Up]]"
---

# Dossier preparatorio Gate A→B GBSoftware

> [!info] In una frase
> Catalogo della conoscenza titolare-side raccolta prima del Gate A→B (sessione operativa 60 min davanti a GB): workflow attuale dei 4 documenti, configurazione GB nota, ranking di priorità writer, decisioni HITL pre-cablate. Quello che resta "da verificare al gate" è esplicitato qui sotto perché vada nel briefing con il contabile società.

> [!tip] Persona di riferimento al Gate A→B
> **Contabile società**. È il custode delle prassi causali e della conoscenza tacita per cliente. La sessione di 60 min davanti a GB richiede la sua presenza.

## 5.1 Workflow attuale dei 4 documenti

### F24 telematico

- **Origine**: **misto** — alcuni clienti pagano in home banking e portano la ricevuta, altri delegano lo studio (predisposizione + trasmissione telematica). AIOS supporta entrambi i flussi.
- **Registrazione in GB**: **misto**.
	- **Manuale**: contestuale alla registrazione movimenti banca (passo 5 della quadratura). È uno dei due colli di bottiglia identificati in [[AIOS-Processo-Quadratura-Trimestrale#Colli di bottiglia (cause primarie)]].
	- **Automatica**: immediata per gli F24 predisposti e trasmessi da GB.
- **Mossa AIOS**: per gli F24 home banking, AIOS pre-registra **prima** del passo 5 (estrazione da home banking autorizzato o da scansione). Quando il contabile arriva al passo 5, l'F24 è già registrato → niente digitazione manuale.

### Visura camerale

- **Chi**: **segreteria** — onboarding nuovo cliente + aggiornamenti successivi (cambio sede, denominazione, amministratore).
- **Tempi**: variabili per adempimento.
- **Mossa AIOS**: AIOS estrae dati dalla visura PDF firmato CCIAA e propone aggiornamento anagrafica GB → riduce carico segreteria. Coerente col bus-factor parziale della segreteria ([[AIOS-Bus-Factor-Studio]]) sul cappello "rapporto enti".

### Variazione IVA (AA7/AA9)

- **Chi**: **segreteria** (compilazione modello + aggiornamento anagrafica GB).
- **Frequenza**: ≈ **20/anno**.
- **Mossa AIOS**: precompila il modello AA7/AA9 dai dati disponibili (visura, PEC AdE) e propone aggiornamento anagrafica GB **unico** → la segreteria fa una sola validazione invece di doppia digitazione (modello + anagrafica).
- **Canale invio**: misto Entratel + PEC (vedi [[AIOS-Firma-Deleghe-Procure-Cliente#6 Canale invio AA7 AA9 misto Entratel PEC]]).

### FatturaPA emessa

- **Chi**: **contabile assegnato del cliente** — prepara + trasmette a SDI (stessa persona).
- **Registrazione GB**: **integrata** (no manuale).
- **Volume**: ≈ **10 clienti** dello studio hanno questo servizio.
- **Mossa AIOS**: il flusso GB-side è già abbastanza fluido (registrazione integrata). Il valore AIOS è nella **preparazione** della fattura (raccolta dati cliente finale, calcolo importi, applicazione codice IVA per il regime cliente) più che nella registrazione.

## 5.2 Configurazione GB

| Aspetto | Stato | Note |
|---|---|---|
| Versione INTEGRATO GB | **Da rilevare al gate** | Non a memoria del titolare |
| Archivio dati | **SQL Server cloud GB** | Implicazione **forte**: integrazione AIOS↔GB via API/connettori cloud GB, non da `.mdb` locale |
| Identificazione ditte | **Per denominazione** (campo libero) | Probabile ambiguità su denominazioni simili → AIOS userà ID record interno di GB (da scoprire al gate), non la denominazione come chiave |
| Anagrafica multi-azienda | **Da verificare al gate** | Unica condivisa vs per-ditta vs misto |
| Contratto assistenza GB + area riservata | **Da verificare** | Da chiarire al gate o all'intervista [[AIOS-Intervista-Esperto-GBSoftware]] (2026-05-01) |

> [!warning] SQL Server cloud GB → integrazione via API
> Il punto **"archivio cloud"** sposta la modalità d'integrazione: niente accesso file `.mdb`. Va chiarito con GBSoftware se esistono API documentate, quale autenticazione, quale rate limit.

## 5.3 Import / export

| Funzione | Stato | Note |
|---|---|---|
| Funzioni di import in uso abituale | **xls + xml** | xls = movimenti banca al passo 5; xml = plausibilmente fatture passive XML SDI |
| Import anagrafica da XML in GB | **Da verificare al gate** | Se esiste, accelera onboarding cliente |
| Fatture elettroniche passive auto-importate | **NO** — trascrizione manuale | **Bersaglio numero uno della Fase B**: alto volume, pain meccanico, XML SDI strutturato → estrazione automatica robusta |

> [!danger] Fatture passive = bersaglio Fase B
> GB **non** importa nativamente le fatture passive. Pipeline AIOS:
>
> 1. Pesca dal cassetto fiscale AdE (passo 1 della quadratura — già automatizzato).
> 2. Estrazione XML SDI.
> 3. Generazione riga prima nota in GB via tracciato import (da verificare al gate).
> 4. Contabile valida (caso (b) della mappa meccanico/giudizio in [[AIOS-Processo-Quadratura-Trimestrale]]).

## 5.4 PDC e causali

| Aspetto | Stato | Note |
|---|---|---|
| Piano dei conti | **Misto**: PDC "tipo studio" per la maggior parte + PDC custom per i 3 archetipi fuori standard | AIOS gestisce **4 PDC base** (default + edilizia + notaio + farmacia) + eccezioni custom |
| Causali contabili | **Codici GB standard** | Mappa codici → significato in documentazione GB; AIOS la consulta dal dizionario standard senza dipendere da una persona |
| Persona di riferimento al gate | **Contabile società** | Custode delle prassi: quali causali standard usate di default per le registrazioni più frequenti, scelte di prassi non documentate |

## 5.5 Variazione IVA — decisione HITL (B3)

GB **non** ha tracciato nativo per la variazione IVA (è un modello AdE, non un evento contabile).

**Frequenza totale variazioni IVA**: non a memoria, riferimento provvisorio ≈ 20/anno (= AA7/AA9; potrebbero esserci altri tipi tipo cambio regime, opzione/revoca, contabilità separata, da quantificare). In ogni caso bassa frequenza.

**Decisione cablata**: **(a) HITL by design**. AIOS produce un **report leggibile e strutturato**, persona dello studio (segreteria) digita in GB. Pronto al go-live 10/05/2026, niente attesa per tracciato dedicato GB Software.

## 5.6 Sandbox per i test in Fase B

| Aspetto | Stato |
|---|---|
| Ditta di prova GB | **Già configurata** (taglia un blocco di setup al gate) |
| Backup automatico + rollback | **Da verificare al gate** |

> [!warning] Backup/rollback non confermati
> Finché non sappiamo se il rollback in GB cloud è banale o richiede manualità tecnica, i test sulla ditta di prova **vanno fatti con cautela** e con backup manuale prima di ogni run significativo.

## 5.7 Priorità — ranking writer Fase B

> [!success] Ranking deciso
> 1. **Visura → anagrafica GB** (priorità massima)
> 2. **Variazione IVA AA7/AA9**
> 3. **F24 telematico**
> 4. **FatturaPA emessa** (priorità minima)

**Logica del ranking**: i primi due liberano la **segreteria** (SPOF parziale dal [[AIOS-Bus-Factor-Studio]] sul cappello "rapporto enti"); F24 ha già parzialmente auto-registrazione GB; FatturaPA è già fluido lato GB (registrazione integrata).

**Quinto documento per sprint successivo**: **decisione rimandata** post-implementazione dei 4 writer (manca contesto sui colli di bottiglia residui dopo aver chiuso i primi 4).

## TODO da verificare al Gate A→B

Lista delle voci che richiedono accesso a GB durante la sessione di 60 min:

- [ ] Versione INTEGRATO GB attualmente installata
- [ ] Anagrafica multi-azienda: unica vs per-ditta vs mista
- [ ] Contratto assistenza GB + accesso area riservata GBSoftware (presenza/assenza, credenziali)
- [ ] Import anagrafica da XML: esiste in GB? Se sì, tracciato + funzionamento
- [ ] Tracciato import prima nota per fatture passive (formato richiesto da GB)
- [ ] ID record interno GB usabile come chiave univoca cliente (vs denominazione)
- [ ] Backup automatico + procedura rollback ditta di prova
- [ ] Mappa codici causali standard usati di default dallo studio (estrarla con il contabile società)

## Collegamenti

- [[AIOS-Intervista-Padre-Follow-Up]] — fonte (tema 5)
- [[AIOS-Intervista-Esperto-GBSoftware]] — sessione esperto (2026-05-01) per chiarire le voci "da verificare"
- [[AIOS-Processo-Quadratura-Trimestrale]] — i 4 writer si agganciano ai passi 2, 3, 5
- [[AIOS-Cliente-Fuori-Standard]] — i 4 PDC base servono i 3 archetipi
- [[AIOS-Firma-Deleghe-Procure-Cliente]] — il canale Entratel vs PEC entra nei writer AA7/AA9
- [[KR1.1 — Phase 10 GBSoftware completata]] — questo dossier alimenta il KR
- [[Sistema-Agentico-Studio]]
- [[Prodotto-Pillar-Delivery-Piloti]]
