---
tipo: concetto
creato: 2026-04-20
aggiornato: 2026-04-25
stato: attivo
tags:
  - pillar/strategico
  - vendite/sales
  - vendite/positioning
area: vendite
pillar-fase: Foundation
pillar-fase-num: 0
pillar-loss:
  - Vantaggio-asimmetrico-non-attivato
  - Capability-marketing-sales-mancante
---

# Pillar — Sales & Positioning

> [!info] In una frase
> Presidia la capability di vendere i due piloti (FT B2C, AIOS B2B+B2C) e l'attivazione del vantaggio asimmetrico Lean/corporate come leva di vendita, tenuti in bucket separati per non annegarli nel sales generico.

## Loss proprietarie

Il pillar possiede **due bucket distinti**. Il vantaggio asimmetrico è un asset *posseduto da attivare*, la capability M&S è una competenza *da costruire*. Segno opposto, tracking separato.

| Bucket | Loss | Natura |
|--------|------|--------|
| A | #5 Vantaggio asimmetrico Lean/corporate non attivato | Mancata attivazione di un asset esistente |
| B | #7 Capability marketing & sales mancante | Costruzione di capability da zero |

## Filosofia di esecuzione

Il bottleneck di M&S non è una variabile sola: è la triade **clarity + tooling + time-block**. Senza chiarezza sul bucket #1 ogni ora investita produce rumore; senza tooling LLM-leverage la chiarezza non scala oltre il founder; senza time-block scolpito + audit settimanale il filone evapora sotto la pressione AIOS. Le tre lenti operano simultaneamente — e [[Crescita-Priorità-Correnti#1. Presidio studio giuridico quotidiano|studio giuridico 1.5-2h/giorno]] è intoccabile in tutte e tre: precede il pillar.

## Bucket #1 attaccante (gate Foundation)

> [!success] Definizione operativa post-intervista padre
> **Clienti del padre del verticale commercio dettaglio medie dimensioni o società impiantistica, con storia recente di scadenze saltate, classificazioni voci errate, o lamentele su ritardi 730. Stima dimensione: ~10-15 clienti dei ~70 totali dello studio.**
>
> Pain quote da estrarre dal padre per evidenze Foundation: *"ritardo 730"*, *"scadenza saltata"*, *"classificazione voce X errata"*. Fonte: [[AIOS-Intervista-Padre-Domande-KB]] sezioni E (pain point) e F (criteri di qualità).
>
> **Messaggio testabile**: *"AI che protegge il rapporto, riduce le scadenze saltate e gli errori di classificazione, certificata dal titolare al ≥80% accuracy classificazione voci / ≥95% scadenze AdE pulite"* — soglie già stabilite in [[Decisione-Soglie-Pilot-AIOS]].
>
> Trigger di switch bucket: se a metà finestra Stability (~2026-12) il bucket #1 non ha prodotto ≥1 pain quote NUOVA da clienti padre concreti, o ≥0 prospect risponde a outreach v0 dopo 2 settimane → freeze Stability per 2 settimane di re-clarity sul bucket.

## Obiettivi di fase (4 end-state)

Sorgente: [[Brainstorm-Obiettivi-Fase-Sales-Positioning]] (2026-04-25).

| Fase | End-state |
|------|-----------|
| **0 Foundation** | Positioning Brief v1.0 versionato (≤4 pagine, KPMG-style snello) + bucket #1 attaccante chiarito + messaggio "compliant by design + AI per piccole realtà" che supera Test del placebo + tooling CRM+sequencer LLM attivo + parere fiscale terzo (non padre) sul contraente AIOS B2C entro 2026-07 + advisor terzo riformula ≥80% del brief al primo colpo |
| **1 Stability** | ≥3 cicli outbound consecutivi conformi al brief, eseguiti con tooling, su prospect qualificati ex-ante (no famiglia, no peer, decisore con budget verbale), con outcome di apprendimento misurato — non solo numero contatti |
| **2 Predictability** | ≥2 closure pagate B2C nel bucket #1 (firma + primo pagamento, NO LOI, NO parenti/amici, prezzo ≥75% del tier dichiarato) + pricing 3-tier pubblicato + playbook eseguibile da secondo operatore (founder fuori stanza) + contraente AIOS B2C disambiguato anche legalmente |
| **3 Agility** | Sales OS in cui ≥70% pipeline opera senza founder nel loop operativo + apertura B2B peer dopo firma abilitazione consulente del lavoro + dopo firma [[Vendite-Pillar-Governance-Reputazionale]] + iterazioni signal→revisione brief ≤6 settimane |

## Health check SMART per fase

### Foundation (time-bound 2026-09-30)

| ID | Misura | Soglia | Tipo |
|----|--------|--------|------|
| HC-F1 | Brief v1.0 esiste, versionato con changelog, ≤4 pagine | binario al 2026-09-30 | Leading |
| HC-F2 | 3 bucket × ≥2 evidenze esterne datate, di cui bucket #1 con ≥3 pain quote verbatim | **3+3+≥3 quote** | Leading |
| HC-F3 | Advisor terzo (no famiglia, no peer, no Angelini) riformula brief al primo colpo | **≥80%** | Lagging Foundation / Leading Stability |
| HC-F4 | Tooling CRM+sequencer LLM attivo con audit log, costo mensile | **da elicitare €30-100/mese** | Leading |
| HC-F5 | Parere fiscale terzo sul contraente AIOS B2C acquisito | **entro 2026-07-31** | Leading, gate Stability |

Goodhart: HC-F2 mitigato richiedendo che l'advisor riformuli in linguaggio cliente target, non in linguaggio brief. HC-F3 mitigato vincolando profilo advisor dichiarato ex-ante. HC-F1 mitigato facendolo gate Stability ("esiste ≠ usato").

### Stability (time-bound 2027-03-31)

| ID | Misura | Soglia | Tipo |
|----|--------|--------|------|
| HC-S1 | Prospect qualificati nel bucket #1 stretto (4 reali nel bucket > 5 mix) | **≥5** | Leading |
| HC-S2 | Prospect su 5 che richiedono **autonomamente** follow-up scritto post-discovery | **≥2** | Lagging |
| HC-S3 | Cicli outbound end-to-end via sequencer con audit a campione 2/5 conformi al brief | **≥3** | Lagging |
| HC-S4 | Decisioni founder (pricing/messaggio/perimetro) modificate, ognuna citante quote verbatim del prospect | **≥2** | Leading Predictability |
| HC-S5 | Playbook v1.0 trasferibile: 1 ciclo simulato eseguito da advisor terzo, founder fuori stanza | **1** | Leading Predictability |

Goodhart: HC-S1 mitigato con criterio bucket #1 stretto in Foundation + audit 2/5 verifica qualifica. HC-S2 mitigato con definizione stretta di "autonomamente" (nessun touch del founder nelle 72h precedenti). HC-S4 mitigato richiedendo quote verbatim per ogni cambio.

### Predictability (gate-event > gate-date, target 2027-12-31)

> [!warning] Gate-event vincolante
> ≥2 closure pagate B2C bucket #1. **Slittamento ammesso fino a 2028-03-31** SE Stability ha chiuso con ≥4 cicli conformi e bucket #1 confermato. Oltre 2028-03 trigger di revisione strategica.

| ID | Misura | Soglia | Tipo |
|----|--------|--------|------|
| HC-P1 | Closure pagate B2C bucket #1 (firma + primo pagamento) | **≥2** (gate-event) | Lagging |
| HC-P2 | Pricing 3-tier pubblicato + ≥1 tier scelto in autonomia dal cliente | **3 tier + ≥1 scelto** | Leading |
| HC-P3 | Playbook eseguibile da secondo: 1 ciclo intero senza founder in stanza, scostamento KPI | **<30%** | Lagging |
| HC-P4 | Decisioni pricing/perimetro modificate post-closure su feedback cliente pagante | **≥2** | Leading Agility |
| HC-P5 | Forecast accuracy: scostamento su pipeline trimestrale, dichiarato ex-ante non rivisto in corsa | **<30% su ≥1 trim** | Lagging |

Goodhart: HC-P1 mitigato con bucket #1 stretto + nessuna parentela/amicizia + prezzo ≥75% del tier. HC-P3 mitigato con founder fisicamente non presente + audit log sequencer come prova. HC-P5 mitigato con forecast scritto e versionato a inizio trim, non in corsa.

### Agility (time-bound 2029-Q3+, post-abilitazione)

| ID | Misura | Soglia | Tipo |
|----|--------|--------|------|
| HC-A1 | Pipeline senza founder in loop operativo (definizione "loop" pre-registrata in Predictability) | **≥70%** | Lagging |
| HC-A2 | Cicli signal→revisione brief/anno con cadenza ≤6 settimane | **≥4** | Leading |
| HC-A3 | Junior reale (non advisor) esegue 1 trimestre completo, scostamento KPI vs founder baseline | **<20%** | Lagging |
| HC-A4 | Decisioni strategiche M&S (pricing/bucket/messaggio/hire) prese da deputy senza escalation | **≥2/anno** | Lagging |

Goodhart: HC-A1 mitigato con definizione ex-ante in Predictability di cosa conta come "loop" (touchpoint cliente, decisione pricing, qualifica prospect). HC-A4 mitigato con definizione ex-ante di "strategiche".

## Target zero-loss sintetici

| Target | Finestra |
|--------|----------|
| Mesi senza Brief v1.0 versionato dopo 2026-09 | **= 0** |
| Bucket dichiarati senza criteri di esclusione | **= 0** |
| Cicli outbound senza audit a campione in Stability | **= 0** |
| Decisioni founder cambiate "a sensazione" senza quote verbatim | **= 0** |
| Closure conteggiate senza primo pagamento incassato | **= 0** |
| Apertura B2B peer prima della firma abilitazione + firma Pillar Governance | **= 0 assoluto** |
| Settimane in cui studio giuridico scende sotto 1.5h/giorno per attività Pillar A | **= 0** |

## Sub-step per avanzamento

- **0 → 1**: tutti gli HC Foundation verdi entro 2026-09-30 (criterio binario AND)
- **1 → 2**: HC-S1+S2+S3+S5 verdi + slot M&S sostenuto ≤3h/sett senza erosione studio giuridico
- **2 → 3**: gate-event ≥2 closure pagate + HC-P3 (playbook trasferibile) + abilitazione consulente del lavoro consolidata
- **3 → mantenimento**: cadenza ≤6 settimane iterazione brief + deputy attivo + bus-factor ≥2

## Stato corrente

- **Fase**: 0 Foundation — bucket riconosciuti in [[Strategia-Attuale]] ma value prop non scritta, advisor terzo non identificato, tooling non scelto
- **Slot M&S dichiarato**: ≤3h/sett, ritagliate da serale/weekend post-AIOS, **mai** da blocco studio giuridico
- **Deputy-of-record**: il padre, briefing trimestrale post-Foundation
- **TODO Foundation aperti**:
  - Scouting advisor terzo: 2-3 nomi entro 2026-06-30 (LinkedIn / network corporate fuori-pharma / coach M&S indipendenti)
  - Estrarre 3-5 pain quote verbatim dal padre su clienti del bucket #1
  - Scelta tooling CRM+sequencer (range €30-100/mese)
  - Avvio richiesta parere fiscale terzo per contraente AIOS B2C entro 2026-07

## Aggancio cross-pillar

- [[Vendite-Pillar-Governance-Reputazionale]] — pillar gemello sul confine reputazionale; Pillar A si ferma a B2C, ogni mossa B2B passa da Governance
- [[Strategia-Pillar-Monitoraggio-Regolatorio]] — cross-pillar B→A: messaging "compliant by design" entra nel Brief Foundation come asset commerciale anticipato
- [[Sistema-Agentico-Studio]] — i prospect AIOS B2C richiedono prodotto in produzione (gate go-live ~2026-05-10)
- [[Crescita-Pillar-Studio-Giuridico]] — abilitazione 2029 sblocca apertura B2B in Agility
- [[Prodotto-Pillar-Delivery-Piloti]] — soglie pilot AIOS (≥80% classificazione, ≥95% scadenze) sono argomento di vendita in Foundation

## Collegamenti

- [[Brainstorm-Obiettivi-Fase-Sales-Positioning]] — sorgente Sessione 1 + 2 (multi-agent deliberation 2026-04-25)
- [[Processo-Definizione-Obiettivi-Pillar]] — metodo applicato
- [[Pillar-Doppio-Livello]] · [[Zero-Loss-Mindset]] · [[Framework-Codificato-Per-Loss]]
- [[AIOS-Intervista-Padre-Domande-KB]] — fonte pain quote bucket #1
- [[Decisione-Soglie-Pilot-AIOS]] — soglie ≥80% / ≥95% riusabili come prove di vendita
- [[Strategia-Attuale#I quattro filoni paralleli]] — filone 4
- [[Identità]] · [[Angelini-Pharma]] — origine vantaggio asimmetrico (bucket A)
- [[OKR-Correnti]] · [[Crescita-Priorità-Correnti]]
