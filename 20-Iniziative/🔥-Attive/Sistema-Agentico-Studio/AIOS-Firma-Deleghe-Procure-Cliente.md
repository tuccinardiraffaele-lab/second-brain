---
tipo: concetto
creato: 2026-05-03
aggiornato: 2026-05-03
stato: attivo
tags:
  - progetto/sistema-agentico
  - knowledge-studio
  - firma-deleghe
  - antiriciclaggio
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari:
  - "[[Strategia-Pillar-Monitoraggio-Regolatorio]]"
  - "[[Vendite-Pillar-Governance-Reputazionale]]"
forma_aggancio: input
sistema_owner: "[[Sistema-Agentico-Studio]]"
fonte: "[[AIOS-Intervista-Padre-Follow-Up]]"
---

# Firma cliente, deleghe, procure — perimetro cablato in AIOS

> [!info] In una frase
> AIOS cabla **blocchi hard** sugli output verso enti esterni quando manca firma cliente per atti dove la legge la richiede; cabla **non-blocco** dove la firma non è prevista; tratta come **zone grigie** i casi normativamente ambigui finché il founder non decide caso per caso.

> [!danger] Doppio aggancio pillar
> Questa nota tocca P3 (Delivery Piloti — primario), P7 (Monitoraggio Regolatorio — la materia è disciplinata da norma in evoluzione) e P4 (Governance Reputazionale — la compliance antiriciclaggio è non-negoziabile per la reputazione professionale).

## 1. I 17 atti normati (catalogo cablato)

Per ogni atto: **sì/no** lo fa lo studio, **frequenza**, **forma firma**.

### Area dichiarazioni e adempimenti AdE

| # | Atto | Studio | Frequenza | Firma cliente | Note |
|---|---|---|---|---|---|
| 1 | Dichiarazione IVA annuale | SÌ | Annuale | Cartacea | |
| 2 | Modello 770 sostituto d'imposta | SÌ | Annuale | Cartacea | |
| 3 | CU ordinaria sostituto verso AdE | SÌ | Annuale | Cartacea | |
| 4 | Dichiarazione IRAP | SÌ | Annuale | Cartacea | |
| 5 | Dichiarazione IMU cartacea | SÌ | Annuale | Cartacea | Solo se variazioni anno precedente |
| 6 | Istanza rimborso IVA (VR/TR) | SÌ | Annuale | Cartacea | Solo su richiesta cliente |
| 7 | Variazione P.IVA (AA7/AA9) | SÌ | Event-driven | Cartacea | Pratica chiusa entro 1 mese dalla scadenza |
| 8 | Istanza interpello (art. 11 L. 212/2000) | SÌ | Event-driven | Cartacea | Idem |
| 9 | Accertamento con adesione | SÌ | Event-driven | Cartacea | Idem |
| 10 | Conciliazione tributaria | SÌ | Event-driven | Cartacea | Idem |

### Area societaria / lavoro / compliance

| # | Atto | Studio | Frequenza | Firma cliente | Note |
|---|---|---|---|---|---|
| 11 | Deposito bilancio CCIAA (XBRL + verbale) | SÌ | Annuale | Firma digitale | |
| 12 | Verbale assemblea ordinaria | SÌ | Annuale | Firma digitale | |
| 13 | Verbale assemblea straordinaria | NO | — | — | Notarile, fuori studio |
| 14 | Pratica ComUnica/REA/SUAP | SÌ | Event-driven | Firma digitale | Pratica chiusa nel mese dall'arrivo |
| 15 | UNILAV (assunzione/cessazione dipendenti) | NO (EXT) | — | — | Consulente del lavoro esterno |
| 16 | Adeguata verifica antiriciclaggio (D.Lgs. 231/2007) | NO oggi → SÌ target | — | — | **Vedi sezione "Gap antiriciclaggio"** |
| 17 | Nomina DPO | NO | — | — | |

## 2. Gap antiriciclaggio — cablato fin dal go-live (γ)

> [!danger] AIOS forza la compliance dove c'è gap
> Oggi nei 10 clienti pilot l'**adeguata verifica clientela antiriciclaggio non è formalizzata**. Lo stato target dello studio (lettera (a) della tassonomia di intervista) è: identificazione + raccolta documenti come prassi interna, **con modulistica firmata**.
>
> Decisione cablata: AIOS al go-live tratta l'antiriciclaggio come **opzione (γ) — cablato fin dal go-live**. Per tutti i 10 pilot:
> - AIOS **genera modulistica adeguata verifica**.
> - AIOS **traccia firma cliente** sulla modulistica.
> - AIOS **blocca output verso enti** (AdE, CCIAA) finché la firma adeguata verifica non è caricata.
>
> Effetto sul prodotto: lo studio entra in compliance antiriciclaggio per via dell'adozione di AIOS. È un valore aggiunto B2C oltre l'efficienza.

## 3. Casi senza firma cliente per legge (cablato come "no blocco")

AIOS **non blocca** gli output per gli atti seguenti, perché la firma cliente non è richiesta dalla legge:

- **LIPE** (liquidazioni IVA periodiche) — firma digitale intermediario.
- **Esterometro / SDI** — firma SDI dello studio.
- **Intrastat** — firma digitale intermediario.
- **Ravvedimento operoso** — atto di comportamento, non di firma.
- **Pareri / perizie / attestazioni di revisione / certificazioni R&S** — firma del professionista. **Override manuale** ammesso: il contabile/titolare può comunque flaggare "richiedi firma cliente" per i casi dove il documento richiede autentica del professionista su firma cliente.
- **Lettera d'incarico professionale** — non obbligo di legge, prudenza professionale.

**Fuori scope studio (consulente del lavoro esterno)** — AIOS non se ne occupa:
- **UNIEMENS**.
- **Autoliquidazione INAIL**.

## 4. Delega unica AdE (D.Lgs. 1/2024 + Provvedimento direttoriale 02/10/2024)

> [!info] Cambio normativo che AIOS deve riflettere
> Dal 02/10/2024 la delega all'intermediario è **unica**: una sola operazione attiva tutte le deleghe (Cassetto Fiscale Delegato, Fatture e Corrispettivi, Equipro). **Durata 4 anni** (validità fino al 31/12 del quarto anno successivo all'attivazione, salvo revoca/rinuncia).

**Stato 10 clienti pilot**: tutti **migrati al nuovo regime**. AIOS al go-live cabla solo il regime nuovo.

**Logiche cablate in AIOS**:

1. Per ogni cliente: campo `delega_unica.data_attivazione` + calcolo automatico `delega_unica.data_scadenza` (= 31/12 del 4° anno successivo).
2. Reminder automatico al **2 ottobre** dell'ultimo anno di validità (data dalla quale può essere comunicato il rinnovo).
3. **Alert collettivo 28/02/2027** (logica generica per clienti futuri pre-2025): le deleghe attive al 05/12/2025 in regime transitorio cessano comunque al 28/02/2027 — AIOS segnala migrazione obbligatoria.
4. La delega unica copre tutti i servizi AdE → AIOS verifica **una sola data per cliente**, non una per adempimento.

**Fonte normativa**:
- D.Lgs. 1/2024, art. 21
- Provvedimento direttoriale AdE del 02/10/2024
- [La delega unica per l'utilizzo dei servizi online (AdE)](https://www.agenziaentrate.gov.it/portale/documents/d/guest/la_delega_unica_per_l-utilizzo_dei_servizi_online)
- [Schede — Delega unica ai servizi on line dell'AdE](https://www.agenziaentrate.gov.it/portale/delega-unica-ai-servizi-on-line-dell-agenzia-delle-entrate-e-dell-agenzia-delle-entrate-riscossione/che-cos-)

## 5. Procura speciale per AdE (art. 63 DPR 600/1973)

Procura per firmare al posto del cliente per istanze e atti verso AdE (rimborso IVA, interpello, accertamento con adesione, conciliazione).

**Modalità studio**: **procura ad hoc per ogni atto**, non procura ombrello generica.

**Logica AIOS cablata**: quando matura un atto di questa famiglia, AIOS attiva flusso "richiedi procura speciale al cliente" come pre-condizione, traccia firma e **blocca l'atto** finché la procura specifica non è caricata.

**Tipologia procura**: **sempre ordinaria** per accertamento con adesione. AIOS tratta una sola tipologia, niente branch ordinaria/autenticata.

## 6. Canale invio AA7/AA9 — misto Entratel + PEC

Lo studio usa entrambi i canali a seconda di cliente/urgenza. **AIOS cabla entrambi**.

**Regola di blocco**:
- **Entratel**: blocca se **manca delega unica** del cliente.
- **PEC istituzionale dello studio**: **non blocca** sull'assenza di delega unica (zona grigia normativa risolta in modalità permissiva — vedi sezione 7).

## 7. Zone grigie — decisioni cablate

| # | Zona grigia | Decisione cablata | Logica AIOS al go-live |
|---|---|---|---|
| 1 | **FEA su tablet** vale come firma autografa? | (c) Zona grigia | AIOS oggi non blocca su FEA, decisione rinviata all'esperienza |
| 2 | **Autotutela** richiede firma cliente? | (c) **Sempre obbligatoria** | AIOS blocca finché manca firma cliente sull'istanza di autotutela |
| 3 | **CU sintetica al percipiente** richiede firma del percipiente? | NO confermato | AIOS genera e consegna senza raccogliere firma del percipiente |
| 4 | **SUAP** — forma firma per Comune | (a) **Mappa Comune → forma firma** | AIOS popola progressivamente la mappa; al primo incontro con un Comune sconosciuto chiede al contabile e aggiunge la riga |
| 5 | **Adeguata verifica clientela a distanza** | (b) **Identificazione documentale a distanza** | AIOS cabla flusso "raccolta documenti identità (copia documento + selfie/videocall) + traccia archiviazione" come pre-condizione onboarding cliente a distanza |
| 6 | **PEC AA7/AA9 bypassa la delega unica?** | (b) **Permissivo** | AIOS blocca solo Entratel sull'assenza di delega unica; la PEC parte comunque (rischio normativo accettato per ridurre frizione) |

> [!question] Zona grigia 6 da risolvere quando l'AdE chiarisce
> La fonte AdE non dice esplicitamente se la PEC istituzionale dell'intermediario richieda comunque la delega unica. La decisione attuale è permissiva. Va riconsiderata se: (a) l'AdE chiarisce normativamente, (b) emerge una contestazione specifica.

## 8. Propagazione override (knowledge cross-cliente)

Quando il contabile corregge una classificazione AIOS spiegando il perché (es. "per cliente X le fatture del fornitore Y vanno su un conto specifico per servizio infragruppo"), AIOS può imparare la regola.

**Modalità decisa**: **(a) sistema propone estensione, contabile decide caso per caso**.

- Default: la regola **resta sul cliente specifico**.
- AIOS **propone l'estensione** ai clienti simili (stesso codice ATECO o stesso regime contabile).
- Il contabile/titolare **approva caso per caso** prima che la regola diventi cross-cliente.

**Implicazione tecnica**: data model AIOS deve avere `regola.scope ∈ {cliente_x, ateco_y, regime_z, studio}` con elevazione manuale.

## Collegamenti

- [[AIOS-Intervista-Padre-Follow-Up]] — fonte (tema 4)
- [[AIOS-Cliente-Fuori-Standard]] — i 3 archetipi possono interagire con override propagati
- [[AIOS-Gate-GBSoftware-Dossier]] — il canale Entratel vs PEC interagisce con i tracciati GB
- [[Sistema-Agentico-Studio]]
- [[Prodotto-Pillar-Delivery-Piloti]]
- [[Strategia-Pillar-Monitoraggio-Regolatorio]]
- [[Vendite-Pillar-Governance-Reputazionale]]
