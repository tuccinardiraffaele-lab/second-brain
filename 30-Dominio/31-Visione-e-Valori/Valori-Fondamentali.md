---
tipo: concetto
creato: 2026-04-13
aggiornato: 2026-04-13
stato: attivo
tags:
  - valori
  - identità
  - principi
area: visione
---

# Valori fondamentali

> [!info] In una frase
> Sei valori che, letti insieme, descrivono come lavoro: **precisione, chiarezza, velocità, efficacia, affidabilità, produttività**. Non sono una lista: sono un sistema in cui ogni valore dà senso agli altri.

## L'architettura dei valori

> [!tip] Principio unificante
> **Produttività = Velocità × Efficacia.** È moltiplicativo: zero su un asse azzera tutto. Precisione e chiarezza sono le condizioni che permettono all'efficacia di non essere zero. Affidabilità è il collante relazionale che tiene insieme tutto verso gli altri.

## Precisione

**Definizione.** Onorare gli impegni verso gli altri attraverso commitment inequivocabili — date, nomi, perimetro dichiarato. Non è pignoleria estetica: è un valore relazionale.

**Esempio.** Workshop aziendale con agenzia esterna coinvolta. Il capo non dichiarava data, settimana, né persone da coinvolgere. Ho preteso di fissare data specifica e lista nominale — non per rigidità, ma per essere *committenti* verso l'impegno preso con l'agenzia che stava aspettando una risposta.

**Principio operativo.** La precisione ha un tetto: **quando blocca la decisione, diventa paralisi**. Scegliere data e persone serve; scegliere anche orario, aula, disposizione sedie, no — si finisce per non decidere mai.

**Radice emotiva del fastidio.** La vaghezza deliberata altrui la leggo come mancanza di rispetto: sono una persona ragionevole, se c'è una ragione posso capirla. Nascondere il perché mi tratta come se non fossi abbastanza adulto per reggerlo.

## Chiarezza

**Definizione.** Calibrare il messaggio sull'interlocutore. È proprietà della *trasmissione*, non del messaggio — distinta dalla precisione, che è proprietà del contenuto. Si può essere precisi e oscuri, chiari e imprecisi.

**Esempio.** Parlare di coding a un non-tecnico. Dire "ho implementato una chiamata API al modello Anthropic per fare leva sull'LLM" è preciso ma oscuro. Dire "ho reso il tool intelligente facendo leva sull'intelligenza artificiale di Claude" è ugualmente preciso e anche chiaro.

**Principio operativo.** Prima diagnosticare la baseline dell'audience con domande, poi usare **esempi concreti come ponte**: funzionano a doppio livello, non annoiano l'esperto e illuminano il novizio.

## Velocità

**Definizione.** Catturare finestre competitive che si chiudono. L'imperfezione è un prezzo accettabile, non un difetto — purché la soluzione generi valore oggi e sia perfezionabile dopo.

**Esempio positivo.** Troubleshooting system basato su GPT in produzione presso [[Angelini-Pharma]]. Architettura non perfetta, passaggi manuali ancora presenti, ma in produzione a generare vantaggio competitivo ora invece che "mai, perché stavamo aspettando l'architettura giusta".

**Esempio negativo.** Pilot del progetto [[Football-Trading]] deployato una settimana dopo l'inizio dello sviluppo. Risultato: bug review continue nel weekend utile (quello con le partite), pilot non funzionante proprio quando doveva produrre dati, ancora oggi certezza parziale sul debug. **La fretta ha bruciato la finestra che volevo catturare.**

> [!warning] Regola-gate velocità vs fretta
> Prima di spingere il deploy: *"cosa mi aspetto che succeda in produzione, e il pilot lo riproduce fedelmente sulle dimensioni che contano?"*. Se non so rispondere, non sto andando veloce — sto consegnando un esperimento incapace di produrre imparamento utile.

## Efficacia

**Definizione.** Colpire il bersaglio vero, attingendo alla fonte giusta, coprendo il perimetro giusto. È il filtro che dà senso a tutti gli altri valori.

> [!quote] Principio fondante
> **Veloce ma non efficace = superfluo.** Un report consegnato in 15 minuti che pesca dalle fonti sbagliate e copre solo pezzi del processo non è "velocità imperfetta": è rumore.

**Come si tutela (non con micromanagement).**
- **Autonomia** ai collaboratori sul "come": libertà decisionale e creativa.
- **Escalation obbligatoria dei dubbi**: chi ha un dubbio non lo tappa da solo sperando che la propria risposta basti, e nemmeno lo bypassa per non disturbare. Lo porta.
- Il mio ruolo è **backstop sull'ambiguità**, non controllore dell'esecuzione.

## Affidabilità / Commitment

**Definizione.** Mantenere gli impegni dichiarati. Se precisione riguarda il *contenuto* dell'impegno, affidabilità riguarda il *mantenerlo nel tempo*. È il valore che pretendo dagli altri ed è lo stesso con cui voglio essere ricordato (vedi [[Identità]]).

**Cosa non tollero.** Il collaboratore che dichiara "alla data X farò Y" e alla data X:
- non dà update, oppure
- inventa scuse per il mancato lavoro, oppure
- peggio, se ne frega del commitment preso.

**Perché è grosso.** Un commitment non preso o non onorato è una forma di presa in giro relazionale. È la stessa radice del fastidio con la vaghezza deliberata: rompe il contratto implicito di trattarsi da adulti.

## Produttività

**Definizione.** **Produttività = Velocità × Efficacia.** Moltiplicativo, non additivo. È il risultato degli altri valori, non un valore indipendente — ma va dichiarato perché è la metrica sintetica con cui giudico il lavoro mio e altrui.

**Conseguenza pratica.** Non ha senso ottimizzare la velocità senza aver prima presidiato l'efficacia. E l'efficacia senza velocità resta potenziale inespresso.

## Regole operative quotidiane

Due abitudini concrete in cui questi valori si traducono ogni giorno.

### 1. Time-blocking fino alla microattività

Organizzo nel calendario anche le microattività della giornata per non perderle. Se non riesco a completarle entro la giornata, le **ripianifico entro fine giornata** — al più lontano entro la settimana corrente. Mai lasciarle fluttuare senza slot.

**Valori serviti.** Affidabilità (il commitment con me stesso vale quanto quello con gli altri), produttività (niente attività persa in testa).

### 2. Chiarificazione totale del contesto prima di agire

Prima di mettere mano a un'attività che produce output decisionale o operativo, devo capire al 100% il contesto in cui mi inserisco. **Non si modifica un processo che non si è prima capito.**

**Valori serviti.** Efficacia (colpire il bersaglio giusto richiede aver capito quale sia), precisione (dichiarare commitment sensati richiede conoscere il terreno).

## Collegamenti

- [[Identità]] — "affidabile" è parte di come voglio essere ricordato
- [[Strategia-Attuale]] — i valori filtrano le scelte strategiche
- [[OKR-Correnti]] — la produttività come metrica del lavoro operativo
- [[Crescita-Priorità-Correnti]] — dove questi valori vengono messi alla prova oggi
