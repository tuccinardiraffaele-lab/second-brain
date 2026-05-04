---
tipo: progetto
creato: 2026-04-19
aggiornato: 2026-05-03  # esecuzione + trascrizione
stato: attivo
tags:
  - progetto/sistema-agentico
  - azione-aperta
  - intervista
  - chiuso
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
prossima_azione: ""
blocco: ""
---

# Seconda intervista padre — follow-up KB

> [!info] Contesto
> La prima intervista ([[AIOS-Intervista-Padre-Domande-KB]]) del 2026-04-19 ha chiuso le metriche pilot (vedi [[KR1.2 — Metriche pilot fissate con padre]]) ma ha lasciato tre aree sotto-approfondite che servono prima del go-live del ~10 maggio 2026.

## Calendario

| Data | Attività |
|---|---|
| **2026-04-25** | Pianificare la sessione: fissare orario, confermare con padre, preparare domande specifiche |
| **2026-04-26** | Esecuzione seconda intervista |

## Temi da approfondire

### 1. Bus-factor per singola persona

Prima intervista (D15) ha risposto in modo generico ("il contatto con la clientela e la contabilità periodica"). Serve mappare il rischio persona per persona sulle **quattro posizioni** ([[AIOS-Intervista-Padre-Domande-KB|D14]]):

- **Titolare** — se salta 1 settimana, cosa si blocca? 1 mese?
- **Contabile società** — stessa domanda
- **Contabile privati** — stessa domanda
- **Segreteria** — stessa domanda

Obiettivo: identificare i **single point of failure** e capire dove AIOS può fungere da backup di competenza.

### 2. Cliente "fuori standard" che dà più lavoro

Prima intervista (A2) ha mappato il cliente tipo (commercio al dettaglio medio + impiantistica) ma non ha isolato il cliente **anomalo** che assorbe tempo sproporzionato. Serve per capire se il pilot deve progettarsi sul caso standard o prevedere branch per casi particolari.

Domande:
- Chi è (o che profilo ha) il cliente fuori standard tipico?
- Cosa lo rende faticoso (volumi, documenti caotici, richieste ad hoc, settore normato)?
- Quanto tempo assorbe in proporzione al peso economico?

### 3. Processo di quadratura trimestrale (pain #1) — MECE

È il pain emerso **tre volte** (E17, E18, E19) e la soglia 1 del pilot ("quadratura trimestrale entro fine mese successivo") dice che AIOS deve aiutare proprio lì. Oggi nel vault la quadratura è una black box: servono **i passi operativi**.

Domande (stile mappatura Lean):
- Per una contabilità ordinaria tipo, qual è la **sequenza di passi** dalla ricezione documenti del trimestre fino alla quadratura chiusa?
- Chi fa ciascun passo (titolare, contabile, segreteria, cliente)?
- Quanto dura tipicamente ciascun passo?
- Dove si **blocca** di solito (attesa documenti cliente, dubbio di classificazione, confronto con GBSoftware, conferma titolare)?
- Quali passi sono **meccanici** (candidati automazione) vs **di giudizio** (candidati assistenza)?

Obiettivo: distinguere ciò che AIOS può automatizzare da ciò che può solo accelerare con assistenza, evitando di sovrastimare o sottostimare il valore del sistema al go-live.

## Criterio di chiusura

La seconda intervista si considera chiusa quando nel vault esistono:

- Una nota o sezione **bus-factor studio** con mappa persona→impatto
- Una nota su **cliente fuori standard** con profilo e peso operativo
- Una nota (o aggiornamento CBA) sul **processo quadratura trimestrale** con passi, attori, durate, punti di blocco

## Collegamenti

- [[AIOS-Intervista-Padre-Domande-KB]] — prima intervista (fonte dei gap)
- [[AIOS-Chiarire-Metriche-Pilot]] — soglia 1 quadratura, dipende dal processo mappato qui
- [[Sistema-Agentico-Studio]]
- [[OKR-Correnti]]

### 4. Firma del cliente, deleghe, procure — quando servono per legge

> [!info] Perché serve
> AIOS sta per essere cablato in modo che certi output non possano partire (essere depositati, trasmessi all'AdE, inviati al cliente) finché il cliente stesso non ha firmato. La regola la stai imponendo tu (D27 della prima intervista): per dichiarativi e bilanci serve sempre colloquio + firma prima di proseguire. Per cablare la regola in modo corretto sull'altro lato (oltre dichiarativi e bilanci) ho fatto un giro di ricerca normativa e ne è uscita una lista di 17 atti per cui la firma del cliente è obbligatoria per legge italiana 2026. Ti chiedo di guardare la lista insieme e dirmi quali stai effettivamente facendo nello studio, quali invece non capitano mai, e se ci sono casi in cui la prassi in studio chiede una firma che la legge non impone (= firma per prudenza, non per legge).

#### 4.1 Conferma dei 17 atti — riga per riga

Riprendiamo la lista e per ognuno di questi mi confermi: lo fate voi in studio? con che frequenza? la firma del cliente la prendete sempre o ci sono scorciatoie ammesse?

**Area dichiarazioni e adempimenti AdE:**
1. Dichiarazione IVA annuale
2. Modello 770 del sostituto d'imposta
3. CU ordinaria del sostituto verso AdE (la sintetica al percipiente la diamo per assodato che NON richiede firma — confermi?)
4. Dichiarazione IRAP
5. Dichiarazione IMU cartacea
6. Istanza di rimborso IVA (VR/TR)
7. Variazione P.IVA (AA7/10, AA9/12)
8. Istanza di interpello (art. 11 L. 212/2000)
9. Accertamento con adesione (firma duplice contribuente + capo ufficio)
10. Conciliazione tributaria

**Area societaria/lavoro/compliance:**
11. Deposito bilancio CCIAA (XBRL + verbale di approvazione)
12. Verbale assemblea ordinaria
13. Verbale assemblea straordinaria (atto pubblico notarile)
14. Pratica ComUnica/REA/SUAP
15. UNILAV (assunzione/cessazione dipendenti) — questo lo fate voi o passa al consulente del lavoro esterno?
16. Adeguata verifica clientela antiriciclaggio (D.Lgs. 231/2007)
17. Nomina DPO

Per ognuno: **lo facciamo SÌ/NO**, e se sì, **come prendete oggi la firma** (cartacea da firmare in studio? digitale via SPID o firma digitale? PEC? a casa del cliente?).

#### 4.2 Casi che AIOS può saltare

Ho già identificato per ricerca normativa una lista di output che la legge **non** richiede di far firmare al cliente, anche se l'errore comune è prenderle per prudenza. Ti chiedo conferma che voi non chiediate la firma del cliente per:

- **LIPE** (liquidazioni IVA periodiche) — basta la firma digitale dell'intermediario sul file
- **Esterometro/SDI** — firma SDI dello studio, no firma cliente
- **Intrastat** — firma digitale intermediario
- **UNIEMENS, autoliquidazione INAIL** — telematica intermediario
- **Ravvedimento operoso** — atto di comportamento, non di firma
- **Pareri scritti, perizie, attestazioni di revisione, certificazioni crediti d'imposta R&S** — firma del professionista, non del cliente
- **Lettera d'incarico professionale** — non è obbligo di legge, prudenza professionale

Se in qualcuno di questi tu o i tuoi chiedete comunque la firma del cliente, ditemelo e me lo segno come "firma prudenziale" — la teniamo nel processo ma non la cabliamo come blocco di sistema (perché bloccherebbe troppe pratiche).

#### 4.3 Mandato di trasmissione telematica — ogni quanto si rinnova?

Tutto ciò che mandi all'AdE per via Entratel passa dall'intermediario (lo studio) e richiede dal cliente una **delega scritta alla trasmissione** (art. 3 c. 6 DPR 322/1998). La legge non specifica una scadenza fissa.

Domande:
- Oggi nello studio, **ogni quanto rinnovate** la delega di trasmissione? Una volta a vita? Una volta all'anno per ogni dichiarazione? Una volta all'anno per tutto il pacchetto fiscale del cliente?
- Quando un cliente nuovo arriva da voi, **quale documento di delega gli fate firmare** in onboarding?
- Per il pilot: i 10 clienti pilota hanno tutti già una delega di trasmissione attiva e in corso, oppure dobbiamo prevedere che AIOS stesso solleciti la prima firma?

Mi serve per decidere se AIOS deve trattare la delega come "una volta firmata, vale per tutto" oppure "verifica per ogni anno fiscale".

#### 4.4 Procura speciale per AdE (art. 63 DPR 600/1973)

Questa è la procura che permette al commercialista di firmare al posto del cliente per istanze e atti verso AdE — rimborso IVA, interpello, accertamento con adesione, conciliazione, ecc.

Domande:
- Per i 10 clienti pilota, **avete già procure speciali depositate** o per ogni atto chiedete una procura ad hoc?
- Per l'accertamento con adesione, la legge prevede sia la **procura ordinaria** sia la **procura autenticata** (se il cliente delega un CAF). La differenza nella pratica per il vostro studio è rilevante? Cioè: AIOS deve sapere se la procura è ordinaria vs autenticata, oppure le tratti come una cosa sola?

#### 4.5 PEC verso AdE per variazione P.IVA (AA7/AA9)

Il modello AA7/AA9 è uno dei pochi che si può mandare via PEC istituzionale all'AdE invece che via Entratel. Domanda: quando lo mandi via PEC come professionista delegato, **serve comunque la delega di trasmissione**? Oppure la PEC è un canale "esente"? Mi serve per capire se AIOS deve verificare la delega anche prima di un invio PEC o solo prima di un invio Entratel.

#### 4.6 Casi grigi (li tengo fuori dal sistema finché non sciogli il dubbio)

Ci sono cinque punti di prassi italiana dove la legge non è chiara o dove il provvedimento attuativo lascia margine. **Su questi NON cablerò un blocco automatico in AIOS** finché non mi confermi tu come trattarli:

1. **FEA (Firma Elettronica Avanzata) su tablet** — vale come firma autografa per gli adempimenti fiscali oppure no? Cioè: se faccio firmare il cliente sul tablet con sistema FEA, AIOS lo deve accettare come firma valida o pretenderlo cartaceo?
2. **Autotutela** — la prassi AdE chiede la firma del cliente, ma nessuna norma la sanziona di nullità. La trattiamo come "firma da chiedere ma non blocco" o come "non chiediamo proprio"?
3. **CU sintetica al percipiente** — confermi che NON richiede firma del percipiente (è il certificato che il sostituto consegna al lavoratore/professionista)?
4. **SUAP** — la forma firma cambia da Comune a Comune. Per i clienti del pilot, di che Comuni parliamo? AIOS deve avere una mappa Comune → forma firma?
5. **Adeguata verifica clientela a distanza** — i provvedimenti UIF 2025-2026 hanno aggiornato le soglie. Come fate oggi l'identificazione del cliente che non viene fisicamente in studio?

#### 4.7 Override umano — come si propaga la conoscenza fra clienti simili

Quando AIOS classifica un documento e tu (o un collaboratore) lo correggi spiegando il perché (es. "per questo cliente le fatture del fornitore X vanno sempre su un conto specifico perché è un servizio infragruppo"), AIOS può imparare quella regola. La domanda è: vuoi che la regola **resti solo su quel cliente** (più sicuro, ma 50 clienti con lo stesso caso = 50 correzioni manuali) o vuoi che il sistema **ti proponga di estenderla** ai clienti simili (stesso regime contabile o stesso codice ATECO) e tu approvi caso per caso?

La nostra ipotesi attuale: **il sistema ti propone, tu decidi caso per caso**. Confermi?

### 5. Gate A→B GBSoftware — preparazione sessione operativa

> [!info] Perché serve
> AIOS sta per generare 4 file di output verso GB (F24 telematico, anagrafica da visura, report variazione IVA, FatturaPA emessa). Per chiudere la **Fase B** dello sprint parser servirà una sessione di 60 min davanti a GB (Gate A→B) — vedi piano `s-non-ti-preoccupare-partitioned-pond.md`. La prima intervista ha escluso l'operatività GB ("coperta separatamente con la persona che se ne occupa"): qui chiedo solo le cose che **tu titolare puoi dirmi senza accendere GB**, così quando ci troviamo davanti al gestionale partiamo già con il 70% delle domande risolte.

#### 5.1 Workflow attuale dei 4 documenti — chi fa cosa, oggi

Per ognuno dei 4 documenti, vorrei capire **come oggi li gestite in studio senza AIOS**, perché AIOS deve sostituire il pezzo meccanico e lasciare a voi il pezzo di giudizio.

1. **F24 telematico** — quando arriva (cliente che lo paga in home banking? predisposto da voi?), chi lo registra in GB, lo digitate a mano nella prima nota o c'è un import? In quanti minuti tipici si chiude un F24?
2. **Visura camerale** (apertura nuovo cliente o aggiornamento) — chi tipicamente la richiede in CCIAA, chi inserisce/aggiorna l'anagrafica in GB, in che momento del processo (è la segreteria a farlo in onboarding, o capita anche dopo)? Quanto tempo si perde tipicamente in questo passaggio?
3. **Variazione IVA (AA7/AA9)** — quando capita (apertura, chiusura, cambio regime, cambio sede), chi compila il modello, chi aggiorna l'anagrafica GB di conseguenza, chi gestisce il deposito? Quante variazioni IVA all'anno gestisce lo studio in totale (stima)?
4. **FatturaPA emessa** (es. fatture che lo studio emette per conto del cliente come servizio aggiuntivo — emerso in [[AIOS-Intervista-Padre-Domande-KB|D7]]) — chi prepara, chi trasmette a SDI, come la registrate in GB sul registro IVA del cliente? Quanti clienti circa hanno questo servizio?

#### 5.2 Configurazione GB — quello che sai a memoria

5. Versione INTEGRATO GB attualmente in uso (numero release o anno).
6. Archivio dati: Access locale (`.mdb`) o SQL Server? Se SQL, è server di studio o cloud GB?
7. Multi-azienda: GB identifica le ditte con codice numerico, alfanumerico, denominazione? Esiste un'unica anagrafica condivisa fra ditte o ogni ditta ha la sua?
8. Lo studio ha **contratto di assistenza GB attivo** + accesso area riservata GBSoftware? È da lì che si scaricano la documentazione tracciati e gli aggiornamenti.

#### 5.3 Import/export — cosa si fa già, cosa è solo manuale

9. Esiste in GB **almeno una funzione di import da file** che lo studio usa abitualmente (anagrafica, prima nota, F24, fatture)? Se sì, quale? Se no, **tutto è digitazione manuale**?
10. Hai mai sentito parlare di **import anagrafica da XML** in GB? Lo avete mai usato o è una funzione che esiste sulla carta ma in studio non la tocca nessuno?
11. Per le **fatture elettroniche passive** (XML SDI ricevuti dai fornitori dei clienti), GB le importa nativamente generando la prima nota, o qualcuno deve trascrivere?

#### 5.4 Codici causali e piano dei conti — chi li conosce

12. Lo studio usa il **piano dei conti standard GB** o uno personalizzato cliente per cliente? Se personalizzato, esiste un PDC "tipo studio" replicato su tutti?
13. Le **causali contabili** (es. "Fattura emessa", "Pagamento F24", "Pagamento INAIL", "Versamento IVA periodica") sono codici GB standard o codici interni dello studio? Chi è la persona di riferimento che conosce a memoria i codici causali usati di default — tu, contabile società, contabile privati, segreteria?
14. Per AIOS l'output dovrà contenere il codice causale corretto altrimenti GB rifiuta l'import: chi è la persona giusta da coinvolgere quando arriviamo al gate per estrarre la mappa codici → significato?

#### 5.5 Variazione IVA — decisione HITL (B3)

> [!info] Perché te lo chiedo prima del gate
> GB Software **non ha un tracciato nativo per la variazione IVA** (è un modello AdE, non un evento contabile). Abbiamo due strade per la Fase B: (a) AIOS produce solo un **report leggibile** che il contabile usa come promemoria per aggiornare a mano l'anagrafica GB — pronto subito, zero attesa; (b) apriamo un canale formale con GB Software per chiedere un tracciato dedicato — settimane/mesi di attesa per una funzione che si usa poche volte l'anno.

15. Stima **frequenza variazioni IVA** all'anno nello studio (≈ 5? ≈ 20? ≈ 50?).
16. È accettabile che AIOS lasci alla persona dello studio la digitazione finale in GB, fornendo un **report già strutturato e completo** (cioè HITL by design)? O preferisci che insistiamo per un tracciato nativo?

#### 5.6 Sandbox per i test in Fase B

17. Esiste già una **ditta di prova** in GB usata per testare cose nuove, oppure ne creiamo una al momento durante il gate? Importante: i test della Fase B **non possono toccare ditte reali**.
18. Backup automatico del database GB attivo? In caso un test rompesse qualcosa, **rollback è banale o richiede manualità tecnica**?

#### 5.7 Priorità — quale dei 4 sblocca più valore

19. Tra i 4 documenti, mettendoli in ordine, **quale ti farebbe risparmiare più tempo se automatizzato per primo**? F24, Visura, Variazione IVA, FatturaPA emessa — ranking 1-4. Serve per decidere quale writer raffinare per primo dopo il gate, se i tempi della Fase B fossero stretti.
20. C'è un **quinto documento ricorrente** che oggi è la stessa categoria di rumore (estrazione + ingresso GB) e che dovremmo aggiungere allo sprint successivo? (Es. modello Unico, LIPE, LUL paghe, dichiarazioni IVA periodiche, certificazione unica.)

## Criterio di chiusura — aggiornamento

La seconda intervista si considera chiusa quando nel vault, oltre alle 3 note già previste, esistono:

- Una sezione **firma cliente per atto** con conferma del catalogo dei 17 atti (quali sì/no, frequenza, forma firma in studio)
- Una decisione su **rinnovo mandato di trasmissione** (annuale, per dichiarazione, una volta a vita)
- Una decisione sulle **5 zone grigie** (FEA tablet, autotutela, CU sintetica, SUAP, adeguata verifica a distanza)
- Una decisione sulla **propagazione degli override** (per-cliente vs proposta sistemica)
- Un **dossier preparatorio Gate A→B GB**: workflow attuale dei 4 documenti, configurazione GB nota, persona di riferimento per codici causali, decisione HITL Variazione IVA, ranking di priorità tra i 4 documenti


## Esito intervista — 2026-05-03

> [!success] Intervista chiusa, trascrizione completata
> Tutti i criteri di chiusura della nota soddisfatti. Le 5 note di output sono state scritte nel vault e linkate dalla MOC [[Sistema-Agentico-Studio]] nella sezione "Knowledge studio del padre (intervista 2026-05-03)".

### Note di output prodotte

- [[AIOS-Bus-Factor-Studio]] — mappa persona→impatto sulle 4 posizioni (tema 1)
- [[AIOS-Cliente-Fuori-Standard]] — 3 archetipi (edilizia, notaio, farmacia) tutti dentro pilot (tema 2)
- [[AIOS-Processo-Quadratura-Trimestrale]] — sequenza 8 passi + colli di bottiglia 5 e 7 (tema 3)
- [[AIOS-Firma-Deleghe-Procure-Cliente]] — 17 atti + delega unica + 6 zone grigie + antiriciclaggio cablato (tema 4)
- [[AIOS-Gate-GBSoftware-Dossier]] — dossier preparatorio Gate A→B (tema 5)

### Decisioni cablate emerse durante l'intervista

- **Pilot stressa il sistema, niente "v2"**: i 3 archetipi fuori standard entrano nel pilot fin dal go-live. Salvata memoria globale `feedback_pilot_no_semplificazioni`.
- **Antiriciclaggio cablato (γ) fin dal go-live**: AIOS forza la compliance D.Lgs. 231/2007 dove oggi c'è gap; modulistica + firma cliente + blocco output verso enti se firma manca. Vedi [[AIOS-Firma-Deleghe-Procure-Cliente#2 Gap antiriciclaggio cablato fin dal go-live]].
- **Delega unica AdE (D.Lgs. 1/2024)**: tutti i 10 pilot già migrati al regime nuovo (4 anni). AIOS cabla solo regime nuovo.
- **Bersaglio numero uno Fase B GB**: import fatture passive (GB non importa nativamente, oggi trascrizione manuale).
- **Ranking writer Fase B**: Visura (1°) → Variazione IVA (2°) → F24 (3°) → FatturaPA (4°), logica "libera la segreteria".

### Voci da verificare al Gate A→B GBSoftware

Vedi [[AIOS-Gate-GBSoftware-Dossier#TODO da verificare al Gate A B]] — versione INTEGRATO, anagrafica multi-azienda, contratto assistenza + area riservata, import anagrafica XML, tracciato import prima nota, ID record interno cliente, backup/rollback, mappa codici causali standard.
