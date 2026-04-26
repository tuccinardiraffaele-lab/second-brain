---
tipo: decisione
creato: 2026-04-13
aggiornato: 2026-04-13
stato: attivo
tags:
  - decisione/strumenti
  - claude-code
  - troubleshooting
area: strumenti
reversibilità: alta
impatto: medio
scadenza-revisione: 2026-07-13
---

## Contesto

Sessione di debugging del 2026-04-13 con Claude Code: per la maggior parte del tempo Claude si è limitato a **supporre** sulla base di pezzi di codice sporadici che andava a leggere, senza proporre dall'inizio di inserire **debug log** per osservare il comportamento reale del codice e risalire alla causa radice.

Il pattern è incompatibile con i [[Valori-Fondamentali#Efficacia|valori di efficacia]]: veloce ma non efficace = rumore. In debug, "veloce" su supposizioni significa ciclare fix a tentativi senza convergere.

## Decisione

**Adotto il metodo UPS (Unified Problem Solving) di P&G — dettagliato in [[Troubleshooting-UPS-Coding]] — come processo standard per ogni sessione di coding/debugging assistita da Claude Code.** Ogni azione si basa su evidenze oggettive (codice letto direttamente, log osservati in esecuzione), mai su supposizioni. Il metodo viene richiamato a livello globale nel `CLAUDE.md` utente, così che ogni sessione di debug lo attivi automaticamente.

## Alternative considerate

1. **Lasciare Claude libero di intuire e correggere dopo** — scartata: esperienza diretta dimostra che non è efficace, produce cicli di fix a tentativi.
2. **Chiedere sempre conferma prima di ogni azione** — scartata: non essendo esperto di coding, le mie conferme produrrebbero comunque output scadente. Sposta il problema, non lo risolve.
3. **Regola generica "niente supposizioni"** senza processo strutturato — scartata: una regola senza metodo non dà a Claude un comportamento operativo riproducibile. UPS fornisce i 5 step concreti da seguire.

## Rationale

- **Evidenza empirica**: la sessione di stasera ha mostrato il costo del pattern attuale.
- **Il metodo è già validato**: UPS è il cuore del sistema IWS (Integrated Working System) di P&G, usato su migliaia di impianti industriali. I principi (Phenomenon Statement via 5W1H, physical analysis, 5-Why sulle condizioni, gemba/osservazione diretta) sono trasferibili al coding.
- **Protegge il non-esperto**: il processo forza Claude a raccogliere evidenza da solo invece di scaricare la decisione sul founder che non ha l'expertise tecnica per validarla.
- **Coerente con i valori**: efficacia (colpire il bersaglio vero) e produttività (velocità × efficacia) sono preservate solo se l'efficacia non va a zero per supposizioni errate.

## Rischi e trade-off

- **Rischio: processo percepito come rallentamento** — mitigazione: il tempo speso su debug log ben piazzati è quasi sempre inferiore al tempo speso in cicli di fix a tentativi. Da verificare empiricamente nelle prossime sessioni.
- **Rischio: Claude applica il processo in modo meccanico anche per bug triviali** (typo, errore di import ovvio dalla traceback) — mitigazione: il processo si attiva per debug non banali; per fix ovvi dalla traceback, evidenza = traceback stesso, quindi lo step 1 è già completo.
- **Trade-off accettato**: alcune sessioni di debug diventeranno più lunghe in tempo di wall-clock, ma più corte in numero di iterazioni fallite.

## Revisione

Rivedere entro [[Scadenziere#2026-07-13]] — criteri di successo:

- Nelle sessioni di debug post-adozione, Claude propone debug log **prima** di ipotesi di fix.
- Il numero di cicli "fix a tentativi" percepiti cala rispetto al baseline attuale.
- Il founder sente di avere più controllo sulla diagnosi senza dover essere esperto di coding.

Se i criteri non sono soddisfatti, rivalutare: processo da raffinare, oppure problema da affrontare a un livello diverso (es. strumenti di logging dedicati).

## Note collegate

- [[Troubleshooting-UPS-Coding]] — il processo operativo
- [[Valori-Fondamentali]]
- [[Strumenti-Claude-Code]]
- [[Procter-And-Gamble]]
