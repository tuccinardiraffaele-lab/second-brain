---
tipo: loss
creato: 2026-04-20
aggiornato: 2026-04-20
stato: chiusa
progetto: "[[Football Trading]]"
pillar: Quality
livello: 2
failure-mode: UPDATE con scope per chiave logica (signal_id) invece che per riga semantica (order_type='green') copia valori su righe che non possono ospitarli
classificazione-chiusura: B
tags:
  - loss/data-integrity
  - loss/sql-scope
area: prodotto
---

## Fenomeno

Query di baseline sul 19/04 rileva 12 `signal_id` con due `green` row ciascuno. Entrambe le righe portano lo **stesso `pnl_final`**, anche se una è `FAILURE` non-settled (tentativo di chiusura abortito) e l'altra è la chiusura autoritativa. Query ingenue `SUM(pnl_final)` senza filtro `settled=TRUE` contano doppio. Ispezione ulteriore: anche le 1180 righe `entry` dello storico portano `pnl_final` popolato — non dovrebbe esistere su una entry row. Il dato è semanticamente nel posto sbagliato.

## Causa base

`PnLSettler` al settle del market eseguiva:

```sql
UPDATE trade_orders
   SET pnl_final = $3, pnl_gross = $1, commission_share = $2,
       outcome_source = $4, outcome_actual = $5
 WHERE signal_id = $6 AND pnl_final IS NULL
```

Lo scope `WHERE signal_id = $6` includeva **tutte le righe** del signal (`entry` + qualunque `green`), non solo la riga autoritativa della chiusura. Il filtro `pnl_final IS NULL` garantiva idempotenza ma non ristrettezza semantica: prima volta che si vedeva una riga, la riempiva, indipendentemente dal fatto che quel dato avesse senso su quella riga.

Root cause: **il concetto di "riga autoritativa del settlement" non era dichiarato nello schema né nel codice**. Il settler ragionava per chiave logica (signal_id) invece che per riga semantica (green settled).

## Strumento applicato

**Audit read-only** dei consumer di `trade_orders` (mapping 10 componenti critici) per capire l'impatto del cambio di scope prima di toccare codice. Poi fix scope a `WHERE signal_id = $6 AND order_type = 'green'` (commit `f6765e5`) + bonifica dati storici (script SQL idempotente: 14 green non-settled + 1180 entry azzerate, invariante Σ pnl_final settled preservato −3556.62 €).

## Classificazione di chiusura

**B** — gap di AC. Lo schema `trade_orders` non dichiarava vincoli sul "dove vive il pnl_final": il settler poteva scriverlo ovunque nel signal. L'AC nuovo introdotto: *"pnl_final esiste solo su righe `order_type='green'` e rappresenta il P&L netto dell'intera chiusura del signal"*. Persistenza B (una sola green row per signal) rende l'invariante enforceable. Dopo bonifica dati e fix codice, invariante verificata con AC-16 / AC-08 del piano master.

## Lezione riusabile

**Un UPDATE con `WHERE chiave_logica` è un bug design in attesa di accadere se la chiave logica identifica più righe con semantiche diverse.** Ogni volta che scriviamo un UPDATE su tabella che può contenere righe eterogenee per la stessa chiave (multi-row per signal/user/order/whatever), dobbiamo chiederci: *"questo dato ha senso su TUTTE le righe che matcherà?"*. Se la risposta è "dovrebbe, ma solo se sono coerenti fra loro", è il segno che manca una dimensione discriminante nel WHERE.

Test operativo riutilizzabile: **per ogni UPDATE in audit, leggere il WHERE e nominare esplicitamente le righe target**. Se la descrizione contiene "tutte le righe del signal" ma poi si aggiunge "ma solo quella dovrebbe", restringi il WHERE o aggiungi la dimensione. Questo stesso pattern va verificato su `liquidity_gate_decisions`, `trade_outcomes`, e qualsiasi altra tabella dove più righe coesistono per lo stesso `signal_id`.

## Sorgente brain locale

Sorgente: `.brain/debug/green-failure-rows-pnl-final-copied.md` (fix-committato `f6765e5`).
Audit correlato: `.brain/planning/2026-04-20-audit-lifecycle-readers.md`.
Script bonifica: `scripts/bonifica_green_failure_pnl.py`.
