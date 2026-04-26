---
name: monthly
description: Usare questa skill per creare o aggiornare la review mensile del diario, con scan cross-progetto delle loss promosse nel mese e verifica assunzioni strategiche di progetto. Attivare quando l'utente dice "facciamo la review del mese", "chiudiamo il mese", "retrospettiva mensile", "review mensile", oppure a fine mese per consolidare pattern, assunzioni strategiche e difetti ricorrenti.
allowed-tools: Read, Glob, Grep, Bash(date *)
---

# Review Mensile

Skill di dominio: orchestra la chiusura del mese. Livello tattico della [[Processo-Review-Cadence]]: verifica assunzioni di progetto, scan pattern cross-progetto delle loss, review difetti aperti. **Non scrive file direttamente**: ogni creazione o modifica viene delegata a `obsidian-markdown`.

## Percorso vault
`/home/raffaele/Second Brain/10-Diario/Mensile/`

## Nome file
`Mensile-YYYY-MM.md` — es. `Mensile-2026-04.md`. Calcola con `date +%Y-%m`.

## Flusso

1. Calcola mese corrente e verifica con `Glob` se il file esiste.
2. Se **non esiste** → invoca `obsidian-markdown` per crearlo dal template sotto. Poi esegui i blocchi nell'ordine, **una domanda alla volta**.
3. Se **esiste** → leggilo, mostra cosa c'è già, aggiorna `aggiornato:` al giorno corrente.

### Blocco 1 — Riepilogo del mese
- "Le review settimanali del mese (cerca con `Glob 10-Diario/Settimanale/Settimanale-YYYY-Www.md` dove Www appartiene al mese) mostrano quali vittorie, ostacoli, insight ricorrenti?"

### Blocco 2 — Scan cross-progetto delle loss (nuovo)
Scan deterministico:
1. `Glob "20-Iniziative/🔥-Attive/*/losses/*.md"` — tutte le loss progettuali.
2. Filtra quelle con `creato:` nel mese corrente.
3. Raggruppa per `pillar` e per similarità di `failure-mode`.
4. **Se stessa classe di loss compare in ≥2 progetti distinti** → proponi promozione a globale in `30-Dominio/<sottodominio>/losses/` del pillar proprietario.
5. La decisione di promozione è del founder, non automatica.

Domanda guida: *"Nel mese sono emerse queste loss cross-progetto (elenco): quali promuoviamo a globale?"*

### Blocco 3 — Review difetti aperti
- Scan `Glob "**/.brain/autonomous-maintenance/defects/open/*.md"` nei repo locali noti (AIOS Studio, Football Trading).
- Elenca difetti aperti con severità.
- Domanda: *"Quali difetti aperti vanno aggrediti nel mese prossimo? Quali rimangono accettati?"*

### Blocco 4 — Assunzioni strategiche di progetto
Per ogni progetto attivo in `20-Iniziative/🔥-Attive/`:
- Leggi la MOC del progetto e la sezione assunzioni (se esiste).
- Domanda: *"Le assunzioni strategiche di `<progetto>` sono ancora vere? Cosa è cambiato?"*

### Blocco 5 — Review delle assunzioni cross-progetto
- "Le assunzioni in [[Strategia-Attuale]] sono ancora vere? Il contesto competitivo è cambiato?"
- "I 4 filoni paralleli stanno progredendo? Qualcuno è stato eroso?"

### Blocco 5bis — Review pillar mensile (Health check + avanzamento fase)
Da [[Pillar-Doppio-Livello]] + [[Processo-Review-Cadence]] Livello 2. Granularità: Health check oggettivi, non capture superficiale (quella è settimanale).

Per ciascuno dei 7 pillar strategici:
1. Leggi `pillar-fase-num` nel frontmatter e la sezione "Health check" della nota pillar.
2. Verifica quali Health check della fase corrente sono soddisfatti: la condizione è oggettiva (conteggio, presenza di artefatti, coerenza di metriche).
3. **Se tutti gli HC della fase sono soddisfatti** → proponi al founder l'avanzamento di `pillar-fase-num` (la decisione resta del founder, non automatica).
4. **Se HC ancora aperti** → elenca cosa manca e propone ≥ 1 azione concreta per il mese prossimo.
5. Registra il riepilogo come tabella `pillar | fase corrente | HC chiusi/totali | proposta`.

Domanda guida: *"Riepilogo review pillar del mese — confermi gli avanzamenti proposti e registri le azioni aperte?"*

### Blocco 5ter — Skill globali (outgrowth check, cadenza mensile)
Da `~/.claude/evals/` — livello tattico della Review Cadence applicato al framework Claude Code.

1. Scansiona `~/.claude/evals/reports/<skill>/` per ciascuna skill critica (`troubleshooting-ups`, `iterate`, `quality-pillar`, `sprint`): trova la data dell'ultima run di eval.
2. **Se ultima run >60 giorni fa** → candidata a outgrowth check. Il modello base potrebbe ormai fare il lavoro senza la skill (skill obsoleta).
3. Registra in tabella `skill | ultima eval | giorni da | proposta` (re-eval, archive, hold).
4. La decisione resta del founder.

Domanda guida: *"Skill globali non rieseguite da >60 giorni: rieseguiamo l'eval (regressione + outgrowth check) o accettiamo che siano stabili?"*

### Blocco 6 — Priorità del mese prossimo
- "Quali sono le 3-5 priorità strategiche del mese prossimo?"
- "Ci sono scadenze in `[[Scadenziere]]` che entrano nel mese prossimo?"

## Template nota nuova

Frontmatter:

```yaml
---
tipo: diario
creato: YYYY-MM-DD
aggiornato: YYYY-MM-DD
stato: attivo
mese: "YYYY-MM"
tags:
  - diario/mensile
---
```

Scheletro sezioni (senza H1):

```markdown
## 📆 Riepilogo del mese
- 

## 🔄 Loss cross-progetto promosse
<!-- populated dal Blocco 2: elenco wikilink a loss progettuali + eventuali promozioni a globali -->

## ⚠️ Difetti aperti fine mese
<!-- populated dal Blocco 3 -->

## 🧭 Assunzioni strategiche — verifica
- Per progetto: 
- Cross-progetto: 

## 🏛️ Review pillar (cadenza mensile)
<!-- da [[Pillar-Doppio-Livello]] + [[Processo-Review-Cadence]] L2 — Health check oggettivi + avanzamento pillar-fase-num -->

| Pillar | Fase | HC chiusi/totali | Azione/proposta |
|---|---|---|---|
| [[Strategia-Pillar-Leadership-Strategica]] | | | |
| [[Vendite-Pillar-Governance-Reputazionale]] | | | |
| [[Crescita-Pillar-Studio-Giuridico]] | | | |
| [[Relazioni-Pillar-Network-Target]] | | | |
| [[Vendite-Pillar-Sales-Positioning]] | | | |
| [[Strategia-Pillar-Monitoraggio-Regolatorio]] | | | |
| [[Prodotto-Pillar-Delivery-Piloti]] | | | |

## 🛠️ Skill globali — outgrowth check (cadenza mensile)
<!-- da ~/.claude/evals/ — Blocco 5ter — skill non rieseguite da >60gg = candidate outgrowth -->

| Skill | Ultima eval | Giorni da | Proposta (re-eval / archive / hold) |
|---|---|---|---|
| `troubleshooting-ups` | | | |
| `iterate` | | | |
| `quality-pillar` | | | |
| `sprint` | | | |

## 🎯 Priorità mese prossimo
- [ ] 
- [ ] 
- [ ] 

## 🔗 Settimane del mese
<!-- wikilinks alle note Settimanale-YYYY-Www dal mese corrente — il legame è già query-abile via frontmatter `mese` -->
```

## Dopo la scrittura

- Se emerse **decisioni strategiche** → `/decision`.
- Se emersi **temi aperti** da esplorare → `/brainstorm`.
- Se la review ha cambiato priorità su un pillar → aggiorna la nota pillar corrispondente (wikilink `[[Pillar-Doppio-Livello]]` per tassonomia).
- Scadenze >30 giorni emerse → `[[Scadenziere]]`.
