---
tipo: decisione
creato: 2026-04-26
aggiornato: 2026-04-26
stato: attivo
tags:
  - decisione/prodotto
area: prodotto
reversibilità: alta
impatto: medio
scadenza-revisione: 2026-05-10
---

## Contesto

Durante lo sviluppo del pilot [[Football-Trading]], dopo il go-live in paper mode ho dovuto riallineare tutti i modelli al SOTA perché non erano performanti. Il rework è costato **3 giorni di implementazione** che potevano essere evitati con un check dello stato dell'arte in fase di definizione dei requirement.

## Decisione

**Prima di implementare un modello o agente AI, verificare stato dell'arte e best practices per evitare rework di allineamento post-delivery.**

Il check SOTA diventa step obbligatorio nella fase di requirement/design di ogni componente AI.

## Alternative considerate

1. **Nessun check SOTA, iterare post-delivery** — scartata perché il costo del rework (3gg su FT) supera il tempo di ricerca upfront
2. **Check SOTA solo su componenti critici** — applicata su FT come compromesso per non consumare tempo da dedicare ad AIOS; i modelli non critici restano non allineati

## Rationale

Il rework dei modelli FT è costato 3 giorni di implementazione. Questo tempo era evitabile se il check SOTA fosse stato fatto durante la definizione dei requirement del pilota. Il pattern "SOTA check pre-implementazione" converte tempo di ricerca upfront (ore) in saving di rework downstream (giorni).

## Rischi e trade-off

- **Trade-off accettato**: il check SOTA aggiunge tempo in fase di design, ma il saving sul rework post-delivery è maggiore
- **Rischio analysis paralysis**: mitigato limitando il check a fonti accreditate e timeboxando la ricerca (max 2h per componente)

## Revisione

Rivedere entro [[2026-05-10]] (prima del go-live AIOS) — criteri di successo:
- [ ] Il check SOTA è stato eseguito sui componenti AI di AIOS
- [ ] Non si è verificato rework di allineamento post-delivery

## Note collegate

- [[Football-Trading]] — pilot dove è emerso il problema
- [[Sistema-Agentico-Studio]] — primo progetto dove applicare il pattern
- [[Settimanale-2026-W17]] — insight emerso nella review settimanale
