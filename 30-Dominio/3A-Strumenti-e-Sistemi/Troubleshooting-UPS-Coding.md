---
tipo: processo
creato: 2026-04-13
aggiornato: 2026-04-14
stato: attivo
tags:
  - processo/troubleshooting
  - strumenti/claude-code
  - metodo/ups
area: strumenti
---

> [!info] In una frase
> Adattamento al coding/debugging del metodo **UPS (Unified Problem Solving)** di Procter & Gamble (sistema IWS): ogni azione su un bug si basa su **evidenze oggettive** raccolte nel punto in cui il fenomeno accade, non su supposizioni lette da pezzi sparsi di codice.

## Origine

Metodo imparato in [[Procter-And-Gamble]] dentro il framework **IWS (Integrated Working System)**, dove il motore di problem solving si chiama **UPS (Unified Problem Solving)**. Principio fondante: *zero-loss mindset* + *go and see* (gemba) — non si diagnostica un problema dalla scrivania, si va dove il fenomeno accade e si raccolgono dati prima di ipotizzare.

## Principio non negoziabile

> [!danger] Regola zero
> **Niente azioni su supposizioni.** Ogni passo deve poggiare su un dato letto direttamente dal codice o da un log osservato in esecuzione. Se un'evidenza manca, il passo successivo è **generarla** (inserire debug log, leggere il file, ispezionare lo stato), non indovinarla.

## Le 5 fasi UPS adattate al coding

### 1. Phenomenon Statement (5W1H)
Descrivere il fenomeno **prima** di qualunque ipotesi, usando le sei dimensioni:

- **What** — cosa succede esattamente? (messaggio d'errore letterale, comportamento osservato)
- **When** — quando accade? (sempre / solo dopo azione X / solo in condizione Y)
- **Where** — dove nel sistema? (quale modulo, quale funzione, quale riga se nota)
- **Who** — chi/cosa lo innesca? (quale input, quale utente, quale chiamante)
- **Which** — quale variante? (quale ambiente, quale versione, quale branch)
- **How** — come si manifesta? (crash / output sbagliato / lentezza / silent failure)

Se una delle sei dimensioni è vuota, **la si riempie prima di procedere**. Un phenomenon statement vago produce diagnosi vaghe.

### 2. Physical Analysis
Capire il **meccanismo** che produce il fenomeno. Nel coding significa:

- Leggere il codice nel punto esatto del fenomeno (non "pezzi sporadici in giro").
- Inserire **debug log strategici** prima e dopo il punto sospetto per osservare lo stato reale.
- Eseguire e **leggere i log oggettivi**, non ciò che ci si aspetta di vedere.

### 3. Conditions
Elencare le condizioni che **devono essere vere** perché il fenomeno si verifichi. Ogni condizione è una riga confermata da evidenza, non da intuizione.

### 4. Root Cause (5-Why sulle condizioni)
Applicare **5-Why** a ciascuna condizione, non al fenomeno generico. Ogni "perché" deve avere una risposta supportata da evidenza (riga di codice, valore di log), altrimenti ci si ferma e si genera l'evidenza mancante.

### 5. Countermeasure → Verify → Standardize
- **Countermeasure**: fix mirato alla root cause, non al sintomo.
- **Verify**: riprodurre lo scenario originale e confermare che il fenomeno è scomparso, **con log che lo dimostrano**.
- **Standardize**: se il pattern di bug può ripetersi, catturare la lezione (regola di review, test di regressione, nota nel vault).

## Come si applica a una sessione con Claude Code

> [!tip] Comportamento atteso di Claude Code in debug
> 1. **Non proporre fix** prima di aver completato il Phenomenon Statement.
> 2. **Default: inserire debug log** e far girare il codice per raccogliere dati, invece di leggere pezzi sparsi e ipotizzare.
> 3. Ogni ipotesi va dichiarata **come ipotesi da verificare**, con il check specifico che la confermerebbe o la smentirebbe.
> 4. Se il founder non è esperto del dominio tecnico, Claude **non** si limita a chiedere conferma: raccoglie l'evidenza da solo e la presenta.

## Anti-pattern da evitare

- **Fix a tentativi** ("provo a cambiare X, vediamo se funziona") senza aver letto i log.
- **Diagnosi da lettura sporadica**: leggere 3 file a caso e formulare una teoria — è esattamente ciò che il metodo vieta.
- **Root cause dichiarata senza 5-Why sulle condizioni**: fermarsi al primo "perché" plausibile.
- **Verifica assente**: dichiarare "sistemato" senza riprodurre lo scenario originale e confermare con log.

## Implementazione come Skill Claude Code

Dal 2026-04-14 questo processo vive anche come **skill globale** di Claude Code: `~/.claude/skills/troubleshooting-ups/SKILL.md`. Attivazione automatica su task di diagnosi causa radice (la `description` è scritta stretta per evitare misfire su scrittura feature / refactor / typo triviali) + invocazione esplicita con `/troubleshooting-ups`. Scope globale: disponibile in ogni progetto senza duplicazione. Motivazione e pattern generale: vedi [[Decisione-Skill-vs-CLAUDE-md]].

## Collegamenti

- [[Decisione-Adozione-UPS-Coding]] — decisione che adotta questo processo
- [[Decisione-Skill-vs-CLAUDE-md]] — pattern Skill-vs-CLAUDE.md applicato a questo processo
- [[Valori-Fondamentali#Efficacia]] — colpire il bersaglio vero, attingendo alla fonte giusta
- [[Valori-Fondamentali#Velocità]] — velocità senza efficacia è rumore; UPS protegge l'efficacia
- [[Processo-Quality-Pillar-Coding]] — framework complementare per quality gate (perdite #3, #6, #7)
- [[Procter-And-Gamble]] — contesto IWS da cui derivano UPS e Quality Pillar
- [[Strumenti-Claude-Code]]
