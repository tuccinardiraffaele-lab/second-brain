---
tipo: concetto
creato: 2026-04-26
aggiornato: 2026-04-26
stato: attivo
tags:
  - strategia/mappa
  - pillar/foundation
area: strategia
pillar_primario: P1
pillar_secondari: []
forma_aggancio: input
sistema_owner: "[[Processo-Review-Cadence]]"
---

# Watch — Promozioni candidate sulla mappa pillar↔sistemi

> [!info] In una frase
> Registro dei sotto-processi/concept oggi assorbiti nella [[Strategia-Mappa-Pillar-Sistemi]] ma candidati a promozione a sistema autonomo a Stability (Q3 2026), se emergono i trigger dichiarati. Funge da input di [[Processo-Review-Cadence]] per la review mensile/trimestrale.

## Origine

Creato il 2026-04-26 a chiusura della sessione di verifica integrità mappa (post-deliberation 2026-04-25). I 3 watch erano già dichiarati implicitamente nella sezione Stability della mappa; questa nota li centralizza per scansione attiva nelle review.

## Watch attivi

### W1 — `FT-Pattern-Zombie-File-Locali`

- **Stato attuale**: nota di progetto in `20-Iniziative/🔥-Attive/Football-Trading/`, `tipo: debito-tecnico`, `progetto: "[[Football-Trading]]"`
- **Candidato a**: promozione a pattern cross-progetto in `40-Conoscenza/` o `30-Dominio/33-Prodotto-e-Tecnologia/`
- **Trigger di promozione**: seconda occorrenza dello stesso pattern (rilevamento + chiusura zombie file in pipeline) in un secondo progetto. Regola delle ≥2 occorrenze (vedi [[Strumenti-Filing-Brain-Globale-Locale]])
- **Pillar di destinazione**: P2 (Delivery Piloti) come standard tecnico cross-pilot
- **Owner check**: weekly review FT, monthly cross-progetto

### W2 — `Prodotto-Vault-Substrato-Di-Prodotto`

- **Stato attuale**: concept di [[Processo-Costruzione-Vault-dedicato]] (sistema P1 #20)
- **Candidato a**: sistema autonomo P2 con doppio aggancio P7(S)
- **Trigger di promozione**: esistenza di un secondo cliente con vault dedicato deployato (oggi solo studio del padre come pilot AIOS). Quando il vault diventa replicabile su N clienti, il concept ha forma canonica (loss + I/O + owner + frequenza)
- **Pillar di destinazione**: P2 primario, P7(S) per dimensione regolatoria/Garante quando ospita KB di terzi
- **Owner check**: trimestrale, ancorato a milestone B2B AIOS

### W3 — `Processo-Prioritizzazione-Operativa`

- **Stato attuale**: sotto-processo di [[Processo-Pianificazione-Giornaliera]] (assorbito 2026-04-25)
- **Candidato a**: sistema autonomo P1 complementare a Pianificazione Giornaliera
- **Trigger di promozione**: emergere di una loss separata non assorbibile (es. priorità intra-day che cambia per ragioni di compliance/rischio reputazionale richiede audit trail proprio — segnalazione Voce 2 EY in deliberation 2026-04-25)
- **Pillar di destinazione**: P1 primario, P3(S) se trigger compliance
- **Owner check**: mensile in chiusura diario, scan delle ripianificazioni di giornata

## Cosa fa Review Cadence con questa nota

- **Settimanale**: scan rapido se nelle note della settimana è emerso un evento che attiva un trigger (es. nuovo caso zombie-file in AIOS)
- **Mensile**: review esplicita dei 3 watch — qualcuno è maturo per promozione? Se sì, escalation a sessione di deliberation
- **Trimestrale**: revisione completa, eventuale aggiunta di nuovi watch o chiusura di watch superati

## Collegamenti

- [[Strategia-Mappa-Pillar-Sistemi]] — mappa target
- [[Processo-Allocazione-Conoscenza-Pillar]] — algoritmo che governa le allocazioni
- [[Processo-Review-Cadence]] — sistema consumer di questo input
- [[Strumenti-Filing-Brain-Globale-Locale]] — regola delle ≥2 occorrenze per W1
- [[Processo-Costruzione-Vault-dedicato]] — sistema owner di W2 oggi
- [[Processo-Pianificazione-Giornaliera]] — sistema owner di W3 oggi
