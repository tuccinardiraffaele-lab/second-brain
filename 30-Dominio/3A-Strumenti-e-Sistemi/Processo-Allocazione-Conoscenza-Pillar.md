---
tipo: processo
creato: 2026-04-25
aggiornato: 2026-04-25
stato: attivo
tags:
  - processo/knowledge-management
  - pillar/foundation
  - strategia/mappa
area: strumenti
---

# Processo — Allocazione conoscenza al pillar/sistema

> [!info] In una frase
> Algoritmo a 6 step che, alla creazione di una nuova nota di conoscenza nel vault (concept, processo, pattern, decisione operativa, asset, policy), determina **dove agganciarla** nella mappa pillar↔sistemi e **come tracciarla** (frontmatter + wikilinks). Output: la nota nasce già allocata, non orfana.

## Origine

Definito il 2026-04-25 come deliverable della deliberation room sulle 25 note candidate da allocare nella [[Strategia-Mappa-Pillar-Sistemi]]. Sintetizza i 3 algoritmi proposti dalle voci (McKinsey loss-first, EY rischio-first, PwC value-chain-first) in un **algoritmo ibrido rischio-first → value-chain-second**.

## Quando si attiva

**Trigger automatico (founder + Claude Code)** ad ogni:
1. Creazione di una nota in `30-Dominio/**`
2. Creazione di una nota in `40-Conoscenza/**`
3. Creazione di una nota di conoscenza atomica dentro un MOC di iniziativa attiva (`20-Iniziative/🔥-Attive/<Progetto>/`) — esclusi diari/log di sessione
4. Promozione di una nota da `00-Inbox/` verso una delle cartelle sopra
5. Promozione di un'OPL/CBA da `.brain/` di un progetto al vault

**Esclusioni**: note diaristiche (`10-Diario/**`), KR/OKR (artefatti già allocati per costruzione), brainstorm di fase (artefatti di processo, non conoscenza), entità (persone, aziende), templates, dashboard, scadenziere.

## Algoritmo a 6 step

> [!tip] Ordine non commutabile
> Gli step vanno percorsi nell'ordine. Saltare lo step 1 per ottimizzare il valore commerciale è esattamente il tipo di errore che distrugge la transizione.

### Step 1 — Gate rischio esterno (override)

**Domanda**: la nota tocca rischio reputazionale verso peer/clienti/studio padre, oppure rischio regolatorio (AI Act, Garante, fiscale, lavoristico)?

- **SÌ rischio reputazionale** → pillar primario candidato `P3` o doppio aggancio P3(S) obbligatorio
- **SÌ rischio regolatorio** → pillar primario candidato `P7` o doppio aggancio P7(S) obbligatorio
- **NO** → procedi step 2

### Step 2 — Gate forma canonica

**Domanda**: la nota ha **loss presidiata + I/O ricorrente + owner + frequenza** dichiarabili oggi?

- **NO** → è concept/pattern/strumento/policy → aggancio come asset/input/policy di sistema esistente. **NON nuovo sistema**. Salta a step 5.
- **SÌ** → procedi step 3

### Step 3 — Identifica il pillar primario per loss

**Domanda**: quale delle 8 loss riduce direttamente?

| Loss | Pillar primario |
|---|---|
| #1 Finestra-competitiva-persa | P1 |
| #2 Contaminazione-relazione-studio-clienti | P3 |
| #3 Identità-consulente-del-lavoro-non-costruita | P5 |
| #4 Networking-target-non-coltivato | P6 |
| #5 Vantaggio-asimmetrico-non-attivato | P4 |
| #6 Rischio-regolatorio-non-monitorato | P7 |
| #7 Capability-marketing-sales-mancante | P4 |
| #8 Maturità-piloti-non-in-tempo | P2 |

Se nessuna loss diretta → la nota non è un sistema, è un asset/input → torna a step 2 con verdetto NO.

### Step 4 — Test absorption

**Domanda**: esiste già un sistema mappato che presidia la stessa loss con I/O sovrapposto >70%?

- **SÌ** → la nota entra come **sotto-processo** del sistema esistente. Stop.
- **NO** → la nota è candidata a nuovo sistema. **Soglia hard**: max 1-2 nuovi sistemi per ciclo deliberativo (la promozione richiede deliberation esplicita, non si auto-attiva). Stop.

### Step 5 — Forma di aggancio per non-sistemi

Per le note che hanno fallito step 2 (forma canonica), determina la forma:

| Tipo di nota | Forma aggancio |
|---|---|
| Processo descrittivo non-ricorrente | sotto-processo del sistema più affine |
| Strumento/tool/skill | strumento di sistema esistente (asset operativo) |
| Pattern/principio/regola | **policy** del pillar owner del sistema governato |
| Caso studio/evidenza/lessons learned | input/asset del sistema di cattura più pertinente |
| Concept/modello mentale | concept di pillar (linkato dai sistemi che ne fanno uso) |
| Snapshot/stato (es. patrimonio, runway) | input di sistema consumer più diretto (es. Cost Deployment) |

### Step 6 — Doppi agganci di controllo (test rischio residuo)

Per ogni allocazione, verifica le 3 domande secondary control:

- (a) "Produce output visibile a clienti o peer professionali?" → P3(S) obbligatorio
- (b) "Contiene dati personali o knowledge base di terzi?" → P7(S) obbligatorio
- (c) "Influenza allocazione tempo o capitale del founder?" → P1(S) obbligatorio se non è già primario

## Output dell'algoritmo

### Frontmatter da scrivere/aggiornare nella nota

Aggiungere ai campi standard del frontmatter del vault:

```yaml
pillar_primario: P1|P2|P3|P4|P5|P6|P7
pillar_secondari: [P3, P7]   # vuoto se nessuno
forma_aggancio: sistema | sotto-processo | input | asset | policy | concept
sistema_owner: "[[Nome-Sistema-Esistente]]"   # se sotto-processo/input/asset/policy
```

### Wikilink obbligatori nel corpo

- Verso il sistema owner (se sotto-processo/input/asset)
- Verso il/i pillar primario (es. `[[Strategia-Pillar-Leadership-Strategica]]`)
- Verso pillar S se doppio aggancio non-negoziabile

### Aggiornamento mappa centrale

Se l'allocazione produce un **nuovo sistema**, aggiornare [[Strategia-Mappa-Pillar-Sistemi]]:
- Inserire il sistema nella sezione del pillar primario con forma canonica completa (loss + I/O + owner + frequenza)
- Aggiornare la tabella sintetica cross-pillar
- Aggiornare il conteggio totale sistemi

Se l'allocazione è sotto-processo/asset/policy: nessun update mappa richiesto (vivono linkati dal sistema owner).

## Esempi di applicazione

### Caso 1 — Nota nuova "Processo-Onboarding-Cliente-AIOS"

- Step 1: tocca clienti studio → P3(S) obbligatorio
- Step 2: ha I/O ricorrente (call cliente → vault dedicato + KB), owner founder, frequenza on-demand → forma canonica SÌ
- Step 3: loss #8 (maturità piloti) e loss #2 (contaminazione studio-clienti) → P2 primario, P3(S) secondary
- Step 4: absorption con `Costruzione Vault Dedicato` (P1)? Sovrapposizione I/O ~80% → **sotto-processo di Costruzione Vault Dedicato**
- Output: `pillar_primario: P1, pillar_secondari: [P2, P3], forma_aggancio: sotto-processo, sistema_owner: "[[Processo-Costruzione-Vault-dedicato]]"`

### Caso 2 — Nota nuova "Pattern-Pricing-Per-Studio-Dimensione"

- Step 1: nessun rischio diretto reputazionale/regolatorio
- Step 2: pattern descrittivo, niente owner/frequenza → forma canonica NO → step 5
- Step 3-4: skip
- Step 5: pattern → policy/asset di sistema → asset di **Positioning Brief** (P4)
- Step 6: produce output verso clienti? sì → P3(S)
- Output: `pillar_primario: P4, pillar_secondari: [P3], forma_aggancio: asset, sistema_owner: "[[Vendite-Pillar-Sales-Positioning]]"` (in attesa che Positioning Brief diventi nota canonica)

### Caso 3 — Nota nuova "Strumenti-Hook-Vault-Write-Guard"

- Step 1: nessun rischio esterno
- Step 2: strumento → forma canonica NO → step 5
- Step 5: strumento infrastrutturale → asset di **Cattura & Retrieval Info** (P1)
- Step 6: influenza allocazione tempo founder? marginale → no S obbligatorio
- Output: `pillar_primario: P1, forma_aggancio: asset, sistema_owner: "[[Processo-Cattura-E-Retrieval-Informazioni]]"`

## Tiebreak e regole anti-frammentazione

- **Tiebreak primario**: se due pillar sono ugualmente plausibili, vince quello con la loss più direttamente presidiata
- **Tiebreak secondario**: se la loss è ambigua, vince il pillar con il sistema più maturo (★ esistente codificato) — massimo riuso prima di qualsiasi nuova creazione
- **Anti-frammentazione**: se una nota è input di più sistemi diversi, NON duplicarla — allocala al consumer più frequente, gli altri come consumer secondari
- **Soglia nuovo sistema**: minimo 3 note con stesso I/O pattern senza casa, OPPURE 1 sola nota che presidia una loss attualmente scoperta. Sotto la soglia: assorbimento

## Verifica periodica

- **Settimanale (in `/weekly`)**: scan note create nella settimana → verifica che ciascuna abbia `pillar_primario` nel frontmatter e wikilink al sistema owner. Note orfane → triage immediato.
- **Mensile (chiusura mese)**: review note che hanno accumulato volume sotto un sistema esistente → valutare promozione a sistema autonomo (regola delle 3 occorrenze)

## Collegamenti

- [[Strategia-Mappa-Pillar-Sistemi]] — mappa target dell'allocazione
- [[Sistemi-Sotto-Pillar]] — forma canonica di sistema (input/output/processo/owner/agganci)
- [[Pillar-Doppio-Livello]] · [[Zero-Loss-Mindset]] · [[Framework-Codificato-Per-Loss]] — meta-architettura
- [[Processo-Definizione-Obiettivi-Pillar]] — processo gemello (definizione obiettivi vs allocazione conoscenza)
- [[Processo-Cattura-E-Retrieval-Informazioni]] — perno cross-pillar di cattura, di cui questo processo è raffinamento di routing
- [[Processo-Review-Cadence]] — verifica settimanale/mensile note allocate
- [[Strumenti-Filing-Brain-Globale-Locale]] — regola complementare globale/locale (questa nota raffina dove dentro il globale)
