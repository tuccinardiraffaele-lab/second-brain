---
tipo: scadenziere
creato: 2026-04-16
aggiornato: 2026-05-03
stato: attivo
tags:
  - sistema/scadenziere
  - operazioni
area: operazioni
---

# Scadenziere

> [!info] A cosa serve
> Raccoglie follow-up, review programmate e commitment schedulati fuori dall'orizzonte della settimana corrente. Le note sorgente puntano qui via `[[Scadenziere#YYYY-MM-DD]]`. Ogni entry ha data, fonte, azione attesa.

> [!tip] Come si usa
> - **Lettura**: scansione almeno a cadenza settimanale in chiusura review (skill `weekly`), più scansione mensile per le scadenze >30gg.
> - **Scrittura**: quando dichiari un impegno con data futura (>7gg), registra qui. Wikilink dalla nota sorgente con anchor di data.
> - **Chiusura**: spostare in `## Orizzonte agosto 2026

### 2026-08-02 — Revisione chiusura pilot Football Trading
- **Fonte**: [[Chiusura-Pilot-Football-Trading]]
- **Azione**: verificare che la chiusura abbia liberato valore — tempo confluito su AIOS, no rientro impulsivo, loss FT riusate cross-progetto.

### 2026-08-10 — Revisione soglie pilot AIOS
- **Fonte**: [[Decisione-Soglie-Pilot-AIOS]]
- **Azione**: verificare se le tre soglie pilot sono state raggiunte sul periodo di osservazione post go-live → promozione AIOS oltre il pilot o stop.

## Trigger evento-driven (no data fissa)

### Pre-apertura filone B2B AIOS — Security audit codebase
- **Fonte**: [[Studio-AI-2026-05-01]] · [[Studio-AI-2026-05-03]] · [[Strategia-Attuale#Il vincolo di reputazione (principio non negoziabile)|vincolo reputazionale B2B]]
- **Trigger**: post go-live AIOS studio padre + decisione di aprire il filone B2B (vendita ad altri studi).
- **Azione**: eseguire security audit del codebase AIOS via **Claude Security** (public beta Enterprise da 2026-05-01) prima del primo prospect B2B. Output: scan + dismissioni documentate + patch generate. Riduce rischio reputazionale di vulnerabilità esposte a peer professionali.

## Archivio` con esito sintetico (fatto/slittato/cancellato) quando la data passa.

## Orizzonte prossimi 14 giorni

### 2026-04-30 — Intervista esperto GBSoftware (dominio di processo)
- **Fonte**: [[AIOS-Intervista-Esperto-GBSoftware]] · [[KR1.1 — Phase 10 GBSoftware completata]]
- **Azione**: eseguire intervista al supervisore contabilità clienti dello studio su flussi GBSoftware e regole di riclassificazione fatture. Spostata da 2026-05-01 (festivo) a giovedì 2026-04-30. Sblocca binario "dominio di processo" della Phase 10.

### 2026-05-02 — Pianificare seconda intervista padre (follow-up KB)
- **Fonte**: [[AIOS-Intervista-Padre-Follow-Up]]
- **Azione**: fissare orario, confermare con padre, preparare domande su bus-factor, cliente fuori standard, processo quadratura.

### 2026-05-03 — Seconda intervista padre (follow-up KB AIOS)
- **Fonte**: [[AIOS-Intervista-Padre-Follow-Up]]
- **Azione**: eseguire intervista su tre aree rimaste aperte dopo la prima sessione del 2026-04-19.

### 2026-05-03 — Stub finanza business completati
- **Fonte**: reminder daily 2026-04-16
- **Azione**: popolare [[Finanza-Business-Economics-FT]], [[Finanza-Business-Pricing-AIOS]], [[Finanza-Business-Pricing-FT]].

### 2026-04-28 — Review template Pianificazione-Giornaliera
- **Fonte**: [[Dashboard]] · [[Decisione-Sistema-Pianificazione-Giornaliera]]
- **Azione**: valutare se il template sta reggendo la cadenza serale dopo 2 settimane di uso.

## Orizzonte maggio 2026

### 2026-05-03 — Phase 10 GBSoftware completata
- **Fonte**: [[KR1.1 — Phase 10 GBSoftware completata]]
- **Azione**: gate tecnico del go-live AIOS.

### 2026-05-10 — Go-live AIOS studio padre
- **Fonte**: [[KR1.3 — Go-live studio padre]] · [[Strategia-Attuale]]
- **Azione**: primo go-live reale del sistema agentico.

## Orizzonte giugno 2026

### 2026-06-01 — Review decisione AIOS Audit Primitive Agentiche
- **Fonte**: [[AIOS-Audit-Primitive-Agentiche]]
- **Azione**: verificare criteri di successo dichiarati nella nota.

### 2026-06-30 — Foundation pillar Delivery piloti: nota canonica framework + template riusabile
- **Fonte**: [[Prodotto-Pillar-Delivery-Piloti]] (F-HC1, F-HC2)
- **Azione**: creare nota `Framework-Delivery-Piloti-Doppio-Livello` (dichiarazione principio) + template riusabile `.brain/` + vault Obsidian locale forkabile. Chiude Foundation se anche F-HC3 (≥1 evidenza per pilota) e F-HC4 (regole scambio) verificati.

## Orizzonte luglio 2026

### 2026-07-13 — Review adozione metodo UPS Coding
- **Fonte**: [[Decisione-Adozione-UPS-Coding]]
- **Azione**: verificare criteri di successo post-3 mesi di uso.

### 2026-07-13 — Review Dashboard auto-generata via Bases
- **Fonte**: [[Strumenti-Dashboard-Auto-Generata-Via-Bases]]
- **Azione**: verificare criteri di successo del setup Bases.

### 2026-07-15 — Review hardening Basic Memory
- **Fonte**: [[Decisione-Hardening-Basic-Memory]]
- **Azione**: spot check 20 note random per mutazioni byte-level attribuibili a BM.



## Archivio

<!-- spostare qui entry chiuse con esito: fatto / slittato / cancellato -->

### 2026-04-17 — Call padre pianificazione KB AIOS: archiviato
- **Fonte**: [[Crescita-Priorità-Correnti]] · [[AIOS-Brainstorm-Knowledge-Map-Padre]]
- **Esito**: fatto — intervista KB eseguita il 2026-04-18, prima tranche chiusa ([[AIOS-Intervista-Padre-Domande-KB]]).

### 2026-04-18 — Ripresa interview processi operativi: archiviato
- **Fonte**: daily 2026-04-14 · [[Brain-Framework-Implementazione]]
- **Esito**: assorbita nella priorità 1 di [[Settimanale-2026-W16|W17]] — finire interview vault globale (aree residue).

### 2026-04-26 — FT paper trading debuggato: archiviato
- **Fonte**: [[KR2.1 — Paper trading debuggato]]
- **Esito**: fatto con 8 giorni di anticipo — debug P&L chiuso il 2026-04-18, pilota in orbita.

### 2026-04-19 — Soglie metriche pilot AIOS fissate con padre: archiviato
- **Fonte**: [[KR1.2 — Metriche pilot fissate con padre]] · [[AIOS-Chiarire-Metriche-Pilot]]
- **Esito**: fatto — chiusa con 8 giorni di anticipo in sessione intervista ([[AIOS-Intervista-Padre-Domande-KB]] G26). Soglie: quadratura trimestrale entro fine mese successivo (ordinarie), classificazione voci ≥80%, scadenze senza segnalazioni AdE ≥95%.

### 2026-04-17 — Stub Angelini Pharma: archiviato
- **Fonte**: microattività daily 2026-04-15/16
- **Esito**: fatto — nota [[Angelini-Pharma]] già compilata il 2026-04-15 (hub capitale trasferibile con primo asset [[Pattern-Corporate-Business-Operations]]).
