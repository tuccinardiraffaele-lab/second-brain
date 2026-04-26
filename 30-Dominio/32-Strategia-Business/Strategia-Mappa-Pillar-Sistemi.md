---
tipo: concetto
creato: 2026-04-25
aggiornato: 2026-04-25
stato: attivo
tags:
  - strategia/mappa
  - pillar/foundation
  - concetto/p-g-iws
area: strategia
---

# Mappa pillar↔sistemi

> [!info] In una frase
> Mappa concreta che aggancia ciascuno dei 7 pillar strategici ai sistemi operativi che ne presidiano la loss, con I/O dichiarato per ogni sistema. Chiude **HC-F4 Foundation** del pillar [[Strategia-Pillar-Leadership-Strategica]] (subordinatamente alla promozione a forma canonica dei 3 sistemi parziali).

## Origine

Definita il 2026-04-25 via architettura **multi-agent** (5 research consulenziali Sonnet stile McKinsey/BCG/Accenture/EY/Kearney → 3 explore vault Sonnet → fact-check Opus → deliberation room 5 voce Sonnet con moderatore Opus). Variante del [[Processo-Definizione-Obiettivi-Pillar]] applicata alla costruzione di un artefatto cross-pillar invece che alla definizione di obiettivi di fase di un singolo pillar.

Forma canonica del sistema applicata: input + output + processo + owner operativo + agganci pillar (vedi [[Sistemi-Sotto-Pillar]]).

## I 7 pillar e le 8 loss

| Pillar | Loss proprietaria | Note |
|---|---|---|
| [[Strategia-Pillar-Leadership-Strategica\|P1 Leadership Strategica]] | #1 Finestra-competitiva-persa | governance del sistema strategico |
| [[Prodotto-Pillar-Delivery-Piloti\|P2 Delivery Piloti]] | #8 Maturità-piloti-non-in-tempo | esecuzione tecnica dei piloti |
| [[Vendite-Pillar-Governance-Reputazionale\|P3 Governance Reputazionale]] | #2 Contaminazione-relazione-studio-clienti | zero-loss assoluto |
| [[Vendite-Pillar-Sales-Positioning\|P4 Sales & Positioning]] | #5 Vantaggio-asimmetrico-non-attivato + #7 Capability-marketing-sales-mancante | **doppia loss** segregata in 2 sotto-output |
| [[Crescita-Pillar-Studio-Giuridico\|P5 Studio Giuridico]] | #3 Identità-consulente-del-lavoro-non-costruita | gate critico orizzonte 2029 |
| [[Relazioni-Pillar-Network-Target\|P6 Network Target]] | #4 Networking-target-non-coltivato | classificato Complex (Cynefin) |
| [[Strategia-Pillar-Monitoraggio-Regolatorio\|P7 Monitoraggio Regolatorio]] | #6 Rischio-regolatorio-non-monitorato | controllo zero, monitoraggio obbligato |

## Mappa per pillar

### P1 — Leadership Strategica

> [!info] Loss presidiata
> #1 Finestra-competitiva-persa

1. **Review Cadence** ★ — *esistente, codificata* in [[Processo-Review-Cadence]]
	- I/O: stato pillar+OKR+brain locali → verbali weekly/monthly/quarterly + trigger correttivi
	- Owner: slot weekly venerdì + chiusura mese
	- Agganci: **P1 primario**, S su tutti gli altri 6 pillar
2. **Cost Deployment** — *da costruire da zero*
	- I/O: richieste capacity vs filoni → decisione allocazione + registro rinunce con costo atteso
	- Owner: trigger event-driven + check mensile in Review
	- Agganci: **P1 primario**, P2 consumer
	- Riferimento: [[Processo-Cost-Deployment]] (principio già descritto, sistema operativo da costruire)
3. **Pianificazione Giornaliera** ★ — *esistente, codificata* in [[Processo-Pianificazione-Giornaliera]] (promossa a forma canonica 2026-04-25)
	- I/O: MIT serale + calendario → time-block diario + microattività ripianificate
	- Owner: slot serale (compilazione) + skill `/daily` mattutina
	- Agganci: **P1 primario**, S su P5 e P2
	- Riferimento: [[Processo-Pianificazione-Giornaliera]], [[Decisione-Sistema-Pianificazione-Giornaliera]]
4. **Studio AI quotidiano** — *da costruire (sistema sistematico, non intermittente)*
	- I/O: fonti AI accreditate → capture in vault + segnali tecnici/competitivi
	- Owner: slot giornaliero da dichiarare nel time-block
	- Agganci: **P1 primario**, S su P2 (input opportunità tecniche piloti) e S su P7 (segnali competitivi → sistema di scouting implicito)
5. **Cattura & Retrieval Info** ★ — *esistente, codificata* in [[Processo-Cattura-E-Retrieval-Informazioni]] (promossa a forma canonica 2026-04-25)
	- I/O: insight/decisione/concetto/riferimento esterno → nota canonica nel territorio + retrieval semantico on-demand
	- Owner: founder (cattura event-driven) + Claude Code (triage in apertura sessione + retrieval) + skill di territorio
	- Agganci: **P1 primario**, S su tutti gli altri 6 pillar (perno cross-pillar simmetrico a Review Cadence)

### P2 — Delivery Piloti

> [!info] Loss presidiata
> #8 Maturità-piloti-non-in-tempo

1. **Quality Pillar Coding** ★ — *esistente* in [[Processo-Quality-Pillar-Coding]]
	- I/O: feature/bugfix → acceptance criteria + similarità ≥99% + defect register
	- Owner: gate ogni implementazione, skill `/quality-pillar`
	- Agganci: **P2 primario**, S su P3 (gate output verso clienti studio), S su P1
2. **UPS Troubleshooting** — *esistente* in [[Troubleshooting-UPS-Coding]]
	- I/O: bug/anomalia → causa radice evidence-based + fix verificato
	- Owner: trigger su debug, skill `/troubleshooting-ups`
	- Agganci: **P2 primario**, S su P3
3. **Knowledge Management Coding** — *esistente* in [[Processo-Knowledge-Management-Coding]]
	- I/O: sessioni coding → OPL/CBA in `.brain/` + promozione vault
	- Owner: pre-sessione (lettura) + intra-sessione (scrittura)
	- Agganci: **P2 primario**
4. **Validazione Pilot** ★ — *esistente, codificata* in [[Processo-Validazione-Pilot]] (promossa a forma canonica 2026-04-25)
	- I/O: output piloti in produzione → verdetto vs soglie pre-dichiarate ([[Decisione-Soglie-Pilot-AIOS]])
	- Owner: trigger su finestre osservazione (FT weekend, AIOS post-go-live)
	- Agganci: **P2 primario**, S su P1 (feed Cost Deployment)

### P3 — Governance Reputazionale

> [!info] Loss presidiata
> #2 Contaminazione-relazione-studio-clienti — zero-loss assoluto

1. **Policy Cross-Selling** — *da costruire*
	- I/O: opportunità su cliente studio → ammesso/rifiutato + perimetro + gate Quality Pillar + escalation
	- Owner: gate event-driven + revisione trimestrale in Review Cadence
	- Agganci: **P3 primario**, S su P4 (vincoli pipeline B2C), S su P2 (gate qualità output)
	- Nota: include la regola binaria minima "nessun output AIOS al cliente del padre senza Quality Pillar superato" anche per il pilot non commerciale (loss #2 si attiva indipendentemente dalla vendita)
2. **Decision Tree Escalation casi ambigui** — *Stability* (rinviato)
	- 1 checkpoint: "questa azione è visibile a un peer professionale o a un cliente dello studio?" → escalation
	- Interim: "in dubbio, escalation a padre"

### P4 — Sales & Positioning

> [!info] Loss presidiate (segregate)
> Sotto-output #5 = Posizionamento (vantaggio asimmetrico) · Sotto-output #7 = Capability marketing/sales

#### Sotto-output #5 — Posizionamento

1. **Positioning Brief** — *da costruire (Foundation entro 2026-05-31)*
	- I/O: identità + vantaggio Lean+AI + soglie pilot + pain quote padre → documento ≤4 pagine versionato
	- Owner: drafting ≤3h/sett serale-weekend + update trimestrale
	- Agganci: **P4 primario**, S su P6 (input narrativa network), S su P3
	- Riferimento: già descritto in [[Vendite-Pillar-Sales-Positioning]]

#### Sotto-output #7 — Capability

2. **Outbound Pipeline** — *Stability (Q3 2026)*
	- I/O: mappa network qualificato + Brief → sequenza contatti + audit log + decisioni con quote verbatim
	- Owner: slot M&S ≤3h/sett post-go-live AIOS
	- Agganci: **P4 primario**, S su P6, S su P3
3. **Capability Building Marketing-Sales** — *KR3.2 conferma decisione apertura filone in Q2 2026*
	- I/O: gap dichiarato → piano formativo + fonti
	- Agganci: **P4 primario**

### P5 — Studio Giuridico

> [!info] Loss presidiata
> #3 Identità-consulente-del-lavoro-non-costruita

1. **Studio Quotidiano Giuridico** ★ — *attività esistente, da formalizzare a sistema*
	- I/O: piano accademico + materiali → progresso esami + capture concetti in vault
	- Owner: time-block 1.5-2h/giorno lun-ven NON negoziabile (guardrail di sistema cross-pillar)
	- Agganci: **P5 primario**, S su P4 (input identità professionale), S su P3 (legittimità ruolo consulente, gate praticantato 2027-12)

### P6 — Network Target

> [!info] Loss presidiata
> #4 Networking-target-non-coltivato

1. **Mappa Network Bootstrap** ★ — *esistente, codificata* in [[Relazioni-Network-Mappa-Bootstrap]] (drafting iniziale 2026-04-25)
	- I/O: contatti esistenti + target → mappa segmentata MECE (mentor/peer/potenziali venditori-partner/off-limits) in `30-Dominio/39-Relazioni-e-Network/`
	- Owner: drafting one-shot + update event-driven
	- Agganci: **P6 primario**, S su P3, P4, P7
2. **Network Probe Loop** — *Stability (Q3 2026)*
	- Trigger: dopo ≥60gg di osservazione sulla Mappa Bootstrap
	- Agganci: **P6 primario**

### P7 — Monitoraggio Regolatorio

> [!info] Loss presidiata
> #6 Rischio-regolatorio-non-monitorato

1. **Sentinella Garante Regolatoria** — *da costruire (Foundation entro 2026-05-31)*
	- I/O: 2-3 fonti regolatorie + segnali competitivi (estensione esplicita) → alert event-driven + nota datata in vault
	- Owner: trigger automatico (alert) + slot sabato 30min (sentinella) + 60min/mese review
	- Agganci: **P7 primario**, S su P1 (input Studio AI quotidiano per segnali competitivi)
2. **Una-tantum Legale Ibrida P7+P4** — *da costruire, timing flessibile*
	- I/O: domande perimetro AI Act/Garante + claim commerciali ammissibili → parere scritto + bullet "compliant by design" per il Brief
	- Owner: one-shot, scouting Claude (~€0) + validation legale online (~€100-300)
	- Agganci: **doppio primario P7+P4** (unico sistema con ownership condivisa esplicita), S su P3
	- Nota: declassato da "gate non negoziabile pre-go-live" a "sistema con timing flessibile" — AIOS è pilot interno non in vendita, rischio AI Act/Garante è monitorabile non bloccante

## Tabella sintetica cross-pillar

| Sistema | P1 | P2 | P3 | P4 | P5 | P6 | P7 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Review Cadence | **P** | S | S | S | S | S | S |
| Cost Deployment | **P** | S | — | — | — | — | — |
| Pianificazione Giornaliera | **P** | S | — | — | S | — | — |
| Studio AI quotidiano | **P** | S | — | — | — | — | S |
| Cattura & Retrieval Info | **P** | S | S | S | S | S | S |
| Quality Pillar Coding | S | **P** | S | — | — | — | — |
| UPS Troubleshooting | — | **P** | S | — | — | — | — |
| Knowledge Management Coding | — | **P** | — | — | — | — | — |
| Validazione Pilot | S | **P** | — | — | — | — | — |
| Policy Cross-Selling | — | S | **P** | S | — | — | — |
| Decision Tree Escalation | — | — | **P** | — | — | — | — |
| Positioning Brief | — | — | S | **P** | — | S | — |
| Outbound Pipeline | — | — | S | **P** | — | S | — |
| Capability Marketing-Sales | — | — | — | **P** | — | — | — |
| Studio Quotidiano Giuridico | — | — | S | S | **P** | — | — |
| Mappa Network Bootstrap | — | — | S | S | — | **P** | S |
| Network Probe Loop | — | — | — | — | — | **P** | — |
| Sentinella Regolatoria | S | — | — | — | — | — | **P** |
| Una-tantum Legale Ibrida | — | — | S | **P** | — | — | **P** |

**P** = pillar primario · **S** = pillar consumer secondario · **—** = nessun aggancio

## Sistemi-perno cross-pillar

> [!tip] Massimo riuso, minima frammentazione
> Cinque sistemi presidiano da soli la maggior parte degli agganci cross-pillar:
> - **Review Cadence** (perno totale: tutti i 7 pillar)
> - **Cattura & Retrieval Info** (perno totale: tutti i 7 pillar — gemello infrastrutturale di Review Cadence)
> - **Mappa Network Bootstrap** (P6 → P3/P4/P7)
> - **Studio Quotidiano Giuridico** (P5 → P4/P3)
> - **Pianificazione Giornaliera** (P1 → P5/P2)
> - **Una-tantum Legale Ibrida** (unico sistema con doppio primario P7+P4)

## Sequenza di costruzione

### Foundation must-have entro 2026-04-30 (countdown HC-F4)

1. ✅ **Promozione a forma canonica dei 3 sistemi parziali** — chiusa il 2026-04-25: [[Processo-Pianificazione-Giornaliera]], [[Processo-Validazione-Pilot]], [[Processo-Cattura-E-Retrieval-Informazioni]] (sotto-funzione `Prioritizzazione Operativa` assorbita in Pianificazione Giornaliera)
2. ✅ **Mappa Network Bootstrap** — drafting iniziale chiuso il 2026-04-25 con i contatti già noti: [[Relazioni-Network-Mappa-Bootstrap]] (2 celle popolate su 16, 14 buchi dichiarati come input per altri sistemi Foundation)

### Foundation deliverable entro 2026-05-31

3. **Cost Deployment** formalizzato (costruito da zero)
4. **Studio AI quotidiano** codificato come sistema sistematico
5. **Policy Cross-Selling** (almeno regola binaria minima sul gate Quality)
6. **Positioning Brief** v1
7. **Sentinella Garante Regolatoria**
8. **Una-tantum Legale Ibrida** (timing flessibile, non più gate hard pre-go-live)

### Stability — Q3 2026

9. **Outbound Pipeline**, **Network Probe Loop**, **Capability Building M&S**, **Decision Tree Escalation completo**, **Deputy Onboarding Protocol** (rischio teorico, non urgente)

## Test MECE applicato

> [!check] Gate di accettazione superati
> - **Gate 1 — Collectively Exhaustive**: ogni loss (8 totali) ha ≥1 sistema owner ✓
> - **Gate 2 — Mutually Exclusive**: nessuna loss ha 2 owner (eccezione dichiarata: Una-tantum Legale è doppio primario su P4+P7 perché copre entrambe le loss simultaneamente) ✓
> - **Gate 3 — I/O chiuso**: ogni output va in input di un altro sistema o in HC pillar ✓

## Stato chiusura HC-F4

> [!success] Chiusa il 2026-04-25
> La mappa è definita end-to-end e i 3 sistemi parziali sono stati promossi a forma canonica con 5 giorni di anticipo sul target 2026-04-30: [[Processo-Pianificazione-Giornaliera]], [[Processo-Validazione-Pilot]], [[Processo-Cattura-E-Retrieval-Informazioni]]. Con HC-F4 chiusa, l'**intero step Foundation** del pillar [[Strategia-Pillar-Leadership-Strategica]] è chiuso (7/7 pillar Foundation + mappa concreta + 3 sistemi canonici).

## Rischi residui dichiarati

- **Bus-factor padre come deputy P4+P7** — rinviato a Stability (rischio teorico secondo founder, non concreto oggi)
- **Degradazione silenziosa sistemi** — da integrare come campo del template Review Cadence ("il sistema X ha prodotto output nell'ultimo periodo?"), non sistema nuovo
- **Escalation casi ambigui P3** — interim "in dubbio, padre", Decision Tree completo in Stability

## Aggiornamento 2026-04-25 — Allocazione 25 note candidate

> [!success] Deliberation room chiusa
> Architettura multi-agent (2 explore Sonnet + 3 research consulenziali Sonnet McKinsey/EY/PwC → resume Opus → deliberation room 3 voci Sonnet + moderatore Opus). Verdetto: **1 nuovo sistema** promosso a forma canonica + 24 note allocate come sotto-processo / input-asset / policy / concept di sistemi esistenti.
>
> Conteggio aggiornato: **20 sistemi** (era 19).

### Nuovo sistema promosso

#### P1 — sistema #6: Costruzione Vault Dedicato ★

> [!info] Loss presidiata
> Dispersione conoscenza dominio cliente in formato non strutturato → impossibile passare bus-factor o replicare su secondo cliente.

- **Codificato** in [[Processo-Costruzione-Vault-dedicato]]
- I/O: interviste cliente + documentazione esistente + sessioni operative → vault Obsidian dedicato con KB strutturata (entità, processi, eccezioni, glossario)
- Owner: founder (Foundation), promuovibile a sub-owner consulente a Stability
- Frequenza: on-demand per ogni nuovo cliente onboarded; review mensile vault esistenti
- Agganci: **P1 primario**, **S su P2** (asset replicabile a Stability che alimenta [[Sistema-Agentico-Studio]]), si integra con [[Processo-Cattura-E-Retrieval-Informazioni]]
- Promozione canonica target: **2026-05-15**, post-go-live AIOS

### Allocazione 25 note candidate

#### Blocco A — Processi (4 note)

| Nota | Pillar | S | Forma aggancio | Razionale |
|---|---|---|---|---|
| [[Processo-Gestione-Interruzioni-E-Errori]] | P1 | — | sotto-processo di **Pianificazione Giornaliera** | Tattica intra-day, non sistema |
| [[Processo-Prioritizzazione-Operativa]] | P1 | — | sotto-processo di **Pianificazione Giornaliera** | Assorbita; promuovibile a Stability se emerge loss separata |
| [[Processo-Costruzione-Vault-dedicato]] | P1 | P2 | **NUOVO SISTEMA** (vedi sopra) | — |
| [[Processo-Definizione-Obiettivi-Pillar]] | P1 | P3 | input/asset di **Review Cadence** | Doppio aggancio P3 per audit su KR reputazionali |

#### Blocco B — Strumenti (5 note)

| Nota | Pillar | S | Forma aggancio | Razionale |
|---|---|---|---|---|
| [[Strumenti-Claude-Code]] | P1 | — | strumento trasversale di **Cattura & Retrieval Info** + Pianificazione | Tooling, non sistema |
| [[Strumenti-Dashboard-Auto-Generata-Via-Bases]] | P1 | — | strumento di **Review Cadence** (cockpit) | Vista, non processo |
| [[Strumenti-Filing-Brain-Globale-Locale]] | P1 | — | **policy** di **Cattura & Retrieval Info** | Regola di routing cross-pillar |
| [[Strumenti-Obsidian-Writer-Source-Of-Truth]] | P1 | — | **policy** infrastrutturale di **Cattura & Retrieval Info** | Skill come SoT del filing |
| [[Prodotto-Vault-Substrato-Di-Prodotto]] | P2 | — | **concept** di **Costruzione Vault Dedicato** | Pattern architetturale (non sistema autonomo); promuovibile a Stability |

#### Blocco C — Pattern/principi (6 note)

| Nota | Pillar | S | Forma aggancio | Razionale |
|---|---|---|---|---|
| [[Pattern-Corporate-Business-Operations]] | P1 | — | input/asset di **Studio AI quotidiano** | Lessons learned corpus Lean/PM |
| [[Tecnologia-Best-Practice-Logging-Pipeline]] | P2 | **P3** | sotto-processo di **Quality Pillar Coding** + audit trail | **Doppio aggancio non-negoziabile** P3 (audit loss #2) |
| [[Vendite-Approcci-Per-Canale]] | P4 | — | input/asset di **Outbound Pipeline** + **Positioning Brief** | Playbook di canale |
| [[Vendite-Caso-Cinofilia]] | P4 | — | input/asset di **Positioning Brief** (case study analogico) | Evidenza fondante |
| [[Vendite-Principio-Educare-Prima-Vendere]] | P4 | **P3** | **policy** di pillar P4 + governance reputazionale | **Doppio aggancio non-negoziabile** P3 (vincolo verso peer) |
| [[Crescita-Modello-Personale]] | P5 | P3 | input di **Studio Quotidiano Giuridico** | Modello personale guida crescita; secondary control identitario |

#### Blocco E — Finanza (15 note distribuite nei 7 pillar esistenti)

| Nota | Pillar | S | Forma aggancio | Razionale |
|---|---|---|---|---|
| [[Finanza-MOC]] | — | — | hub L0, **non allocato** | Indice navigazione |
| [[Finanza-Business]] | — | — | hub L1, **non allocato** | Indice |
| [[Finanza-Personale]] | — | — | hub L1, **non allocato** | Indice |
| [[Finanza-Professionale]] | — | — | hub L1, **non allocato** | Indice |
| [[Finanza-Business-Capitale-Iniziale]] | P1 | — | input di **Cost Deployment** | Vincolo capacity finanziaria |
| [[Finanza-Business-Costi-Operativi-AIOS]] | P2 | P1 | input di **Validazione Pilot** | Soglia sostenibilità AIOS |
| [[Finanza-Business-Economics-FT]] | P2 | P1 | input di **Validazione Pilot** | P&L paper trading |
| [[Finanza-Business-Economics-Studio]] | **P3** | P4 | **policy governance** + input pricing | **Doppio aggancio non-negoziabile** — economics studio = controllo finanziario, non leva commerciale |
| [[Finanza-Business-Pricing-AIOS]] | P4 | P3 | input di **Positioning Brief** | Pricing rispetta vincolo reputazionale |
| [[Finanza-Business-Pricing-FT]] | P4 | — | input di **Outbound Pipeline** (retail) | Pricing canale FT |
| [[Finanza-Personale-Flussi]] | P1 | — | input di **Cost Deployment** | Runway dinamico |
| [[Finanza-Personale-Patrimonio]] | P1 | — | input di **Cost Deployment** | Buffer di rischio |
| [[Finanza-Personale-Runway-Transizione]] | P1 | — | input di **Cost Deployment** | Vincolo strategico hard |
| [[Finanza-Professionale-Cornice-Funzionale]] | P5 | — | input di **Studio Quotidiano Giuridico** | Cornice consulente lavoro (5 blocchi A-E) |
| [[Finanza-Professionale-Percorso-Formativo]] | P5 | — | input di **Studio Quotidiano Giuridico** | Roadmap gate identità |
| [[Finanza-Professionale-Piano-Accademico]] | P5 | — | input di **Studio Quotidiano Giuridico** | Tracker esami CFU |
| [[Mappa-Finanza-Livello-Professionale]] | P5 | — | mappa cross-pillar input P5 | Sintesi cluster professionale |

### Doppi agganci non-negoziabili (4)

> [!danger] Controllo cross-pillar obbligatorio
> Questi 4 agganci NON sono nice-to-have. Rimuoverli espone il sistema a rischio reputazionale o di audit.

1. **Tecnologia-Best-Practice-Logging-Pipeline** → P3(S): senza log verificabile, Policy Cross-Selling non ha audit trail della loss #2
2. **Vendite-Principio-Educare-Prima-Vendere** → P3(S): governa la postura verso peer professionali (vincolo reputazionale assoluto)
3. **Finanza-Business-Economics-Studio** → P3 PRIMARIO (non P4): economics studio del padre crea conflitto interessi se owned da pillar di velocità competitiva
4. **Processo-Definizione-Obiettivi-Pillar** → P3(S): KR di pillar hanno implicazioni reputazionali, P3 ha diritto di veto

### Concept e pattern non-sistemi

> [!info] Catalogo riferimenti
> Note che vivono nel vault come riferimento, alimentano sistemi ma NON entrano nella mappa come sistemi autonomi (no I/O ricorrente, no owner, no frequenza):
> - [[Prodotto-Vault-Substrato-Di-Prodotto]] (concept architetturale)
> - [[Strumenti-Filing-Brain-Globale-Locale]] (policy infrastrutturale)
> - [[Strumenti-Obsidian-Writer-Source-Of-Truth]] (policy infrastrutturale)
> - [[Crescita-Modello-Personale]] (modello mentale)
> - [[Pattern-Corporate-Business-Operations]] (lente diagnostica)
> - [[Vendite-Caso-Cinofilia]] (evidenza fondante)

### Concentrazione P1 — alert e mitigazione

P1 ora ospita **6 sistemi** + numerosi input/policy. È atteso (P1 = governance del sistema strategico, perno cross-pillar) ma è single point of failure operativo. Mitigazione:
- Review Cadence include check esplicito "P1 sta funzionando?" — non auto-review tacita
- A Stability: sub-owner per cluster (Pianificazione, Cattura-Retrieval, Validazione, Cost-Runway)

### Algoritmo decisionale per allocazioni future

> [!tip] Processo riutilizzabile
> Il processo di auto-allocazione di nuove note al pillar/sistema corretto vive in [[Processo-Allocazione-Conoscenza-Pillar]] (creato 2026-04-25). Si attiva automaticamente alla creazione di ogni nuova nota in `30-Dominio/`, `40-Conoscenza/` e nelle cartelle MOC di iniziative attive.

### Sequenza aggiornata Foundation / Stability

**Foundation (entro 2026-05-31)** — invariata + aggiunge:
- Promozione canonica di **Costruzione Vault Dedicato** target 2026-05-15

**Stability (Q3 2026)** — invariata + aggiunge:
- Valutazione promozione **Vault-Substrato-Prodotto** a sistema autonomo P2 (oggi concept)
- Valutazione promozione **Prioritizzazione-Operativa** a sistema autonomo P1 (oggi sotto-processo) se emerge loss separata
- Sub-owner per cluster interno P1

## Collegamenti

- [[Sistemi-Sotto-Pillar]] — quarta faccia meta-architettura, principio di forma canonica
- [[Strategia-Pillar-Leadership-Strategica]] — pillar proprietario di HC-F4 che questa nota chiude
- [[Pillar-Doppio-Livello]] · [[Zero-Loss-Mindset]] · [[Framework-Codificato-Per-Loss]] — altre 3 facce della meta-architettura
- [[Processo-Definizione-Obiettivi-Pillar]] — processo gemello (definizione obiettivi vs costruzione mappa)
- [[Processo-Review-Cadence]] · [[Processo-Quality-Pillar-Coding]] · [[Troubleshooting-UPS-Coding]] · [[Processo-Knowledge-Management-Coding]] · [[Processo-Pianificazione-Giornaliera]] · [[Processo-Validazione-Pilot]] · [[Processo-Cattura-E-Retrieval-Informazioni]] · [[Processo-Cost-Deployment]] — sistemi esistenti agganciati
- I 7 pillar: [[Strategia-Pillar-Leadership-Strategica]] · [[Prodotto-Pillar-Delivery-Piloti]] · [[Vendite-Pillar-Governance-Reputazionale]] · [[Vendite-Pillar-Sales-Positioning]] · [[Crescita-Pillar-Studio-Giuridico]] · [[Relazioni-Pillar-Network-Target]] · [[Strategia-Pillar-Monitoraggio-Regolatorio]]
- [[Dashboard]] — countdown Foundation chiuso 7/7 + mappa
