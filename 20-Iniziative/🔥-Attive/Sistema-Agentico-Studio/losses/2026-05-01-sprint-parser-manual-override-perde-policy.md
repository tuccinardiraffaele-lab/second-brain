---
tipo: loss
creato: 2026-05-01
aggiornato: 2026-05-01
stato: chiusa
progetto: "[[Sistema-Agentico-Studio]]"
pillar: quality
livello: 1
failure-mode: "introduzione di nuova fonte di proposte (manual_override) come side effect tracciabilità, senza registrarla nel framework di priorità che la considera proposta competitiva → al successivo merge la fonte umana viene declassata da automatici"
classificazione-chiusura: A
tags:
  - loss/correctness
  - loss/cross-layer-coupling
  - loss/sprint-parser-estensione
area: prodotto
---

# Sprint Parser Estensione — `manual_override` perde contro automatici nel policy framework

## Fenomeno

Step 5 ha aggiunto la scrittura di una riga audit in `client_field_extractions` con `agente="manual_override"` per ogni `apply_manual_correction` (Sprint R1 T-R1-11), per chiudere il gap di tracciabilità D-5. Ma `FIELD_POLICIES` non aveva `SourceRanking("manual_override", ...)` in nessuna policy: `rank_of("manual_override")` ritornava 9999 (sentinel "agente sconosciuto"). Al successivo evento `practice.field_proposed` per quel campo, il `ProfileFieldMergeConsumer` ricomputava lo stato globale ordinando per priority: la proposta umana priority 9999 perdeva contro qualunque automatica (XBRL=1, gestionale=2, cespiti=3) → manual_override declassato a RIFIUTATA con motivo `policy_override:bilancio_xbrl_parser`. **L'override del padre si perdeva silenziosamente alla prima riproposta automatica.**

## Causa base

Coupling cross-layer non riconosciuto. Step 5 ha trattato l'audit row come "side effect tracciabilità" (gemella di `client_profile_signals` via flusso parallelo) **senza considerare che il MergeConsumer policy-driven la avrebbe vista come proposta competitiva**. Il framework `field_priority_policy` introdotto Step 4 era diventato l'arbitro implicito di "chi vince" su ogni campo del profilo, ma manual_override non ne sapeva niente.

## Strumento applicato

UPS livello 1 durante review giro 1. Il finding emergeva come **nitpick** ("priority 9999 sentinel non desiderato per manual"); promosso a **rosso** dopo aver ricostruito che il side effect dello Step 5 attivava la regressione. Fix:
- `_MANUAL_OVERRIDE = SourceRanking("manual_override", 0)` priority 0 = sopra qualunque automatico.
- Inserito di default in tutte le policy via helper `_policy()`.
- Conditional D-4 (`_conditional_immob_materiali`) controlla `manual_override` **prima** di tutto, garantendo che vinca anche nel branch conditional.
- Test di regressione `test_manual_override_beats_all_automatic_sources` con permutations su 3 fonti (XBRL + gestionale + manual).

## Classificazione di chiusura

**A** — violazione AC Sprint R1 T-R1-11 (l'override umano è autoritativo per definizione, non sovrascrivibile da extractor automatici).

## Lezione riusabile

> *Quando un sistema centralizza la decisione "chi vince" in un framework dichiarativo (policy registry, ranking, FSM, ecc.), aggiungere una nuova fonte richiede DUE registrazioni: (1) il flusso di scrittura, (2) il framework decisionale. Se servono solo "side effect tracciabilità" è quasi sempre un'illusione — i lettori downstream interpretano comunque le righe.*

Pattern UPS: i finding "nitpick" durante review possono nascondere bug semantici significativi quando intersecano cambi recenti in altri layer. La review reviewer ha visto il sentinel come "priority 9999 strano"; UPS ha ricostruito la catena causale fino a "valore corretto a mano si perde" che era il vero problema.

## Sorgente brain locale

Sorgente: `.brain/autonomous-maintenance/defects/closed/AIOS-Studio-Sprint-Parser-Estensione-Manual-Override-Loses-Policy-2026-05-01.md`
