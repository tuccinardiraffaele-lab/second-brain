---
tipo: processo
creato: 2026-04-14
aggiornato: 2026-04-27
stato: attivo
tags:
  - strumenti/claude-code
  - strumenti/obsidian
  - processo/knowledge-management
  - mece
area: strumenti
---

# Filing — Brain Globale vs Brain Locale

> [!info] In una frase
> Il principio è **MECE applicato al livello di astrazione**: globale = astrazione trasferibile (cosa vale anche altrove), locale = dettaglio implementativo specifico (cosa vale solo qui).

## Principio guida

Il confine NON è "tocca il codice / non tocca il codice". Il confine è **"vale solo qui / vale anche altrove"**.

- **Brain globale** = il vault Obsidian (`~/Second Brain/`) → concetti, strategia, decisioni riutilizzabili, persone, SOP, identità.
- **Brain locale** = **vault Obsidian locale** dentro il repo di ciascun progetto, che **comprende `.brain/` come sottocartella navigabile** (non è un'entità separata dal vault locale) → codebase, architettura, debito tecnico, problemi risolti, sprint.

> [!tip] Chiarimento architetturale (2026-04-20)
> Il vault locale **include** `.brain/` — non sono due entità parallele. Il repo pilota ha **un solo vault Obsidian locale**, di cui `.brain/` è una sottocartella. Conseguenza operativa: il grafo di Obsidian vede sia le note Obsidian native del repo che il contenuto di `.brain/` come parte dello stesso grafo locale. Chiarimento emerso nella strutturazione Sessione 2 di [[Prodotto-Pillar-Delivery-Piloti]].

Le note di livello diverso si **referenziano via wikilinks**, non si duplicano.


> [!example] Insight tassonomico osservato (triage AIOS 2026-04-27)
> Il confine **`20-Architettura/` (tecnico) vs `40-Dominio/` (business)** del brain locale si verifica leggendo il **contenuto**, non il nome. Esempio reale: `Workflow-AIOS.txt` sembrava architettura tecnica per nome — risultava invece descrizione del dominio studio commercialista (paese ~20k abitanti, 4 linee operative). Riallocato a `40-Dominio/Workflow-Studio-Commercialista.md`. Vedi [[Processo-Triage-Repo-Multi-Agent]] per la pipeline che ha catturato il misfiling.

## Regola di filing canonica

| Dimensione | Vault globale | Brain locale `<repo>/.brain/` |
|---|---|---|
| **Progetto** | MOC business: scopo, valore, ICP, mercato, rischi, metriche, stato | Codebase, stack tecnico, runbook |
| **Architettura** | Approccio concettuale (se esiste un principio astraibile) | Diagrammi, componenti, flussi, scelte implementative |
| **Decisioni tecniche** | Solo se trasferibili (principio riapplicabile ad altri progetti) — **default locale**, promozione esplicita | Default. Tutto ciò che è vincolato a questo codebase |
| **Decisioni strategiche/business** | Sempre | Mai |
| **Persone** | Sempre (tutte nel vault; il repo locale viene clonato sempre insieme al vault) | Mai |
| **Meeting** | Strategici, review, 1:1, coaching | Operativi di progetto (standup, review tecnica, call cliente di *quel* progetto) |
| **Problemi risolti** | Concetto astratto promosso (nuovo pattern di dominio) | Dettaglio completo: stack trace, fix, contesto riproducibile |
| **Debito tecnico** | Mai | Sempre |
| **Diario giornaliero** | Sempre | Mai |
| **Sprint/roadmap tecnica** | Mai | Sempre |
| **OKR, valori, identità, strategia** | Sempre | Mai |
| **Conoscenza di dominio riutilizzabile** | Sempre | Mai |
| **Runbook specifici del progetto** | Mai | Sempre |

## Note "gemelle" — quando un insight vive su due livelli

Alcuni insight hanno naturalmente un livello astratto + uno implementativo (esempio: una decisione tecnica con impatto strategico, o un problema risolto che rivela un pattern). In questo caso:

- **Entrambe le note esistono**. Non è duplicazione.
- La **locale** ha il "come" completo: codice, stack, fix, versioni, output.
- La **globale** ha il "cosa" astratto: pattern, principio, quando si applica, cosa evita.
- **Wikilink obbligatorio**: dalla locale alla globale (il collegamento al principio).
- **Wikilink facoltativo**: dalla globale a una o più locali come esempi applicati.
- **Niente ridondanza di contenuto**: se riscrivi lo stesso paragrafo in entrambe, hai sbagliato.

## Meccanismo di promozione autonoma

> [!tip] Principio
> La promozione locale → globale non è manuale. Il sistema deve riconoscere il pattern riutilizzabile autonomamente. **Soglia: ≥2 occorrenze** del pattern prima di promuovere. Un solo caso = aneddoto, non pattern.

### Meccanismo 1 — Rilevamento contestuale alla scrittura

Quando Claude sta per scrivere una nota `problema-risolto` o `decisione-tecnica` in un `.brain/` locale:

1. Prima di salvare, chiama `search_notes` via MCP Basic Memory sul vault e filesystem su altri `.brain/` di altri progetti.
2. Query: titolo + tag + libreria/componente menzionati.
3. Se trova **≥1 precedente con pattern strutturalmente simile** (stesso tipo di problema, stessa classe di fix, stessa libreria), Claude propone in conversazione:
	> "Ho trovato N casi simili: [lista]. Sembra emergere un pattern [descrizione]. Vuoi che scriva una nota concettuale globale che astragga il pattern e wikilinki i casi?"
4. Su approvazione utente, Claude invoca la skill appropriata (es. `/decision`) per scrivere la nota globale **conforme** alle convenzioni del vault, e aggiorna i wikilink nelle locali.

### Meccanismo 2 — Scansione periodica in `/weekly`

Agganciato alla skill `/weekly` esistente:

1. Claude elenca tutti i `problema-risolto` e `decisione-tecnica` scritti nei `.brain/` di tutti i progetti nella settimana.
2. Li **clusterizza** per tag, area, componente. Cluster con ≥2 elementi = candidato promozione.
3. Propone la lista candidati durante la review settimanale. L'utente scarta o approva in batch.

### Quando il sistema NON promuove

- **Un solo caso** → resta locale.
- **Similarità superficiale** (stessa libreria ma fix strutturalmente diverso) → Claude segnala ma non promuove. Decide l'utente.

## Esempi applicati

> [!example] [[FT-Vincolo-Sportmonks-Piano-API]] ([[Football-Trading]])
> - **Locale** (`<repo>/.brain/architecture/sportmonks-integration.md`): endpoint disponibili sul piano attuale, rate limit, workaround, costo upgrade.
> - **Globale**: nulla per ora. È specifico di questa integrazione.
> - **Se emerge un pattern** (es. stesso tipo di problema su altra API in altro progetto): nota concettuale "come disegnare ingestion resiliente su API con piani tiered" in `30-Dominio/33-Prodotto-e-Tecnologia/`, con wikilink alla locale come esempio applicato.

> [!example] Scelta broker low-cost per retail ([[Football-Trading]])
> - **Globale**: decisione strategica "per prodotti retail B2C, ottimizzare cost-to-trade prima di feature avanzate". Trasferibile ad altri progetti retail.
> - **Locale**: quale broker concreto, API, integrazione, costi comparati, setup. Wikilink alla globale.

> [!example] AIOS go-live con studio del padre ([[Sistema-Agentico-Studio]])
> - **Globale**: `Sistema-Agentico-Studio.md` → bet strategico, ICP, valore portato, roadmap business, metriche pilot, rischi strategici, mercato B2B/B2C.
> - **Locale**: `~/projects/aios/.brain/` → architettura multi-agent, integrazione GBSoftware, prompt degli agenti, test suite, debito tecnico, deploy runbook.

## Applicabilità

Questa regola si applica **ovunque**: sia quando Claude gira in un repo esterno al vault, sia quando gira dentro il vault stesso. È una regola di **organizzazione della conoscenza**, non una regola di codice, quindi non ricade nelle [[CLAUDE#Esclusioni per vault Obsidian|esclusioni per vault]] che escludono solo regole di coding (ciclo review, anti-overengineering, ecc.).

## Collegamenti

- [[Decisione-Framework-Brain-Globale-Locale]] — decisione architetturale completa con alternative valutate
- [[Brain-Framework-Implementazione]] — roadmap di implementazione
- [[Troubleshooting-UPS-Coding]] — altra metodologia del meta-sistema
