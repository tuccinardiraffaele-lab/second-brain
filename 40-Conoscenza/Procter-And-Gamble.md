---
tipo: concetto
creato: 2026-04-16
aggiornato: 2026-04-20
stato: attivo
tags:
  - azienda
  - manufacturing
  - continuous-improvement
area: conoscenza
---

# Procter & Gamble

> [!info] In una frase
> Multinazionale FMCG (beni di largo consumo) che ha sviluppato internamente **IWS (Integrated Work System)**, uno dei sistemi di eccellenza manifatturiera più codificati al mondo — da cui derivano i framework adottati in questo vault ([[Troubleshooting-UPS-Coding]], [[Processo-Quality-Pillar-Coding]]).

## IWS — Integrated Work System

Sistema operativo proprietario per l'eccellenza manifatturiera, cresciuto organicamente dentro P&G a partire dal 1969. Non è TPM, non è Lean, non è Six Sigma — è un framework che li **contiene tutti** in un unico sistema che abbraccia persone, processi, tecnologia e cultura.

> [!quote] Definizione ufficiale (Marc Winkelman, Global Director IWS)
> *"P&G's chosen corporate operational excellence program based upon our practical experience to drive common culture and common standards across all functions and all levels in all supply chains."*

### Timeline

| Anno | Tappa |
|------|-------|
| 1969 | High-Performance Work Systems (HPWS) |
| 1983 | Total Quality / Process Control |
| 1986 | TPM e processi di manutenzione strutturati |
| 1990 | Six Sigma |
| 1996 | Reliability Engineering |
| 2001 | Supply Chain Initiatives |
| 2003 | End-to-End Optimization |
| 2009 | Benchmark diretto Toyota (studio del TPS) |
| 2010 | E2E Synchronization |
| 2013 | Partnership di licensing con EY — IWS disponibile esternamente |

### I 2 principi fondamentali

1. **Zero Losses** — l'obiettivo è l'**eliminazione totale** delle perdite, non la riduzione. Ogni perdita viene categorizzata nella loss tree, quantificata economicamente, attaccata con lo strumento appropriato.
2. **100% Total Employee Ownership** — ogni dipendente identifica ed elimina perdite attivamente. L'operatore è il primo proprietario della macchina. Da "hero culture" (pochi risolutori) a "everyone culture".

### I 12 pillar

| # | Pillar | Funzione |
|---|--------|----------|
| 1 | **Leadership** | Servant leadership, decision-making bottom-up |
| 2 | **Focused Improvement (FI)** | Kobetsu Kaizen adattato; RCA e FMEA |
| 3 | **Progressive Maintenance (PM)** | Manutenzione proattiva e predittiva |
| 4 | **Education & Training** | Learn-Do-Teach: impara, applica, insegna |
| 5 | **Supply Network** | Ottimizzazione Service-Inventory-Cost |
| 6 | **Work Process Improvement** | Standardizzazione, eliminazione sprechi |
| 7 | **Initiative Management** | Gestione progetti, eliminazione rework |
| 8 | **Quality** | Zero defects lungo tutta la supply chain |
| 9 | **HSE** | Zero incidenti |
| 10 | **Enterprise** | Trasformazione organizzativa |
| 11 | **Autonomous Maintenance (AM)** | Operatore proprietario della macchina, progressione a 7 step |
| 12 | **Organization** | Allineamento comportamenti ai bisogni di business |

> [!tip] Differenza chiave vs TPM classico JIPM
> TPM ha 8 pillar centrati sull'equipment. IWS ne ha 12, aggiunge Leadership, Enterprise, Organization, WPI, Supply Network, Initiative Management. Lo scope è l'intera organizzazione, non solo la manutenzione.

### I 5 principi guida

1. **DMS (Daily Management System)** — sistema strutturato per mantenere e migliorare risultati quotidianamente
2. **DDS (Daily Direction Setting)** — riunione di inizio turno, allineamento priorità, gestione deviazioni
3. **Learn-Do-Teach** — meccanismo di diffusione capability esponenziale
4. **Strumenti zero-loss** — loss analysis, UPS, WPI, health check
5. **Servant Leadership** — leader che servono i team rimuovendo ostacoli

### Strumenti operativi chiave

- **UPS (Unified Problem Solving)** — framework unificante di problem solving, contiene 5-Why, 6W-2H, Work Point Analysis. Vedi [[Troubleshooting-UPS-Coding]] per l'adattamento al coding.
- **CIL (Clean, Inspect, Lubricate)** — standard di Autonomous Maintenance quotidiano (Step 3 AM)
- **Centerline Management / Run-to-Target** — setting ottimali di processo con limiti, monitoraggio deviazioni real-time
- **Loss Tree** — categorizzazione e quantificazione di tutte le perdite con Pareto
- **AM 7 Step** — progressione operatore da pulizia iniziale a self-management completo
- **Layered Process Audits** — audit a livelli progressivi (operatore → supervisor → manager → plant leader)

### 4 fasi di implementazione per sito

1. **Foundation** — baseline, standard minimi, awareness
2. **Operational Stability** — performance consistente, processi ripetibili
3. **End-to-End Stability** — allineamento cross-funzionale
4. **Agility** — operazioni adattive, risposta rapida al cambiamento

### Confronto con altri sistemi

| Dimensione | IWS (P&G) | WCM (Stellantis) | TPS (Toyota) |
|-----------|-----------|-------------------|-------------|
| Driver | Loss tree + UPS | Cost Deployment | Genchi Genbutsu + Hoshin Kanri |
| Carattere | Americano/corporate, altamente codificato | Europeo-giapponese, scoring competitivo tra siti | Giapponese, introspettivo, dal basso |
| Licensing | Sì (EY, dal 2013) | Sì (Yamashina Institute) | No (filosofia aperta) |
| Pillar | 12 | 10 tecnici + 10 manageriali | Non strutturato a pillar |

### Risultati documentati

- OEE: 85-94% across factories
- Riduzione downtime non pianificato: 80-95%
- Produttività: +20-40%
- $15 miliardi risparmi cumulativi (alleanza EY, 400+ fabbriche esterne)
- ROI: 3-5x a siti maturi, payback 12-18 mesi
- Boryspil plant: 11 anni senza infortuni

### Diffusione esterna

Dal 2013 P&G licenzia IWS tramite la partnership con **EY (Ernst & Young)**. Oltre 400 fabbriche non-P&G lo adottano. EY lo combina con Smart Factory e Run-to-Target Transformation Accelerator.

## Cosa è stato adottato in questo vault

| Concetto P&G | Adattamento | Nota |
|---|---|---|
| UPS (Unified Problem Solving) | Troubleshooting strutturato per coding/debug | [[Troubleshooting-UPS-Coding]] |
| Quality Pillar + AM (defect tracking) | Quality gate per coding: AC, verifica outcome, defect register con severità | [[Processo-Quality-Pillar-Coding]] |
| Loss tree + zero-loss mindset | Mappa dei 12 tipi di perdita nel coding e nel lavoro strategico | [[Processo-Quality-Pillar-Coding#Loss map]] |
| OPL + CBA + DMS push-based | Cattura conoscenza nel momento in cui emerge (OPL/CBA nel brain locale) + retrieval push-based pre-sessione | [[Processo-Knowledge-Management-Coding]] |
| Cost Deployment (Loss Tree + Matrici A-E) | Chiavi di conversione per rendere visibile il costo dei trade-off aperti, auto-correzione della prioritizzazione | [[Processo-Cost-Deployment]] |
| DMS Review Cadence + Layered Process Audit + Phase Assessment | Review prescrittive a tre livelli (settimanale/mensile/trimestrale) per forzare CI strategico | [[Processo-Review-Cadence]] |
| Pillar come doppio livello (operativo locale + strategico globale) | Principio trasversale: pillar come gate locale oggettivo + inventario strategico cross-entità, derivato dal loss tree del sistema strategico personale | [[Pillar-Doppio-Livello]] |
| Zero-Loss Mindset come moltiplicatore di ROI | Principio trasversale: rifiuto ontologico della loss + infrastruttura (pillar+ownership+risorse scalabili) che rende auto-bilanciante il sistema; capex di prevenzione scala inversamente alla maturità | [[Zero-Loss-Mindset]] |
| Framework codificato per tipo di loss | Principio trasversale: gerarchia strumenti (AM→UPS→Capex) + MECE per classe di loss + regola "un solo record vivo" + classificazione A/B/C di chiusura | [[Framework-Codificato-Per-Loss]] |

## Fonti principali

- [Delft Consulting — The power of P&G's IWS](https://delft-consulting.com/articles/the-power-of-procter-gambles-iws-can-you-get-it-for-free/)
- [Henkan — UPS Practical Guide](https://henkan.com/a-practical-guide-to-applying-unified-problem-solving-ups-in-a-ci-environment/)
- [LinkedIn — Chr. Roumeliotis, IWS Model](https://www.linkedin.com/pulse/integrated-work-system-iws-pgs-model-operational-chr-roumeliotis-d1see)
- [LinkedIn — Andrew Caveney, Beyond Lean](https://www.linkedin.com/pulse/beyond-lean-next-generation-manufacturing-excellence-andrew-caveney)
- [IWS Primer — Intellections](https://intellections.wordpress.com/2024/05/14/iws-integrated-work-system-primer/)
- [EY — P&G Alliance](https://www.ey.com/en_us/alliances/pg)
- Slideshare — Laszlo Marta & Olesia Burak, P&G Boryspil

## Collegamenti

- [[Troubleshooting-UPS-Coding]] — UPS adattato al coding
- [[Decisione-Adozione-UPS-Coding]] — decisione di adozione UPS
- [[Processo-Quality-Pillar-Coding]] — Quality Pillar adattato al coding
- [[Valori-Fondamentali#Efficacia]] — "colpire il bersaglio vero"
- [[Valori-Fondamentali#Velocità]] — "velocità senza efficacia è rumore"
- [[Pillar-Doppio-Livello]] — meta-principio dei pillar a doppio livello applicato al sistema strategico personale
- [[Zero-Loss-Mindset]] — principio trasversale del rifiuto ontologico della loss e moltiplicatore ROI
- [[Framework-Codificato-Per-Loss]] — principio trasversale del framework codificato per tipo di loss + regola MECE record vivo
- [[Dashboard]]
