---
tipo: decisione
creato: 2026-04-15
aggiornato: 2026-04-15
stato: attivo
tags:
  - decisione/prodotto
area: prodotto
reversibilità: media
impatto: medio
scadenza-revisione: 2026-06-01
---

## Contesto

Nel brainstorming [[AIOS-Brainstorm-Audit-Primitive-Agentiche]] è emersa la domanda: AIOS Phase 0-9 regge il confronto con le primitive agentiche standard (skill, hook, MCP, sub-agent di Claude Code; visione Jensen GTC 2026)? Il rischio non è "aver sbagliato" ma aver internalizzato un'architettura buona-ma-non-ottimale come se fosse ovvia, portandosi dietro il debito nelle Phase 10-12 senza nominarlo.

Tre strade possibili: audit strutturato, inlining dei gap dentro Phase 11, non fare audit.

## Decisione

**Audit strutturato delle primitive agentiche AIOS vs Claude Code, materializzato come nota viva `.brain/architecture/Audit-Primitive-Agentiche-AIOS.md` nel repo AIOS, agganciato al punto 7 della roadmap [[Brain-Framework-Implementazione]] — anticipato da "post-go-live" a "in questi giorni". Phase 11 resta pulita: solo feature di prodotto (vault-studio normativo come moat).**

## Alternative considerate

1. **Inlining dei gap dentro Phase 11** — scartata: meno sistematico, rischia di catturare solo i gap che cadono addosso durante il lavoro normativo, non quelli che richiedono confronto attivo con le primitive Claude Code. Meno leggibile come artefatto unico per il planning Phase 12.
2. **Non fare audit affatto** — scartata: Jensen e Claude Code sono specchio retroattivo che può rivelare debito architettonico nominabile. Non sfruttarlo = conferma identitaria per default.
3. **Audit pre-go-live come workstream a sé stante** — scartata per vincolo temporale duro (go-live 2026-05-10, Phase 10 GBSoftware deadline 2026-05-03).
4. **Agganciare a Phase 11 (vault come substrato di prodotto)** — scartata: Phase 11 va mantenuta pulita come feature prodotto (moat normativo). Mescolare audit tecnico con substrato prodotto confonde i due livelli.

## Rationale

- **Punto 7 della roadmap brain è il posto naturale**: applica ad AIOS lo stesso pattern [[Strumenti-Filing-Brain-Globale-Locale]] già validato su Football Trading. La nota di audit nasce dove vivrà — nel `.brain/architecture/` AIOS — non in un posto temporaneo che dopo dovrebbe migrare.
- **Scaffold ora, compilazione a giugno**: lo scaffold vuoto pre-go-live costa 30-45 min, non erode Phase 10. La compilazione (3-4h) avviene post-stabilizzazione go-live, quando le primitive AIOS sono state stress-testate in produzione e i giudizi sono informati dall'uso reale, non speculativi.
- **Output azionabile**: l'audit chiude con una gap-list *ranked* top-3, non una descrizione. Diventa input concreto per planning Phase 12, non documento accademico.

## Rischi e trade-off

- **Rischio 1 — Punto 7 anticipato sottrae tempo a Phase 10 GBSoftware** → go-live slitta. **Mitigazione**: budget duro 3h totali su A1+A2+A3 (scaffold + frontmatter MOC + aggiornamento roadmap). Oltre la soglia, si rivaluta.
- **Rischio 2 — B1 (compilazione) slitta a settembre** per saturazione giugno-agosto (stabilizzazione go-live, secondo esame studio giuridico, eventuale apertura marketing/sales). **Mitigazione**: B1 deliberatamente a metà giugno con 5 settimane di buffer dal go-live; reality-test del 2026-06-01 come checkpoint esplicito.
- **Rischio 3 — Audit diventa accademico** (conferma identitaria invece di ranking che forza scelta). **Mitigazione**: B2 obbliga a top-3 ranked per leva competitiva × effort.
- **Trade-off accettato**: priorità del punto 7 rivista (da post-go-live a in questi giorni) viola la logica originale *"fino al go-live solo tecnico su Phase 10"*. È una scelta consapevole: il seed `.brain/` AIOS era comunque da fare, farlo ora lo aggancia al brainstorming appena chiuso invece di rimandarlo a contesto dimenticato.

## Revisione

Rivedere entro [[Scadenziere#2026-06-01]] — criteri di successo:

- **Scaffold nota audit creato entro 2026-04-20** (dentro budget 3h). Se fallisce → segnale che il bucket 1 non tiene, ripiegare su inlining.
- **Phase 11 partita entro 2026-06-01**. Se non partita e scaffold ancora vuoto → rivalutare: promuovere audit pre-Phase 11 oppure ripiegare su inlining.
- **Compilazione B1 entro 2026-06-15**. Se slitta oltre → audit perde valore per Phase 12 planning, rivalutare.

## Note collegate

- [[AIOS-Brainstorm-Audit-Primitive-Agentiche]] — brainstorming Rumelt che ha prodotto la decisione
- [[Brain-Framework-Implementazione]] — punto 7 della roadmap a cui l'audit è agganciato
- [[Sistema-Agentico-Studio]] — progetto a cui la decisione si applica
- [[Strumenti-Filing-Brain-Globale-Locale]] — pattern brain globale+locale trasferito ad AIOS
- [[Prodotto-Vault-Substrato-Di-Prodotto]] — Phase 11, feature di prodotto (fuori scope audit)
- [[Decisione-Framework-Brain-Globale-Locale]] — decisione architetturale brain globale+locale
- [[Strategia-Attuale]] — bet strategico principale + vincolo reputazionale
- [[OKR-Correnti]] — ambiente di trade-off temporale
