---
tipo: concetto
creato: 2026-04-26
aggiornato: 2026-04-26
stato: attivo
progetto: "[[Sistema-Agentico-Studio]]"
tags:
  - aios/mvp
  - prodotto/scope
area: prodotto
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari:
  - "[[Vendite-Pillar-Sales-Positioning]]"
forma_aggancio: policy
sistema_owner: "[[Processo-Validazione-Pilot]]"
---

# AIOS — MVP, confine operativo

> [!info] In una frase
> MVP = **contabilizzazione automatica fatture + integrazione GBSoftware**. Tutto il resto è post-MVP. **No GBSoftware → no pilot.**

## Confine netto

> [!warning]
> MVP = **contabilizzazione automatica delle fatture + integrazione GBSoftware**. Tutto il resto (scadenziario autonomo, sollecito clienti, advisory finanziario) è **post-MVP**, anche se è parte della visione.

## Perché proprio questo

Il pain point più significativo di uno studio commerciale è la **riclassificazione manuale delle fatture** nel giusto conto e nella giusta voce di stato patrimoniale/conto economico, seguendo la legislazione corrente. Settimane di lavoro per ogni cliente dello studio, interamente eseguite a mano dal dipendente. Il demo di cinque minuti che porto a mio padre è: "dammi le fatture, ti vedi lo stato patrimoniale e il conto economico nel gestionale GB senza toccare niente".

## GBSoftware come gate vincolante

Lo studio di mio padre usa **GBSoftware**. L'integrazione è **Phase 10 — primary deliverable** del repo, ancora da completare al 2026-04-13. **No GBSoftware → no pilot.** Non è una feature negoziabile.

Vedi [[KR1.1 — Phase 10 GBSoftware completata]] e [[AIOS-Intervista-Esperto-GBSoftware]].

## Ripriorizzazione post-MVP (dopo intervista 2026-04-19)

Ordine post-MVP aggiornato alla luce dell'evidenza raccolta:

1. **Scadenziario autonomo con alert** — era già in roadmap ma sale al primo posto post-MVP. Giustificazione: è l'ossessione dichiarata del titolare (D19), è errore tipico ricorrente (D18), ed è direttamente collegato alla soglia pilot ≥95% no-segnalazioni-AdE.
2. **Deposito bilancio al Registro Imprese** — emerso come pain #2 (D17.2). Integrazione esterna aggiuntiva, non prevista oggi. Pilot o post-MVP da decidere (vedi Domande aperte).
3. **Agente advisory finanziario** — scende di priorità rispetto alla versione precedente. Resta in roadmap ma non è più il "prossimo dopo MVP".
4. **Agente consulenza del lavoro** — domanda insoddisfatta confermata dall'intervista (D8: servizio richiesto dai clienti e non offerto). Rafforza ICP "commercialista + consulenza del lavoro".

## Domande aperte

> [!question]
> - **Deposito bilancio al Registro Imprese (pain #2 D17.2)**: integrazione esterna aggiuntiva — dentro pilot o post-MVP? Decisione da prendere prima del go-live.
> - **Archivio documenti su unità esterna centrale (D13)**: come la lettura di AIOS si aggancia alla fonte dei documenti fuori da GBSoftware?

## Collegamenti

- [[Sistema-Agentico-Studio]] — MOC del progetto
- [[KR1.1 — Phase 10 GBSoftware completata]]
- [[AIOS-Intervista-Esperto-GBSoftware]]
- [[AIOS-Intervista-Padre-Domande-KB]] — D17, D18, D19, D8
