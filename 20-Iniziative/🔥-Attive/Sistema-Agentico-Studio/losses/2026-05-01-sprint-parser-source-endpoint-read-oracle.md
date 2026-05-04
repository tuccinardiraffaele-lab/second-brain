---
tipo: loss
creato: 2026-05-01
aggiornato: 2026-05-01
stato: chiusa
progetto: "[[Sistema-Agentico-Studio]]"
pillar: quality
livello: 1
failure-mode: "guardia sintattica (`isalnum()`) sostituisce guardia semantica (whitelist contro registry di campi gestiti) su parametro path-interpolato in SQL → information disclosure"
classificazione-chiusura: A
tags:
  - loss/sicurezza
  - loss/defense-in-depth
  - loss/sprint-parser-estensione
area: prodotto
---

# Sprint Parser Estensione — Endpoint `source` come read-oracle

## Fenomeno

`GET /v1/clienti/{client_id}/profile/{campo}/source` accettava `campo` filtrato solo da `campo.replace("_", "").isalnum()`, interpolato direttamente in `SELECT {campo} FROM client_complete_profiles`. Pass: `email`, `codice_fiscale`, `partita_iva`, `pec_email`, `iban` — qualsiasi colonna PII presente sul profilo. In più `try/except Exception: pass` sulla query nascondeva l'errore Postgres ma abortiva la transazione, facendo fallire silenziosamente le query successive.

## Causa base

Doppia guardia mancante:
1. **Whitelist sintattica vs semantica**: `isalnum()` valida la *forma* del nome colonna (anti-injection di metacaratteri SQL), non la *destinazione semantica* (è una colonna che il framework intende esporre via API tracciabilità?). Il guard giusto è `campo not in FIELD_POLICIES → 404`, lo stesso registry che il consumer usa per decidere il merge.
2. **`try/except Exception: pass` su path Postgres**: un `ProgrammingError` su nome colonna inesistente abortisce la transazione corrente; le query successive ricevono `InFailedSqlTransaction`. Lo swallow non è "non determinismo locale" — corrompe l'intera richiesta.

## Strumento applicato

UPS livello 1 in-line durante review giro 1 dello skill `iterate`. Causa identificata staticamente dal codice (review reviewer subagent), defect aperto in `.brain/autonomous-maintenance/defects/open/`, fix mirato + test di regressione `test_get_profile_field_source_404_for_unwhitelisted_campo` con 6 campi forbidden + assert `session.execute.assert_not_called()`.

## Classificazione di chiusura

**A** — violazione AC D-5 (tracciabilità fonte tramite API che esponga SOLO i campi profilo dichiarati nel framework, non l'intero schema). Il defect è promosso e chiuso, fix applicato in giro 1.

## Lezione riusabile

> *Quando un parametro path/query viene interpolato in identifier SQL, la whitelist deve essere **semantica** (registry-driven) non **sintattica** (regex sul nome). Lo stesso registry che il flusso applicativo usa per decidere cosa fare è anche il guard più chiaro per cosa esporre.*

Cross-pattern: già visto nella loss [[2026-04-29-r1-apply-manual-correction-sql-injection]] (POST `/correct` aveva whitelist semantica sin dall'inizio via `KNOWN_PROFILE_COLUMNS`; il GET `/source` introdotto Sprint Parser Estensione l'aveva persa). Coerenza: stesso servizio deve usare lo stesso registry per validazione su tutti gli endpoint che toccano lo stesso modello.

Pattern di rule-of-thumb: **mai swalloware `Exception`** dentro una transazione Postgres aperta — l'errore non si annulla, la sessione resta in stato fallito.

## Sorgente brain locale

Sorgente: `.brain/autonomous-maintenance/defects/closed/AIOS-Studio-Sprint-Parser-Estensione-Source-Endpoint-Read-Oracle-2026-05-01.md`
