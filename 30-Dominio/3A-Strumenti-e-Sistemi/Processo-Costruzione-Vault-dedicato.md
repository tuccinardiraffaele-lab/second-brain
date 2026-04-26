---
tipo: processo
creato: 2026-04-13
aggiornato: 2026-04-13
stato: attivo
tags:
  - processo/vault
  - strumenti/ai
area: strumenti
---

# Processo — Costruzione di un vault dedicato a una soluzione

> [!info] In una frase
> Meta-processo a 3 passi (**struttura → aggancio AI → riempimento**) per costruire un vault Obsidian-based che funga da substrato di prodotto per una soluzione AI specifica. La forma concreta di ciascun passo cambia in funzione di **rischio tollerato** e **scopo dell'AI nel prodotto**.

## Perché è il processo a più alta leva

È il processo che **libera e potenzia tutti gli altri**. Una volta costruito bene il vault dedicato, la soluzione AI che ci gira sopra eredita automaticamente: base di conoscenza navigabile, regole di orientamento, meccanismo di aggiornamento. Vale per [[Sistema-Agentico-Studio]] e, con modalità diversa, anche per [[Football-Trading]].

Estende [[Prodotto-Vault-Substrato-Di-Prodotto]]: quella nota dice *cosa* è il vault-prodotto; questa dice *come* lo si costruisce.

## I tre passi

### Passo 1 — Struttura di cartelle

Scheletro vuoto del vault. Si parte **sempre da una struttura standard** (tipo PARA/MECE come nel [[Dashboard|second brain personale]]) e si **customizza sul dominio del prodotto**.

La customizzazione dipende da **due diagnostiche sull'utente finale**:

| Diagnostica | Domanda | Effetto sulla struttura |
|---|---|---|
| Rischio tollerato | Quanto costa una decisione sbagliata dell'AI? | Rischio zero → struttura che supporta dialogo e chiarificazione. Rischio accettato → struttura che separa autoritativo da sperimentale |
| Costo dell'interazione online | Quanto erode valore fermare l'AI per chiedere all'utente? | Costo basso → modalità dialogica. Costo alto (es. tempestività in live trading) → modalità pre-computata |

Le due diagnostiche generano **due modalità di vault** (vedi sezione dedicata).

### Passo 2 — Aggancio dell'AI con regole di orientamento

Collegamento dell'API del modello (es. [[Anthropic]]) con un set di regole — l'equivalente del `CLAUDE.md` di questo vault — che dicono all'AI:

- **qual è la base di conoscenza** (il vault)
- **come navigarla**
- **quando agire in autonomia e quando no**

La **natura delle regole cambia con lo scopo dell'AI nel prodotto**, non con la modalità in sé:

- Se l'AI è *knowledge base + validator + generatore di suggerimenti* → regole su navigazione, validazione, invito alla chiarificazione in caso di incertezza.
- Se l'AI è *scopritore di insight + costruttore e validatore offline, con gate di approvazione umana prima del live* → regole su cosa è autoritativo (validato, usabile), cosa è sperimentale (in studio), e come comportarsi al gate di approvazione.

### Passo 3 — Riempimento del vault

Due meccanismi complementari, **entrambi presenti sempre**, con ruoli distinti nel tempo:

- **Interview** — estrazione *proattiva* di conoscenza implicita. Si fanno domande all'utente, si struttura la risposta nel vault. Serve a **bootstrappare** il vault quando la conoscenza esiste solo nella testa dell'utente.
- **Retrofeedback** — raffinamento *reattivo*. L'AI usa il vault, produce output, l'utente corregge; la correzione rientra come regola/nota aggiornata. Serve a **mantenere e affinare** il vault con la conoscenza che emerge dall'uso.

**Pattern operativo: raccolta continua + consolidamento a cadenza.** Durante l'uso quotidiano l'AI segnala insight e correzioni accumulandoli in una **coda**. Al trigger temporale si **processa la coda**.

**La cadenza del trigger è guidata dal ritmo di cambiamento del dominio**, non da una regola generale.

## Le due modalità di vault

> [!tip] Discriminante
> **Rischio tollerato dall'utente finale** + **costo dell'interazione online**. La modalità non è scelta estetica: deriva dal prodotto.

### Vault dialogico
- L'AI può fermarsi e **chiedere chiarimento all'utente** durante l'uso.
- Adatto a prodotti dove il rischio di errore è inaccettabile e l'interazione non erode valore.
- Esempio: [[Sistema-Agentico-Studio]] (decisioni documentali → rischio zero tollerato → dialogo come mitigazione).

### Vault pre-computato
- Il dialogo avviene **offline** (scoperta pattern, sperimentazione, validazione); l'esecuzione online attinge a quanto già cristallizzato.
- Gate di approvazione umana **al confine offline→online**, non durante l'esecuzione live.
- Adatto a prodotti con rischio intrinseco accettato dall'utente e tempestività di azione come fonte di valore.
- Esempio: [[Football-Trading]] (live trading → interazione online erode efficienza → erode monetizzazione).

## Applicazione ai casi vivi

### [[Sistema-Agentico-Studio]] (AIOS)

| Passo | Forma concreta |
|---|---|
| 1 — Struttura | Base di conoscenza navigabile. Rischio zero, interazione online ammessa |
| 2 — Regole AI | "Naviga il vault, valida documenti, suggerisci al commercialista, **chiedi in caso di incertezza**" |
| 3 — Riempimento | Interview col padre per bootstrap della knowledge base + retrofeedback continuo. Trigger consolidamento coda: **mensile** (dominio fiscale/documentale cambia lento) |

### [[Football-Trading]]

| Passo | Forma concreta |
|---|---|
| 1 — Struttura | Separazione netta tra pattern/strategie *autoritative* (validate offline, usabili in live) e *sperimentali* (in studio). Nessuna interazione online |
| 2 — Regole AI | "Scopri insight, costruisci e valida offline, presenta all'utente per approvazione al gate, poi usa solo l'autoritativo in live" |
| 3 — Riempimento | Interview per bootstrap del framework iniziale + retrofeedback dagli esiti del paper/live trading. Trigger consolidamento coda: **settimanale** (mercato cambia veloce) |

## Cosa questo processo abilita

- **Riutilizzo del framework** su future soluzioni (non è un one-off per AIOS).
- **Coerenza architetturale** tra prodotti diversi: la struttura del vault diventa la firma del metodo.
- **Scalabilità del B2B**: quando si venderà AIOS ad altri studi, ogni onboarding sarà un'istanza di questo processo, non una reinvenzione.

## Domande aperte

> [!question] Da chiarire nelle prossime iterazioni
> - Qual è il **meccanismo concreto di segnalazione** che l'AI usa per accodare insight/correzioni durante l'uso? (skill? hook? log strutturato?)
> - Come si versiona la separazione **autoritativo vs sperimentale** nel vault Football Trading senza introdurre attrito operativo?
> - Esiste una **struttura-template di cartelle** riutilizzabile tra soluzioni, o ogni dominio la ridisegna quasi da zero?

## Collegamenti

- [[Prodotto-Vault-Substrato-Di-Prodotto]] — il *cosa* (questa nota è il *come*)
- [[Sistema-Agentico-Studio]] — applicazione modalità dialogica
- [[Football-Trading]] — applicazione modalità pre-computata
- [[Strategia-Attuale]] — i due piloti che vivono questo processo
- [[Strumenti-Dashboard-Auto-Generata-Via-Bases]] — esempio di come il second brain personale applica il processo a se stesso
