---
tipo: architettura
creato: 2026-04-26
aggiornato: 2026-04-26
stato: attivo
progetto: "[[Sistema-Agentico-Studio]]"
tags:
  - aios/architettura
  - prodotto/design
area: prodotto
pillar_primario: "[[Prodotto-Pillar-Delivery-Piloti]]"
pillar_secondari:
  - "[[Vendite-Pillar-Sales-Positioning]]"
forma_aggancio: asset
sistema_owner: "[[Processo-Quality-Pillar-Coding]]"
---

# AIOS — Architettura a tre strati

> [!info] In una frase
> [[Sistema-Agentico-Studio]] **non è "AI con qualche SOP a corredo"**: è un sistema a **tre strati inseparabili** — vault Obsidian (knowledge) + processi lean (SOP) + agenti AI (esecuzione). Ogni strato senza gli altri non funziona.

## Strato 1 — Vault Obsidian (substrato di conoscenza)

Modello **ibrido** a due livelli:

- **Vault baseline comune** a tutti gli studi, mantenuto da me, aggiornato periodicamente sulla base delle normative italiane emesse dallo Stato. Asset centrale e difendibile.
- **Vault per-studio agganciato al baseline**, co-costruito col cliente in fase di onboarding per strutturare le SOP sui bisogni e sul design specifico dello studio.

## Strato 2 — Processi lean su SOP

Flussi operativi con output ben definiti, responsabili, trigger. È il ponte tra knowledge e agenti: rende il lavoro ripetibile quindi automatizzabile.

## Strato 3 — Agenti AI operativi

I cinque agenti leggono dal vault come fonte di verità, eseguono i task dentro i processi lean definiti sopra, escalano al commercialista tramite [[AIOS-Architettura-Agenti#Review e validazione come invariante|Review/Validation Agent]] quando la confidenza è bassa.

## Perché funziona solo l'intero sistema

> [!tip]
> Uno studio caotico non può essere automatizzato direttamente: manca la ripetibilità. Ma un puro intervento lean senza AI resta uno sforzo umano. L'unicum è **l'ordine che abilita l'AI, e l'AI che esegue dentro l'ordine**. Questo è anche il valore asimmetrico che porto io: ingegnere Lean + futuro consulente del lavoro = il ponte raro tra i due mondi (vedi [[Identità]]).

## Domande aperte

> [!question]
> - Il vault baseline comune: chi lo aggiorna quando sono in consulenza full-time? Servirà un meccanismo di update sostenibile.

## Collegamenti

- [[Sistema-Agentico-Studio]] — MOC del progetto
- [[AIOS-Architettura-Agenti]] — strato 3 in dettaglio
- [[Prodotto-Vault-Substrato-Di-Prodotto]] — vault come asset di prodotto
- [[Identità]] — l'asimmetria Lean + giuridico
