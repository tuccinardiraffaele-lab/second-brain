---
tipo: concetto
creato: 2026-04-20
aggiornato: 2026-04-20
stato: attivo
tags:
  - brainstorm/pillar
  - prodotto/delivery
  - pillar/delivery-piloti
area: prodotto
---

# Brainstorm — Obiettivi di fase pillar Delivery piloti

> [!info] In una frase
> Sessione 1 (end-state 4 fasi) del pillar [[Prodotto-Pillar-Delivery-Piloti]], eseguita il 2026-04-20 via [[Processo-Definizione-Obiettivi-Pillar]]. Sessione 2 (Health check + zero-loss) aperta subito dopo.

## Step 0 — KB recovery

Letture effettive (2026-04-20):
- [[Prodotto-Pillar-Delivery-Piloti]] (scaffold pre-brainstorm)
- [[Pillar-Doppio-Livello]] (principio generativo + distinzione pillar-fase vs progetto-stato)
- [[Football-Trading]] (stato pilota + struttura `.brain/`)
- [[Decisione-Soglie-Pilot-AIOS]] (soglie pilot AIOS fissate 2026-04-19)
- [[Processo-Definizione-Obiettivi-Pillar]] (metodo)

### Test 0.c

1. **Problema del pillar**: garantire che il framework di delivery (SOP/KB/scaffold riutilizzabili) arrivi a una maturità tale da far arrivare i piloti (FT, AIOS, N+1) allo stato di leva strategica **entro la finestra competitiva**. Il pillar presidia la **maturità del framework**, non lo stato dei singoli piloti (che vive nelle MOC progetto).
2. **Vincoli concreti**:
    - Finestra competitiva AIOS stretta (go-live 2026-05-10) + vincolo reputazionale B2B off-limits fino abilitazione 2029
    - FT capacity-capped (~10 italiani / ~500 globali) → delivery = consegnare al cap in modo affidabile, non scalare infinitamente
    - Tempo founder limitato (sera + WE, Angelini lun-ven) + bus-factor AIOS centrato sul padre
3. **Freschezza note**: tutte ≤7 giorni. KB fresca.

Step 0 ✓.

## Cynefin quick check

**Complicated con zone Complex**. Framework IWS + pillar tecnici coding (Complicated), ma delivery di un pilota in contesto studio professionale (AIOS) è parzialmente Complex per adozione umana e adattamento real-time post go-live. → Procedi con cautela.

## Sessione 1 — End-state

### D1-D2-D3 risposte founder (normalizzate)

Agility = 5 elementi distinti:

- **A1** Framework a doppio livello dichiarato — globale (vault Second Brain) + locale (repo dei piloti con proprio `.brain/` Obsidian).
- **A2** Principi globali ereditati in cascata — scaffold, processi, best practice definiti nel vault globale arrivano *automaticamente* nel vault locale, non per copia manuale.
- **A3** Feedback loop bidirezionale automatico — finding/aggiornamento locale viene promosso al globale senza rito manuale discrezionale.
- **A4** Onboarding standardizzato di nuovo pilota — all'ingresso di un pilota: mappatura strategica globale + init scaffold locale (repo + vault Obsidian locale) come riflesso, non decisione ad-hoc.
- **A5** Grafo integrato osservabile — i collegamenti tra grafo globale e grafi locali sono chiaramente navigabili da un terzo.

### Asset già posseduti (non target del pillar)

- Vault globale esiste
- `/sprint` promuove loss dal locale al globale
- Alcuni repo hanno `.brain/`

**In Agility la differenza è sistematicità e automatismo, non esistenza.**

### Backward chain

| Fase | End-state scelto |
|------|------------------|
| Agility | A1-A5 tutti attivi + pilota #3 onboardato via standard |
| Predictability | Framework su N=2 (FT + AIOS) + **almeno un ciclo feedback locale→globale realmente promosso e ricaduto in cascata sull'altro pilota** |
| Stability | **AIOS ha `.brain/` + vault Obsidian locale completo**; FT ancora in setup. AIOS prioritario perché bet principale |
| Foundation | Doppio livello **dichiarato come principio** nel vault globale + pillar tecnici operativi (Quality, UPS, KM, Cost Deployment, Review Cadence) noti ma applicazione disomogenea tra i due piloti |

### Step 1.4 — Challenge

#### Pre-mortem — 3 cause confermate dal founder

1. **Feedback locale→globale resta manuale** — promozione via `/sprint` esiste ma richiede invocazione discrezionale. Senza meccanismo strutturale (hook, trigger automatici) il ciclo si spezza quando il founder è sotto pressione.
2. **Onboarding standardizzato non viene mai stress-testato** — non arriva mai un pilota #3 perché il filone non si apre. Il framework resta ottimizzato per N=2 e collassa al primo nuovo progetto.
3. **Divergenza tra grafo globale e locale** — senza disciplina di naming/link, i grafi locali si frammentano e non sono più navigabili dall'esterno. Il segnale A5 evapora silenziosamente.

#### WRAP widen — alternativa dichiarata

**Il framework a doppio livello entra a far parte dell'offerta B2B di AIOS.**

Decisione strategica: non è "fuori scope" ma "asset commerciale del pilota AIOS in fase Agility". Conseguenza: crea aggancio esplicito con:
- [[Vendite-Pillar-Sales-Positioning]] — il framework è parte della proposta di valore verso studi peer
- [[Vendite-Pillar-Governance-Reputazionale]] — B2B off-limits fino abilitazione 2029, quindi commercializzazione framework segue lo stesso gate

#### Reality-test

- A1, A2, A3, A5 verificabili da terzi (esistenza meccanismi strutturali, apertura vault da peer)
- **A4** verificabile solo con evento futuro (pilota #3 effettivo). Conseguenza: in Predictability il framework è già *progettato* per l'onboarding, ma Agility si certifica solo con pilota #3 reale.

## Collegamenti

- [[Prodotto-Pillar-Delivery-Piloti]]
- [[Processo-Definizione-Obiettivi-Pillar]]
- [[Pillar-Doppio-Livello]]
- [[Sistema-Agentico-Studio]] · [[Football-Trading]]
- [[Vendite-Pillar-Sales-Positioning]] · [[Vendite-Pillar-Governance-Reputazionale]]

## Sessione 2 — Health check + target zero-loss

Eseguita il 2026-04-20 subito dopo Sessione 1. Framework combinato: SMART + Leading/Lagging + Goodhart.

### Chiarimento architetturale emerso

Il **vault locale comprende `.brain/`** come sottocartella navigabile — non sono due entità separate. Ogni repo pilota ha UN vault Obsidian locale che include `.brain/`.

### Spostamento A1, A2 a Foundation

Decisione founder: A1 (nota canonica framework) e A2 (template riusabile `.brain/` + vault locale) sono requisiti **Foundation**, non Agility. Conseguenza: Foundation diventa più pesante (anticipa meccanismi strutturali), Agility più stretta (solo A3 hook + A4 onboarding + A5 peer).

### Health check elicitati (soglie dal founder)

Vedi tabelle per fase in [[Prodotto-Pillar-Delivery-Piloti]]. Sintesi soglie:

| Fase | Soglia chiave | Time-bound | Finestra valutazione |
|------|--------------|-----------|---------------------|
| Foundation | Nota canonica + template + ≥1 evidenza/pilota + regole scambio | entro 2026-06-30 | mensile |
| Stability | `.brain/` AIOS completo (5 componenti) + vault locale AIOS + FT ≥1 componente avviato | entro 2026-05-31 | mensile |
| Predictability | FT Stability completo + ≥1 promozione bidirezionale/pilota + ricaduta cascata tracciata | entro 2026-09-30 | mensile+trimestrale |
| Agility | Hook feedback + onboarding pilota #3 ≤1gg + peer esterno naviga ≤30min | entro 2030-12-31 | mensile + semestrale A-HC3 |

### Gaming mitigation complessiva

- F-HC3: ogni OPL/CBA/loss deve avere ≥1 wikilink entrante (proof of use reale)
- P-HC2: promozione citata in ≥1 review mensile prima di contare (proof of use)
- A-HC2: pilota #3 deve avere stakeholder esterno reale + obiettivi business propri
- A-HC3: peer test con persona diversa dal founder, cronometrato

### Target zero-loss derivati

Tutti i target zero-loss sono derivati come **negazione degli Health check** (nessuna metrica nuova inventata): "mesi/trimestri con [metrica] sotto soglia = 0 per la finestra di valutazione".

### Challenge Sessione 2 — reality-test finale

- Tutti gli Health check verificabili da terzo? ✓
- Tutti i target zero-loss derivati e non inventati? ✓
- Gate critico unico o gate multipli? → **Foundation è gate composito** (4 Health check), Predictability è il **gate più rischioso** (richiede ciclo feedback reale bidirezionale, che dipende da vita operativa non accelerabile)
- Soglie tutte elicitate dal founder, nessuna inferita? ✓

### Anti-pattern evitati

- Nessuna inferenza numerica al posto del founder
- Nessuna invenzione di artefatti esterni
- Nessuno Health check vago (tutti con soglia + finestra)
- Step 0 rigoroso (test 0.c passato esplicitamente)

