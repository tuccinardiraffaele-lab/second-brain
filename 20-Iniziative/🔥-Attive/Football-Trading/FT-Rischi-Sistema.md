---
tipo: concetto
creato: 2026-04-26
aggiornato: 2026-04-26
stato: attivo
progetto: "[[Football-Trading]]"
tags:
  - ft/rischi
  - prodotto/risk
area: prodotto
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari:
  - "[[Strategia-Pillar-Leadership-Strategica]]"
forma_aggancio: input
sistema_owner: "[[Processo-Validazione-Pilot]]"
---

# FT — Rischi di sistema

> [!info] In una frase
> Due rischi di sistema (piattaforma = basso, modello/edge = presidiato con doppia mitigazione tecnica + commerciale). Il cold calling FT è **sicuro** dal punto di vista reputazionale (target retail/privati).

## Rischio piattaforma — basso

- **Betfair**: i bot sono parte del modello di business (programma developer dedicato). Piano: migrare da account personale ad **account API commerciale** Betfair quando si apre la soluzione al mercato.
- **SportMonks**: sostituibile con alternative professionali (SofaScore API, altri provider). Scelto oggi per costo. Vedi [[FT-Vincolo-Sportmonks-Piano-API]].

## Rischio modello (evaporazione dell'edge) — presidiato

Il prezzo Betfair si forma dalla liquidità di chi scommette. Se più attori usano ensemble simili (Poisson + XGBoost + AI), tutti comprano/vendono insieme → il prezzo si allinea alla probabilità reale e l'**edge svanisce** (arbitraggio di mercato classico).

**Doppia mitigazione:**

1. **Tecnica — riaddestramento mensile come auto-correzione dell'edge.** Se al mese N l'edge calcolato non si è realizzato in P&L, il modello alza il filtro e smette di far passare quei segnali. Latenza massima: 1 mese. Il modello è auto-addestrante → dovrebbe essere tra i primi a offrire edge sempre aggiornati.

2. **Commerciale — esclusività come feature di prodotto.** Il pricing high-ticket non serve solo al margine: serve a **limitare l'adozione per preservare l'edge**. Se l'80% dei trader usa lo stesso sistema, il riaddestramento diventa vano perché tutti si muovono uguale. L'esclusività diventa leva di vendita, non vanity.

> [!tip] Connessione strategica
> Il pricing high-ticket e il rischio modello sono **due facce dello stesso meccanismo**: l'edge si preserva solo se gli utenti restano pochi. Questo va comunicato al cliente come **ragione per cui la fee è alta** — non come extra margine.

## Rischi reputazionali

Dal [[Strategia-Attuale#Il vincolo di reputazione]]: cold calling Football Trading è **sicuro** (target retail/privati, dominio separato dalla consulenza). Diverso il caso del [[Sistema-Agentico-Studio]] B2B.

## Collegamenti

- [[Football-Trading]] — MOC del progetto
- [[FT-Pricing-Model]] — pricing come leva commerciale
- [[FT-Modello-Business-Capacita-Limitata]] — cap utenti coerente
- [[FT-Vincolo-Sportmonks-Piano-API]] — vincolo dato provider
- [[Strategia-Attuale]] — vincolo reputazionale
