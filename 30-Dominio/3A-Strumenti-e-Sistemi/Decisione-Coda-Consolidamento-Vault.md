---
tipo: decisione
creato: 2026-04-13
aggiornato: 2026-04-13
stato: attivo
tags:
  - decisione/architettura
  - strumenti/ai
  - processo/vault
area: strumenti
---

# Decisione — Pattern "coda + consolidamento a cadenza" come meccanismo di riempimento dei vault-prodotto

## La decisione

Adottare come **principio architetturale** dei vault dedicati a soluzioni AI il pattern **raccolta continua in coda + consolidamento a trigger temporale**:

- durante l'uso quotidiano l'AI **non modifica** il vault in modo diretto: accumula insight e correzioni in una **coda**
- a cadenza prefissata, un **trigger** apre una finestra di consolidamento che processa la coda e aggiorna le note
- la **cadenza del trigger è funzione del ritmo di cambiamento del dominio**, non una costante

## Perché

Tre ragioni, in ordine di peso:

1. **Separare scrittura da esecuzione protegge l'integrità del vault.** Se l'AI scrivesse in diretta, ogni errore durante l'uso contaminerebbe la base di conoscenza. La coda è un buffer che permette revisione umana prima che il vault cambi.
2. **Retrofeedback senza rituale muore.** Una review periodica completa è costosa e si salta; la raccolta continua senza consolidamento produce una coda che cresce senza mai diventare conoscenza. Il pattern tiene entrambe le gambe.
3. **Allineamento al [[Valori-Fondamentali|valore di efficacia]].** Consolidare a cadenza calibrata sul dominio è colpire il bersaglio giusto nel momento giusto, non ottimizzare la frequenza in astratto.

## Alternative considerate

| Opzione | Perché scartata |
|---|---|
| Scrittura diretta dell'AI sul vault | Rischio di contaminazione senza gate di revisione. Nessun buffer contro errori in diretta. |
| Review periodica completa senza coda | Si perde ciò che emerge nel mezzo. La memoria umana non regge tra due review. |
| Coda senza trigger (consolidamento "quando capita") | In pratica non capita mai. Senza rituale il debito si accumula. |
| Cadenza unica per tutti i prodotti | Mismatch tra ritmo del dominio e ritmo di aggiornamento. Troppo frequente spreca tempo; troppo rara rende il vault stantio. |

## Parametri per soluzione

| Soluzione | Cadenza consolidamento | Driver |
|---|---|---|
| [[Sistema-Agentico-Studio]] (AIOS) | **Mensile+** | Dominio fiscale/documentale cambia lento |
| [[Football-Trading]] | **Settimanale** | Pattern/strategie di mercato cambiano veloce |

## Reversibilità e blast radius

- **Reversibilità**: alta. È un pattern architetturale, si può sostituire con un altro se si dimostra inefficace senza perdere contenuto (la coda e il vault restano).
- **Blast radius**: alto verso l'alto — vincola l'impianto dei due piloti e dei futuri vault-prodotto. È la ragione per cui va registrato come decisione, non solo come nota di processo.

## Implicazioni operative

- Il passo 2 del [[Processo-Costruzione-Vault-dedicato]] (aggancio AI) deve includere nelle regole **il comportamento "accoda, non scrivere"**.
- Serve definire il **formato concreto della coda** (file, struttura, campi) — oggi non specificato. Domanda aperta.
- Serve un **meccanismo di trigger** (manuale? skill dedicata? cron?) — oggi non specificato. Domanda aperta.

## Criterio di revisione

Rivedere questa decisione se:

- dopo 2 cicli di consolidamento consecutivi la **coda risulta sistematicamente vuota** (segnale: l'AI non sta segnalando → il meccanismo non funziona), oppure
- il **costo del consolidamento** supera il valore prodotto (segnale: cadenza troppo frequente o coda troppo rumorosa).

## Collegamenti

- [[Processo-Costruzione-Vault-dedicato]] — il processo di cui questa decisione è principio architetturale
- [[Prodotto-Vault-Substrato-Di-Prodotto]] — la cornice concettuale
- [[Sistema-Agentico-Studio]] · [[Football-Trading]] — i due casi di applicazione
- [[Valori-Fondamentali]] — efficacia come filtro della cadenza
