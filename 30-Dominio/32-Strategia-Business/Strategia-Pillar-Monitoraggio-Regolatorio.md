---
tipo: concetto
creato: 2026-04-20
aggiornato: 2026-04-25
stato: attivo
tags:
  - pillar/strategico
  - strategia/regolatorio
  - rischio/esogeno
area: strategia
pillar-fase: Foundation
pillar-fase-num: 0
pillar-loss:
  - Rischio-regolatorio-non-monitorato
---

# Pillar — Monitoraggio regolatorio AI

> [!info] In una frase
> Presidia il rischio esogeno più pericoloso dichiarato in [[Strategia-Attuale#Rischio esogeno — regolatorio]]: il legislatore può limitare l'uso autonomo dell'AI in ambito contabile/giuslavoristico. Controllo zero sulla sostanza del rischio, presidio pieno sulla **visibilità anticipata trasformata in decisione**.

## Loss proprietarie

| # | Loss bucket |
|---|-------------|
| #6 | Rischio regolatorio non monitorato — oggi cieco, nessuna fonte affidabile; se il regolatore si muove non ce ne accorgiamo in tempo |

## Filosofia di esecuzione

Il pillar nasce **cieco**. Quattro mosse strutturali si rinforzano a vicenda: (1) **una-tantum legale ibrida pre-go-live AIOS** (90% Claude scouting + 1h validation legale online ~€100-300) come asset di credibilità immediato e baseline classificazione AI Act dei moduli AIOS; (2) **sentinella Garante settimanale separata** dal ciclo mensile, perché in IT il Garante è il regolatore *de facto* AI lavoro/HR; (3) **≥2 decisioni business anticipate** come metrica di efficacia reale (gate non negoziabile Predictability→Agility); (4) **tooling LLM** costruito dal founder come abilitatore di disciplina sostenibile. Promozioni di fase ancorate a **eventi-gate**, non a date di calendario: le date sono target, gli eventi sono vincoli.

## Azione spot pre-go-live AIOS — Una-tantum legale ibrida

> [!warning] Approccio ibrido (opzione C scelta dal founder 2026-04-25)
> 90% scouting AI-assistito (Claude) + 10% validation legale online — preserva valore reputazionale "firma terzo" a costo basso.

| Item | Dettaglio |
|---|---|
| **Timing ottimale** | 2026-05-05 (5gg pre-go-live ~2026-05-10) |
| **Fallback** | Baseline ex-post entro Foundation 2026-09 |
| **Costo target** | €100-300 (validation online tipo ConsulenzaLegaleItalia / LegaleAI / equivalente) |
| **Output (a)** | Classificazione AI Act moduli AIOS sui 4 livelli (minimal / limited risk / high-risk / unacceptable) + checklist obblighi residui per livello + 1 pagina disclaimer/informativa standard |
| **Output (b)** | 2-4 bullet **"compliant by design"** riusabili come messaging [[Vendite-Pillar-Sales-Positioning]] (preventivo studio padre, futuri pitch B2C) |
| **Cross-pillar B→A immediato** | PDF di output diventa allegato silenzioso al preventivo studio padre da 2026-05 — asset di credibilità che precede qualsiasi LinkedIn (rinviato in [[Strategia-Attuale#Cosa NON sto facendo di proposito]]) |
| **Cross-pillar B→AIOS** | Modulo "high-risk" → vincolo di design pre-go-live, non patch ex-post |

## Obiettivi di fase (4 end-state)

Sorgente: [[Brainstorm-Obiettivi-Fase-Monitoraggio-Regolatorio]] (2026-04-25).

| Fase | End-state |
|------|-----------|
| **0 Foundation** | Pillar passa da cieco a osservante strutturato: 3 fonti primarie monitorate con `tipo_fonte` chiuso, ≥2 primarie indipendenti per perimetro (AI Act EU + Garante IT), 1 newsletter pagata, glossario chiuso "rilevante" + scala impatto, processo review documentato, sentinella Garante operativa, una-tantum legale archiviata, ≥1 decisione business già modificata da input regolatorio |
| **1 Stability** | Routine **ridondata e auditata**: ≥9 cicli mensili senza skip, audit trimestrale a campione 4 review/trim, deputy-of-record briefing 30min/trim, sentinella Garante a regime ≥48 sett/anno, tooling LLM v1 operativo (routine ≤30min) |
| **2 Predictability** | Sistema **anticipa** invece di reagire: ≥2 decisioni anticipate (azione registrata PRIMA della data efficacia trigger normativo, catena causale validata da deputy), lead time mediano detection→azione ≤21gg sostenuto su ≥3 trim, varianza <30% trim/trim, ≥70% alert qualificati |
| **3 Agility** | **Sopravvivere a ≥1 evento regolatorio reale** con time-to-response ≤14gg mediana / ≤21gg p90 detection→decisione+comunicazione clienti studio + 3-5 scenari playbook scritti + dry-run annuale sealed envelope dal deputy + bus-factor ≥2 |

## Health check SMART per fase

### Foundation (time-bound 2026-09-30, gate-vincolato)

| ID | Misura | Soglia | Tipo |
|----|--------|--------|------|
| HC-F1 | Moduli AIOS classificati AI Act pre-go-live (output una-tantum legale ibrida) | **100%** | Lagging |
| HC-F2 | Fonti primarie attive con tipologia chiusa `tipo_fonte` ∈ {primaria, sec-istit, aggregatore} | **3 totali, ≥2 primarie indipendenti per perimetro** | Leading |
| HC-F3 | Routine mensile 60min eseguita con artefatto datato (anche per "nessuna novità") | **≥3 cicli consecutivi** | Lagging |
| HC-F4 | Sentinella Garante coperta da inizio attivazione | **≥90% settimane** | Leading |
| HC-F5 | Decisioni business documentate con catena causale "input regolatorio → decisione" | **≥1** | Lagging |

Goodhart: HC-F2 mitigato con tipologia chiusa (aggregatori esclusi dal numeratore) + changelog motivato per modifiche. HC-F3 mitigato con sezione obbligatoria "implicazione AIOS" + "implicazione Pillar A" in ogni nota; se entrambe vuote per 2 cicli consecutivi → audit del glossario di rilevanza. HC-F5 mitigato richiedendo che la decisione cambi un comportamento osservabile dell'AIOS o un asset commerciale, validato dal deputy.

### Stability (time-bound 2027-03-31, gate-vincolato)

| ID | Misura | Soglia | Tipo |
|----|--------|--------|------|
| HC-S1 | Cicli mensili consecutivi senza skip (artefatto datato in tutti) | **≥9** | Lagging |
| HC-S2 | Audit trimestrale a campione 4 review/trim conferma classificazioni | **≥80%** | Lagging |
| HC-S3 | Sentinella Garante coperta + provvedimenti su perimetro triagati | **≥48 sett/anno + ≥80%** | Leading |
| HC-S4 | Decisioni business modificate per trimestre | **≥1/trim su 2 trim consecutivi** | Lagging |
| HC-S5 | Tooling LLM v1 operativo: routine mensile mediana | **≤30min su ≥3 cicli** | Leading |

Goodhart: HC-S1 mitigato con audit qualità (HC-S2) che pesca 4 review casuali. HC-S2 mitigato con deputy-of-record che vede campione audit (no auto-audit). HC-S3 mitigato con output settimanale che richiede screenshot/URL Garante. Tooling LLM se classificazione automatica scende sotto 80% confermate → torna in advisory mode (suggerisce, non classifica).

### Predictability (time-bound 2027-12-31, gate-vincolato)

> [!danger] Gate non negoziabile
> **≥2 decisioni anticipate** (azione registrata PRIMA della data efficacia del trigger normativo, catena causale validata da deputy esterno) — se il contatore è 0-1 al 2027-12, la fase NON è chiusa, indipendentemente dal resto del sistema.

| ID | Misura | Soglia | Tipo |
|----|--------|--------|------|
| HC-P1 | Decisioni anticipate cumulative validate da deputy | **≥2** (gate-event) | Lagging |
| HC-P2 | Lead time mediano detection→azione, sostenuto trim consecutivi | **≤21gg su ≥3 trim** | Lagging |
| HC-P3 | Varianza HC-P2 trim/trim | **<30%** | Lagging |
| HC-P4 | Alert qualificati su totale alert (precision) | **≥70%** | Leading |
| HC-P5 | Audit trimestrale conferma classificazioni Predictability | **≥85% su 2 trim** | Lagging |

Goodhart: HC-P1 mitigato con catena causale validata da deputy esterno (no auto-certificazione) + registro decisioni timestampato (data decisione < data efficacia trigger, verificabile). HC-P2 mitigato con timestamp automatici dove possibile (data nota Obsidian, data file aggregatore RSS). HC-P4 mitigato con peer review trimestrale del registro alert.

### Agility (time-bound 2028-09-30, gate-vincolato)

> [!info] Gate-event
> Sopravvivere a ≥1 evento regolatorio reale con time-to-response ≤14gg mediana / ≤21gg p90.

| ID | Misura | Soglia | Tipo |
|----|--------|--------|------|
| HC-A1 | Time-to-response detection→decisione+comunicazione clienti studio (eventi reali o dry-run) | **≤14gg mediana / ≤21gg p90** | Lagging |
| HC-A2 | Dry-run annuale eseguito su scenario sealed envelope dal deputy | **1/anno** | Leading |
| HC-A3 | Bus-factor verificato (1 ciclo mensile completo eseguito senza founder) | **≥2** | Leading |
| HC-A4 | Clienti studio raggiunti da brief privato post-evento entro 14gg | **≥90%** | Lagging |
| HC-A5 | Decisioni anticipate cumulative + clienti studio con messaging "compliant by design" | **≥4 cumulative + ≥3 clienti** | Lagging |

Goodhart: HC-A1 contrappeso da HC-A4 (se "decisione applicata" è cosmetica, comunicazione cliente vuota); criteri di "successo" pre-registrati nel playbook validati dal deputy. HC-A2 mitigato con scenario costruito dal deputy, non auto-assegnato. HC-A3 mitigato con una review mensile/anno eseguita materialmente dal deputy come prova.

## Sentinella Garante (sezione dedicata)

> [!tip] Rationale value-at-stake
> Il Garante Privacy in IT è il regolatore *de facto* su AI applicata al lavoro/HR, strutturalmente in anticipo sull'AI Act EU per i provvedimenti puntuali. Un singolo provvedimento (es. ordinanza su sistema decisionale automatizzato HR) può azzerare un modulo AIOS overnight. **Spegnere la sentinella = spegnere il pillar.**

- **Cadenza**: 30min/settimana, slot fisso **sabato** (decisione founder 2026-04-25, fuori da time-block studio giuridico), ≥48 settimane/anno
- **Output**: registro 3 colonne, una riga per provvedimento scansionato
- **Integrazione**: alimenta HC-F4 (Foundation), HC-S3 (Stability), HC-P2 (Predictability), HC-A1 (Agility)

| Provvedimento + data | Rilevanza ambito AIOS (sì/no/forse) + motivo 1 riga | Azione (triage decisione / no-action motivato / escalation) |
|---|---|---|
| ... | ... | ... |

## Target zero-loss sintetici

| Target | Finestra |
|--------|----------|
| Mesi senza nota datata di review post-Foundation | **= 0** |
| Settimane senza scan Garante post-attivazione (>2 consecutive) | **= 0** |
| Moduli AIOS in produzione senza classificazione AI Act | **= 0 al go-live** |
| Skip mensili che resettano il contatore Stability | **= 0 dopo 9 cicli** |
| Trimestri senza audit a campione in Stability/Pred | **= 0** |
| Decisioni "anticipate" non validate dal deputy | **= 0** |
| Eventi reali con response >21gg in Agility | **= 0** |
| Anni senza dry-run in Agility | **= 0** |

## Sub-step per avanzamento

- **0 → 1**: tutti i 5 HC Foundation verdi + una-tantum legale ibrida archiviata + glossario rilevanza inizializzato
- **1 → 2**: ≥9 cicli senza skip + ridondanza fonti + ≥1 audit trim ≥80% + ≥1 deputy briefing + tooling LLM operativo + ≥1 decisione/trim su 2 trim
- **2 → 3**: gate ≥2 decisioni anticipate validate da deputy + lead time ≤21gg su 3 trim + varianza <30% + tooling pre-flagga ≥60%
- **3 → mantenimento**: 1 evento reale superato a target + dry-run annuale + bus-factor effettivo

## Stato corrente

- **Fase**: 0 Foundation — iniziativa aperta in [[Monitoraggio-regolatorio-AI]] ma cieca; nessuna fonte attiva, nessun glossario, nessuna classificazione AI Act dei moduli AIOS
- **Deputy-of-record**: il padre, briefing trimestrale 30min (decisione founder 2026-04-25)
- **Bus-factor risk**: il padre è deputy anche per [[Vendite-Pillar-Sales-Positioning]]; concentrazione del backstop su una persona (~2×30min/trim totali). Accettabile in Foundation/Stability, da rivedere in Predictability se serve secondo deputy per validation catena causale HC-P1
- **TODO Foundation aperti**:
  - Una-tantum legale ibrida: scouting Claude entro 2026-04-30 + sessione validation legale online entro 2026-05-05
  - Selezione 3 fonti primarie + 1 newsletter pagata (test trial 1 mese su IAPP / Eutekne / OneTrust)
  - Glossario "rilevante" + scala impatto {alto/medio/basso} versionato
  - Slot sabato sentinella Garante in calendario + prima scansione

## Aggancio cross-pillar

- [[Vendite-Pillar-Sales-Positioning]] — cross-pillar B→A: messaggio "compliant by design" anticipato a Foundation Pillar A; brief privati clienti studio sono asset di vendita non pubblico
- [[Sistema-Agentico-Studio]] — classificazione AI Act dei moduli AIOS è gate pre-go-live ~2026-05-10
- [[Vendite-Pillar-Governance-Reputazionale]] — confine: brief regolatori privati a clienti studio OK; pubblici LinkedIn NO finché [[Strategia-Attuale#Cosa NON sto facendo di proposito|personal brand rinviato]]
- [[Strategia-Pillar-Leadership-Strategica]] — ogni decisione anticipata HC-P1 aggiorna [[Strategia-Attuale]] entro 14gg

## Limiti di knowledge dichiarati

> [!info] Da verificare con fonte primaria, non assumere come fatti
> - Scadenze esatte AI Act EU (general-purpose ago 2025, sistemi alto rischio ago 2026 — cifre da verificare con EUR-Lex)
> - Provvedimenti specifici Garante privacy su HR/AI citati durante la deliberation
> - Qualità reale newsletter pagate candidate (IAPP ~€500/anno, Eutekne, OneTrust DataGuidance) — testare con trial 1 mese prima di sottoscrivere

## Collegamenti

- [[Brainstorm-Obiettivi-Fase-Monitoraggio-Regolatorio]] — sorgente Sessione 1 + 2 (multi-agent deliberation 2026-04-25)
- [[Processo-Definizione-Obiettivi-Pillar]] — metodo applicato
- [[Pillar-Doppio-Livello]] · [[Zero-Loss-Mindset]] · [[Framework-Codificato-Per-Loss]]
- [[Monitoraggio-regolatorio-AI]] — iniziativa operativa (gemella)
- [[Strategia-Attuale#Rischi strategici]] · [[OKR-Correnti]]
- [[KR3.3 — Monitoraggio regolatorio AI]]
