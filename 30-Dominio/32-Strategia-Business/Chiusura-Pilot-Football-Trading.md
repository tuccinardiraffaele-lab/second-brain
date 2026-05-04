---
tipo: decisione
creato: 2026-05-02
aggiornato: 2026-05-02
stato: attivo
tags:
  - decisione/strategia
  - football_trading
area: strategia
reversibilità: bassa
impatto: alto
scadenza-revisione: 2026-08-02
---

## Contesto

[[Football-Trading]] era il pilota #1 della strategia a 4 filoni — deployato in produzione il 2026-04-12, dichiarato "in orbita" per liberare attenzione verso il bet principale [[Sistema-Agentico-Studio]]. Lo stato salvato il 2026-04-26 era "paper trading in fase di apprendimento, nessun bug attivo, gate ≥1 mese in green non ancora valutato".

Nelle settimane successive, lavorando sui modelli per migliorare l'accuratezza dei trade, è emerso un comportamento strutturale: **tunare per accuracy comprime il volume ma non sposta il segno del PnL**. Il sistema è intrinsecamente in perdita: aumentare la qualità dei trade riduce il numero ma non ribalta il trend. L'edge tra probabilità reali e prezzo Betfair, come modellato dall'ensemble Dixon-Coles + Poisson + XGBoost + Odds Expectation Model, non esiste in modo monetizzabile su questo design.

## Decisione

**Chiusura definitiva del pilota Football Trading.** Archiviazione del progetto, riallocazione totale del tempo verso [[Sistema-Agentico-Studio]] come unico pilota attivo della strategia.

## Alternative considerate

1. **Pivot del design** (modello/mercato/sport diverso) — scartata: anche con un edge ipoteticamente recuperabile, FT non costruisce reputazione né capability per il dominio target della transizione (studi professionali). Il costo di esplorazione non ha ritorno strategico.
2. **Pausa-parcheggio in `💤-In-Pausa/`** — scartata: tenere il progetto in stato ambiguo lascia attrito mentale e tentazione di rientro. La chiusura definitiva è più pulita.
3. **Paper trading acceso a costo zero come strumento di apprendimento** — scartata: l'apprendimento tecnico è già stato estratto (5 loss promosse, vedi sotto). Mantenere i job in esecuzione consuma attenzione di osservabilità senza nuovo segnale.

## Rationale

Anche se l'edge esistesse, FT non porta al cliente target della transizione (studi professionali). Il pilota era nato come "in orbita" per liberare tempo verso AIOS, ma in realtà sta consumando attenzione su un dominio retail/trading che non costruisce reputazione né capability per la consulenza in proprio. L'evidenza tecnica (sistema strutturalmente in perdita con trade-off accuracy/volume che non ribalta il segno) chiude il dubbio, ma la scelta sarebbe stata corretta anche con numeri marginalmente positivi: il disallineamento strategico è il driver primario, l'evidenza tecnica è il driver di tempistica.

## Rischi e trade-off

- **Sunk cost del lavoro tecnico** (ensemble Dixon-Coles + XGBoost + layer AI + 5 loss promosse) — accettato. Mitigazione: le 5 loss restano knowledge cross-progetto riusabile (vedi sezione Loss chiuse di [[Football-Trading]]); il codice del repo non si recupera.
- **Rischio "ho mollato troppo presto"** — accettato. Mitigazione: la decisione è scritta e definitiva; eventuale riapertura richiede una nuova `/decision` esplicita di reversal con nuova evidenza che invalidi la diagnosi strutturale.
- **Costo opportunità reputazionale residuo** — accettato. Se il progetto è stato menzionato a network/peer, la chiusura va comunicata o resta silenziosa a seconda del contesto. Nessun rischio sul vincolo reputazionale di [[Strategia-Attuale]] perché FT non era nel dominio della consulenza.

## Revisione

Rivedere entro **2026-08-02** (3 mesi). La revisione non rivaluta la chiusura — verifica che la chiusura abbia liberato il valore atteso. Criteri di successo:

1. Tempo liberato è effettivamente confluito su AIOS — verificabile dai diari giornalieri e dai log sessioni AIOS post-2026-05-02.
2. Nessun rientro impulsivo su FT — no commit nel repo `~/projects/ai-football-trading`, no nuove note in `90-Archivio/Football-Trading/`, no nuovi `.brain/` entries.
3. Le 5 loss promosse restano linkate e riutilizzate dal brain locale AIOS dove applicabili — pattern cross-progetto effettivamente attivati.

## Note collegate

- [[Strategia-Attuale]] — strategia da aggiornare a "4 filoni / 1 pilota"
- [[OKR-Correnti]] — Objective 2 archiviato, KR2.1/2.2/2.3 chiusi senza target
- [[Football-Trading]] — MOC del progetto archiviato
- [[Sistema-Agentico-Studio]] — unico pilota attivo, beneficiario della riallocazione
- [[Crescita-Priorità-Correnti]] — priorità #2 (FT debugging) decade
- [[Identità]] · [[Valori-Fondamentali#Velocità]]
