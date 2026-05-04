---
tipo: progetto
creato: 2026-04-13
aggiornato: 2026-05-02
stato: archiviato
repo_path: ~/projects/ai-football-trading
brain_path: ~/projects/ai-football-trading/.brain
tags:
  - football_trading
  - pilota
  - prodotto
area: prodotto
prossima_azione: "—"
blocco: "Pilota chiuso definitivamente — vedi Chiusura-Pilot-Football-Trading"
---

# Football Trading

> [!failure] Pilota chiuso definitivamente il 2026-05-02
> Sistema strutturalmente in perdita: tunare i modelli per accuracy comprime il volume ma non sposta il segno del PnL. L'edge non è monetizzabile su questo design. Combinato con il disallineamento strategico (FT non costruisce reputazione/capability per la consulenza in proprio), il pilota è chiuso definitivamente. Tempo riallocato totalmente su [[Sistema-Agentico-Studio]].
>
> Riferimento canonico: [[Chiusura-Pilot-Football-Trading]]. Riapertura possibile solo con nuova `/decision` di reversal.


> [!info] In una frase
> Sistema di football trading **automatico** che monetizza l'edge tra probabilità reali dell'evento e prezzo del mercato Betfair, attraverso un ensemble statistico (Poisson + XGBoost con embedding contestuali live) amplificato da un layer AI che filtra ambiguità e si riaddestra periodicamente. Rivolto a trader esperti high-ticket che cercano **monetizzazione passiva** senza presidio manuale.

## Indice navigabile

> [!tip] Hub di accesso al progetto
> Le sezioni di dettaglio vivono in note atomiche. Questa MOC mantiene solo: hub, stato vivo, log sessioni, debito, loss chiuse, azioni aperte.

**Prodotto**
- [[FT-ICP-Trader-Esperto]] — chi è il cliente target
- [[FT-Pricing-Model]] — due tier SaaS + garanzia di rimborso
- [[FT-Modello-Business-Capacita-Limitata]] — cap utenti hedge-fund-like

**Architettura**
- [[FT-Edge-Tecnico-Ensemble]] — ensemble Dixon-Coles + Poisson + XGBoost + Odds Expectation Model
- [[FT-Layer-AI-Tre-Fasi]] — stato layer AI + tre fasi (paper → live proprietario → mercato)

**Pilot**
- [[FT-Gate-Promozione-Fasi]] — gate di promozione tra le tre fasi
- [[FT-KPI-Monitorati]] — report `metrics_analyzer.py` (12 blocchi A→L) + monitoring quotidiano
- [[FT-Rischi-Sistema]] — rischio piattaforma + rischio modello (con doppia mitigazione)

## Stato attuale (vivo)

- **Fase**: paper trading attivo, **fase di apprendimento** — accumulo trades per addestramento modelli.
- **Modalità**: paper trading (zero capitale a rischio, solo costo API Betfair + SportMonks).
- **Bug noti**: nessun bug attivo. Bug emersi nella sessione 2026-04-13 (mercati sospesi tradati a prezzo differito; analytic agent regressione post-fix) sono **chiusi**.
- **Gate prossimo**: ≥1 mese paper trading in green + KPI sopra threshold (vedi [[FT-Gate-Promozione-Fasi]]).

## Azioni aperte

- [[FT-Chiarire-KPI-Metrics-Analyzer]] — sessione con AI su KPI non padroneggiati + definire threshold esplicite
- **Ricerca benchmark** — indagare se esistono trader/hedge fund sportivi con ROI verificabile (gap di ricerca conclamato — no riferimenti noti affidabili)
- **Pricing definitivo** — definire prezzo Premium e Basic a partire dai numeri del paper trading (vedi [[FT-Pricing-Model]])
- **Worst-case rimborsi** — calcolare sostenibilità finanziaria (vedi [[FT-Pricing-Model]])
- **Adverse selection** — meccanismo di screening per la garanzia (vedi [[FT-Pricing-Model]])

## Log sessioni

- [[2026-04-26]] — split MOC in note atomiche (8 atomiche FT create); pulizia stato bug (tutti chiusi); `prossima_azione` aggiornata a "fase di apprendimento — accumulo trades paper mode per training modelli".
- [[2026-04-13]] — sessione serale paper trading: Bug 1 (mercati sospesi) risolto, Bug 2 (analytic agent) emerso. **Entrambi successivamente chiusi**. Note atomiche: [[FT-Bug-Mercati-Sospesi-Prezzo-Differito]].
- 2026-04-24 — allineamento pipeline training a 2 anni (zombie decision chiusa) + osservabilità metriche XGBoost via `xgboost_models.metadata_json` JSONB. Retrain produttivo e attivazione `id=16`. Note atomiche: [[FT-Pattern-Zombie-File-Locali]].

## Debito tecnico

Pattern di debito osservati in codice o in osservabilità, con causa e indicazione di chiusura.

- [[FT-Pattern-Zombie-File-Locali]] — file locale letto da un consumer attivo ma non più scritto da nessuna pipeline corrente. Caso del 2026-04-24: `models/xgboost_evaluation.json` faceva mentire la dashboard XGBoost. Rilevamento: scan writer vs reader; chiusura: eliminazione, mai "deprecato".
- [[FT-Vincolo-Sportmonks-Piano-API]] — vincolo dato provider SportMonks.

## Loss chiuse

Lezioni riusabili catturate dal registro defect locale e promosse al livello progettuale (vedi [[Framework-Codificato-Per-Loss]]).

- [[2026-04-20-atomicita-one-shot-vs-live]] — quando porti logica da script one-shot a componente live-running, atomicità e durata del lock diventano requisiti espliciti. Classe A (violazione AC esistente).
- [[2026-04-20-rolling-vs-bootstrap]] — un algoritmo rolling live e lo stesso at-bootstrap non sono intercambiabili: il primo reagisce al presente, il secondo giudica il passato. Classe A.
- [[2026-04-20-ordine-reset-pipeline]] — estendere una pipeline di retrain con nuovi step integrati richiede di rivalutare gli step di reset pre-esistenti: quello che era cleanup legacy diventa danno se opera su stato che il nuovo flusso considera autoritativo. Classe A.
- [[2026-04-20-walker-abbandono-stato-fantasma]] — un `return` silenzioso in un branch di fallimento di retry lascia stato fantasma non sorvegliato. Ogni stato transient in memoria deve avere equivalente durable. Classe A (violazione AC esistente).
- [[2026-04-20-update-scope-troppo-largo]] — UPDATE con `WHERE chiave_logica` su tabella multi-row per stessa chiave copia valori su righe senza semantica per ospitarli. Serve la dimensione discriminante nel WHERE. Classe B (gap di AC).

## Collegamenti

- [[Strategia-Attuale]] — pilota 1 "in orbita" della strategia a 4 filoni
- [[Sistema-Agentico-Studio]] — pilota 2, bet principale
- [[Valori-Fondamentali#Velocità]] — il deploy del 2026-04-12 onora questo valore
