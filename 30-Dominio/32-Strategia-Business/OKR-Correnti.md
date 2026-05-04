---
tipo: processo
creato: 2026-04-13
aggiornato: 2026-05-02
stato: attivo
tags:
  - strategia/okr
  - q2-2026
area: strategia
---

# OKR correnti — Q2 2026

> [!info] In una frase
> Due Objective attivi per il trimestre: portare **AIOS in produzione** e mantenere i **fondamenti della transizione** (studio giuridico, marketing/sales, monitoraggio regolatorio). L'Objective 2 — Football Trading è stato **archiviato il 2026-05-02** dopo la chiusura definitiva del pilota (vedi [[Chiusura-Pilot-Football-Trading]]).

## Diagnosi strategica

Q2 2026 è il trimestre in cui il **bet strategico principale** ([[Sistema-Agentico-Studio]]) va in go-live reale sul primo cliente (studio del padre). Il rischio dominante non è tecnico: è di **focus** — quattro filoni tirano in direzioni diverse e due (studio giuridico, marketing/sales) sono facili da sacrificare proprio quando servirebbero. La sfida è portare AIOS al go-live funzionante senza rompere gli altri tre filoni.

Vedi [[Strategia-Attuale]] per la strategia completa.

## Guiding policy

**Farai:**
- Priorità #1: AIOS go-live, presidio quotidiano finché non è in produzione (FT chiuso, tempo riallocato totalmente qui)
- Studio giuridico: 1.5-2h/giorno lun-ven, presidio costante
- Gate espliciti prima del go-live (metriche pilot con padre, Phase 10 GBSoftware)

**NON farai:**
- Nessun refactor AIOS fuori dalla critical path (**unica eccezione**: integrazione vault Obsidian + integrazioni strutturali correlate)
- Nessuna attività sul filone marketing/sales oltre a decidere quando aprirla
- Nessun B2B sul sistema agentico (vincolo reputazionale)
- Nessun nuovo pilota o esplorazione

## Objective 1 — AIOS Studio in produzione

Portare il sistema agentico al primo go-live reale presso lo studio del padre entro metà maggio.

- [[KR1.1 — Phase 10 GBSoftware completata]]
- [[KR1.2 — Metriche pilot fissate con padre]]
- [[KR1.3 — Go-live studio padre]]

## ~~Objective 2 — Football Trading validato e in orbita~~ (archiviato 2026-05-02)

> [!failure] Objective archiviato
> Pilota Football Trading chiuso definitivamente il 2026-05-02 (sistema strutturalmente in perdita + disallineamento strategico). I tre KR sono chiusi senza target. Vedi [[Chiusura-Pilot-Football-Trading]].

- [[KR2.1 — Paper trading debuggato]] — archiviato
- [[KR2.2 — Paper trading in profitto 30 giorni]] — archiviato
- [[KR2.3 — KPI metrics_analyzer chiariti con AI]] — archiviato

## Objective 3 — Fondamenta della transizione consolidate

Mantenere vivi gli altri tre filoni (studio giuridico, marketing/sales, monitoraggio regolatorio) senza che AIOS li eroda.

- [[KR3.1 — Esami studio giuridico]]
- [[KR3.2 — Decisione apertura filone marketing-sales]]
- [[KR3.3 — Monitoraggio regolatorio AI]]

## Pre-mortem (rischi identificati)

> [!warning] Cause di fallimento più probabili
> 1. **Integrazione GBSoftware** più complessa del previsto → slip go-live AIOS
> 2. **Layer Obsidian AIOS** non sufficientemente completo al go-live
> 3. **Erosione studio giuridico** — l'ora e mezza/giorno salta nelle settimane critiche AIOS

## Piano B (se go-live 10 maggio non è fattibile)

Spostare il go-live e usare il buffer per **consolidare il layer Obsidian**. Il killer della fattibilità è l'**indisponibilità del padre** a raccogliere la knowledge base da inserire nel vault Obsidian.

## Collegamenti

- [[Strategia-Attuale]]
- [[Identità]] · [[Valori-Fondamentali]]
- [[Sistema-Agentico-Studio]] · [[Chiusura-Pilot-Football-Trading]]
- [[AIOS-Chiarire-Metriche-Pilot]] · [[AIOS-Verifica-Roadmap-Agenti]]
- [[Monitoraggio-regolatorio-AI]]
