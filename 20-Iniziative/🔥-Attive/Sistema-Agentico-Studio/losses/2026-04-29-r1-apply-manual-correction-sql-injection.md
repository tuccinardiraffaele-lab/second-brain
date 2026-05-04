---
tipo: loss
creato: 2026-04-29
aggiornato: 2026-04-29
stato: chiusa
progetto: "[[Sistema-Agentico-Studio]]"
pillar: quality
livello: 1
failure-mode: "validazione applicata solo al bordo del sistema (route HTTP) e non al bordo del modulo (service di dominio), lasciando SQL-injection-friendly il chiamante interno"
classificazione-chiusura: A
tags:
  - loss/sicurezza
  - loss/defense-in-depth
area: prodotto
---

# R1 — `apply_manual_correction` interpola identifier SQL non whitelisted

## Fenomeno

`ProfileEnrichmentService.apply_manual_correction()` interpolava `signal_key` direttamente in fstring SQL (INSERT + UPDATE su `client_complete_profiles`). La whitelist `KNOWN_PROFILE_COLUMNS` era applicata solo nel route handler. Qualunque altro chiamante (consumer, batch job, replay tool) bypassava la difesa: il pattern era SQL-injection-friendly al livello di interfaccia di dominio.

## Causa base

Difesa al "bordo del sistema" (route HTTP) considerata sufficiente. Sottovalutata la regola complementare: **un service di dominio è esso stesso un bordo per chiamanti futuri**. La regola "validate at boundaries" non significa solo "input utente", significa "input non controllato dal modulo che lo riceve".

## Strumento applicato

UPS in revisione post-implementazione (giro 1 reviewer). Il fix è classico defense-in-depth: replico la stessa whitelist all'inizio del metodo dominio.

## Classificazione di chiusura

**A — violazione di AC esistente** (gli AC di sicurezza R1 richiedono che nessun input utente raggiunga identificatori SQL non validati). Non gap di AC.

## Lezione riusabile

Quando una validazione viene aggiunta al bordo route, è una decisione **contestuale al chiamante corrente**, non al sistema. Domanda da porsi prima di chiudere il task: *"se domani chiamo questo metodo da un consumer/job/replay tool, la difesa regge?"*. Se no, la validazione va spostata o duplicata nel dominio. Niente shortcut. Vale per sql identifier, ma anche per: format date, range numerici, enum values, path traversal, regex denylist.

Generalizzazione: **valida ai bordi del modulo, non solo ai bordi del sistema**. I moduli sono i veri perimetri di trust nel codice.

## Sorgente brain locale

Sorgente: `.brain/autonomous-maintenance/defects/closed/AIOS-Studio-R1-Apply-Manual-Correction-SQL-Injection-2026-04-29.md`

## Note collegate

- [[Sistema-Agentico-Studio]]
