---
tipo: concetto
creato: 2026-04-26
aggiornato: 2026-04-27
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
> MVP = **6 use case end-to-end** che coprono il ciclo intake → contabilità → adempimenti → scadenze → validazione, con **integrazione GBSoftware** come gate vincolante. Tutto ciò che non è in lista è **fuori scope esplicito**, anche quando appartiene alla visione.

## I 6 use case dentro l'MVP

Verità di prodotto consolidata dalla verifica codice del 2026-04-27 (vedi [[AIOS-Sanitizzazione-Note-Vault]]).

1. **Intake documentale** — ricezione e classificazione di FatturaPA, CU, bilanci PDF, altri documenti studio. Owner: DocumentAgent.
2. **Apertura pratica** — apertura automatica di pratica AIOS contestuale al cliente, con stato workflow inizializzato. Owner: orchestration + practice-context-service.
3. **Contabilità operativa** — contabilizzazione fatture con classificazione SP/CE secondo regime contabile del cliente. Owner: AccountingAgent.
4. **Adempimenti fiscali standard** — generazione output per dichiarativi/bilanci nei flussi standard (no advisory complesso). Owner: FiscalAgent.
5. **Scadenze e task** — tracking scadenze fiscali con alert proattivi e routing task interni. Owner: workflow-governance-service (motore presente, esposizione API in corso, vedi [[AIOS-Verifica-Roadmap-Agenti]]).
6. **Validazione output** — validazione indipendente con soglia di confidenza ed escalation umana. Owner: ValidationAgent + Human Review Surface.

> [!warning] GBSoftware come gate vincolante
> L'integrazione con **GBSoftware** è **Phase 10 — primary deliverable** del repo. **No GBSoftware → no pilot.** Non è una feature negoziabile. Vedi [[KR1.1 — Phase 10 GBSoftware completata]] e [[AIOS-Intervista-Esperto-GBSoftware]].

## Fuori scope MVP (esplicito)

> [!danger] Cosa NON entra nel pilot 2026-05-10
> Nessuna delle voci sotto è "non importante" — sono **fuori dal perimetro MVP per scelta**. Promettere uno solo di questi al padre rompe il confine e brucia credibilità.

- **Payroll / buste paga** — fuori MVP. Resta nella visione del filone consulenza del lavoro post-abilitazione.
- **Audit verso enti pubblici** — fuori MVP. Richiede compliance e tracciabilità che non sono in scope per il pilot interno.
- **Tax advisory complesso** — fuori MVP. L'agente advisory finanziario è rinviato (vedi sotto).
- **Labor advisory** — fuori MVP. Citato in intervista ma non ancora nel codice (vedi [[AIOS-Verifica-Roadmap-Agenti]]).
- **Ricerca normativa autonoma** — fuori MVP. Lo strato 1 (knowledge-reference-service) è **PARZIALE**: esiste come baseline ma manca auto-update normativo (vedi R3 in [[AIOS-Rischi-Pilot]] e Phase-10-Guardrail nel `.brain/`).

## Perché proprio questi 6 use case

Il pain point più significativo di uno studio commerciale resta la **riclassificazione manuale delle fatture** nel giusto conto SP/CE seguendo la legislazione corrente — settimane di lavoro per cliente, eseguite a mano. Il demo da 5 minuti al padre è: *"dammi le fatture, ti vedi stato patrimoniale e conto economico nel gestionale GB senza toccare niente"*.

I 6 use case allargano il demo dal singolo "contabilizza fatture" al **ciclo end-to-end** che il padre osserverà nel pilot, perché le soglie di successo (vedi [[Decisione-Soglie-Pilot-AIOS]]) misurano:

- accuratezza classificazione voci ≥ 80% (use case 3)
- scadenze senza segnalazioni AdE ≥ 95% (use case 5)
- quadratura trimestrale entro fine mese successivo (use case 3 + 4)

Ridurre l'MVP a "solo contabilizzazione" lascia scoperto il gate scadenze, che è la **soglia pilot più stringente**.

## Ripriorizzazione post-MVP (dopo intervista 2026-04-19)

Ordine post-MVP aggiornato alla luce dell'evidenza raccolta:

1. **Scadenziario autonomo con alert** — già dentro MVP come use case 5, ma il completamento (esposizione API + scheduler automatico) sale al primo posto post-MVP. Giustificazione: ossessione dichiarata del titolare (D19), errore tipico ricorrente (D18), legato alla soglia ≥95% no-segnalazioni-AdE.
2. **Deposito bilancio al Registro Imprese** — emerso come pain #2 (D17.2). Integrazione esterna aggiuntiva. Pilot o post-MVP da decidere (vedi Domande aperte).
3. **Agente advisory finanziario** — scende di priorità. Resta in roadmap ma non è più il "prossimo dopo MVP".
4. **Agente consulenza del lavoro** — domanda insoddisfatta confermata dall'intervista (D8). Rafforza ICP "commercialista + consulenza del lavoro".

## Domande aperte

> [!question]
> - **Deposito bilancio al Registro Imprese (pain #2 D17.2)**: integrazione esterna aggiuntiva — dentro pilot o post-MVP? Decisione da prendere prima del go-live.
> - **Archivio documenti su unità esterna centrale (D13)**: come la lettura di AIOS si aggancia alla fonte dei documenti fuori da GBSoftware?

## Collegamenti

- [[Sistema-Agentico-Studio]] — MOC del progetto
- [[AIOS-Architettura-Agenti]] — i 5 agenti che eseguono i 6 use case
- [[AIOS-Rischi-Pilot]] — rischi architetturali R1-R7
- [[KR1.1 — Phase 10 GBSoftware completata]]
- [[AIOS-Intervista-Esperto-GBSoftware]]
- [[AIOS-Intervista-Padre-Domande-KB]] — D17, D18, D19, D8
- [[AIOS-Sanitizzazione-Note-Vault]] — fonte della riscrittura
