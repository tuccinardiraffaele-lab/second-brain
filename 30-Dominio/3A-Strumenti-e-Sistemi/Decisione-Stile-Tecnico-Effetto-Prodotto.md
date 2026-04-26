---
tipo: decisione
creato: 2026-04-15
aggiornato: 2026-04-15
stato: attivo
tags:
  - strumenti/claude-code
  - stile-comunicazione
  - decisione/stile
area: strumenti
---

# Decisione — Traduci sempre il tecnico in effetto sul prodotto

> [!info] In una frase
> Quando Claude parla di codice, funzioni o componenti tecnici, deve **tradurre in effetto sull'utilizzatore finale del prodotto**. Forma canonica: *"se modifico X, il prodotto passa dal comportamento A al comportamento B"* — dove A e B sono ciò che vede o fa l'utente, non ciò che fa il codice.

## Contesto

Il founder è in **apprendimento su molti framework e tooling** (vedi [[Identità]] — "in apprendimento" esplicito nel profilo). Una spiegazione puramente tecnica (es. *"ho implementato una chiamata API al modello Anthropic per fare leva sull'LLM"*) è **precisa ma oscura**: il founder non riesce a giudicare se la modifica sta andando nella direzione giusta finché non la traduce mentalmente in effetto osservabile. La traduzione mancante è un collo di bottiglia.

La tesi imprenditoriale del founder è portare AI nelle piccole realtà dal punto di vista dell'utilizzatore finale (studi commercialisti, consulenti del lavoro, trader retail) — ogni decisione tecnica ha senso solo se quell'utente ne riceve un effetto concreto. Parlare di codice senza tradurlo in effetto sul prodotto è un'abitudine che toglie allineamento.

Questo principio risuona con [[Valori-Fondamentali#Chiarezza|Chiarezza]] nei valori fondamentali: *"calibrare il messaggio sull'interlocutore… esempi concreti come ponte"*.

## Decisione

Regola operativa integrata nel **sotto-blocco "Traduci sempre il tecnico in effetto sul prodotto"** dentro la sezione 5 del CLAUDE.md globale:

Quando Claude parla di codice, funzioni, componenti tecnici, **traduce in effetto sull'utilizzatore finale**. Forma canonica:

> *"Se modifico X in questo modo, il prodotto passa dal comportamento A al comportamento B."*

Dove **A e B sono ciò che vede o fa l'utente**, non ciò che fa il codice. Vale identicamente in implementazione e in debugging: ogni volta che si propone un cambio o si diagnostica un bug, si chiude il ragionamento mettendosi nei panni dell'utilizzatore finale (funzionalità, usabilità, comportamento osservabile).

**Fallback**: se Claude non riesce a tradurre → significa che non ha ancora capito a cosa serve il pezzo di codice → deve fermarsi e chiedere.

## Alternative valutate e scartate

- **Spiegazione tecnica pura**: più veloce per Claude, ma lascia il founder a metà strada. Rompe il principio di chiarezza.
- **Doppia spiegazione (tecnica + business in appendice)**: verboso, spezza il flusso della risposta. La traduzione deve essere **integrata**, non annessa.
- **Solo in spiegazioni, non in debugging**: scartata. Il debugging è dove il POV utente è più critico — capire cosa l'utente vede andare storto è il primo passo per trovare la root cause.

## Conseguenze

**Positive:**
- Il founder può giudicare velocemente se una modifica va nella direzione giusta senza tradurre mentalmente dal tech.
- Claude è forzato a **capire davvero** a cosa serve il codice prima di modificarlo — se non riesce a tradurre in effetto-utente, c'è un gap di comprensione da chiudere.
- Allineamento con la tesi imprenditoriale del founder (AI che serve l'utilizzatore finale).

**Negative / rischi:**
- Rischio di over-translation su modifiche puramente interne (refactor senza impatto utente). Da gestire: in quei casi la traduzione canonica degenera in *"nessun comportamento osservabile cambia, è una ristrutturazione interna che rende X più facile da modificare in futuro"* — accettabile.

## Come si misura se funziona

Al founder: dopo ogni sessione di coding con Claude, riesce a **ripetere a un non-tecnico** cosa è cambiato nel prodotto? Se sì, la regola sta funzionando. Se no, la traduzione non c'è stata o non era nel mirino.

## Collegamenti

- [[Valori-Fondamentali]] — in particolare Chiarezza (calibrare messaggio sull'interlocutore)
- [[Identità]] — profilo "in apprendimento" + tesi imprenditoriale (AI per utilizzatore finale)
- [[Brain-Framework-Implementazione]] — decisione integrata nella sezione 5 del CLAUDE.md globale durante Step C
