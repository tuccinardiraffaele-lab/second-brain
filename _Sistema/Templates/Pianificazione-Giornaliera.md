---
tipo: diario
creato: <% tp.date.now("YYYY-MM-DD") %>
aggiornato: <% tp.date.now("YYYY-MM-DD") %>
stato: attivo
tags:
  - pianificazione
  - diario/giornaliero
area: operazioni
data-pianificata: <% tp.file.title %>
---

# Pianificazione — <% tp.file.title %>

> [!info] Compilato la sera del <% moment(tp.file.title).subtract(1, 'day').format("YYYY-MM-DD") %>
> Template basato su Newport (time-blocking + shutdown), Covey (MIT), McKeown (essential intent), Pink (energy mapping). Vedi [[Processo-Pianificazione-Giornaliera]].

## 1. Shutdown di oggi (<% moment(tp.file.title).subtract(1, 'day').format("YYYY-MM-DD") %>)

> [!example] Chiusura della giornata appena conclusa
> Compilare prima di passare alla pianificazione di domani. Senza shutdown, il cervello continua a girare e la sera viene erosa.

- **MIT chiusi**:
- **MIT aperti / non finiti** (e perché):
- **Inbox svuotato** (mail, promemoria, idee → catturate nel sistema): [ ]
- **Microattività ripianificate** (spostate a giorni successivi):

## 2. Essential intent di domani

> [!tip] Una sola frase
> *"Se domani faccio solo questa cosa, la giornata è vinta."* — McKeown

**Intent**:

## 3. MIT — Most Important Tasks (max 3)

> [!warning] Massimo 3
> Più di 3 = nessuno. Ogni MIT collegato al filone strategico di riferimento ([[OKR-Correnti]]).

| # | MIT | Filone | Energy required |
|---|-----|--------|-----------------|
| 1 |  |  | alta / media / bassa |
| 2 |  |  |  |
| 3 |  |  |  |

## 4. Time-block della giornata

> [!note] Allocare ogni minuto, sapendo che il piano va rivisto in corsa
> Il piano è un'ipotesi, non un contratto. Il valore non è la rigidità — è aver pensato la giornata prima che inizi.

### Mattina — Corporate (Angelini)
- 09:00 –
- 11:00 –
- 13:00 — pranzo

### Pomeriggio — Corporate
- 14:00 –
- 17:00 — uscita / transizione

### Sera — Lavoro proprio
- 18:00 –
- 20:00 –
- 22:00 — buffer / chiusura

### Buffer reattivo esplicito
Slot dichiarato per imprevisti (default: 30-45 min nel pomeriggio):

## 5. Capture aperto

> [!question] Input da non perdere
> Idee, dubbi, cose emerse oggi che non vanno fatte domani ma non devono cadere. Vanno processate nella weekly review o ripianificate quando hanno una collocazione.

-

### Attività future da non perdere (non domani, ma da tracciare)

> [!note] Impegni con data o deadline oltre domani
> Attività, call, scadenze o milestone che non entrano nei MIT di domani ma non devono cadere dal radar. Ogni voce: data/finestra + oggetto + link al KR/progetto se applicabile.

-

## 6. Check di fine giornata di domani (<% tp.file.title %> sera)

> [!todo] Da compilare domani sera, non ora
> - [ ] Essential intent realizzato?
> - [ ] MIT 1 / MIT 2 / MIT 3 — chiusi?
> - [ ] Se MIT non chiuso → causa (energia? interruzione? sotto-stimato? ambiguità?)
> - [ ] Microattività non chiuse → ripianificate (mai lasciarle fluttuare, vedi [[Valori-Fondamentali#Affidabilità / Commitment|Affidabilità]])
> - [ ] Domani sera ripeti dallo step 1.

## Collegamenti

- [[Processo-Pianificazione-Giornaliera]] — il processo che questo template implementa
- [[Valori-Fondamentali]] — time-blocking e affidabilità (regole operative quotidiane)
- [[OKR-Correnti]] — riferimento per filone dei MIT
- [[Dashboard]] — vista d'insieme settimanale
