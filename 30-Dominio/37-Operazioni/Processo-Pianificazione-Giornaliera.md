---
tipo: processo
creato: 2026-04-14
aggiornato: 2026-04-25
stato: attivo
tags:
  - processo/pianificazione
  - operazioni
  - produttività
  - pillar/leadership-strategica
area: operazioni
---

# Pianificazione Giornaliera

> [!info] In una frase
> Sistema operativo personale che converte MIT della sera, calendario lavorativo e microattività in **time-block giornaliero scritto** dentro `10-Diario/Giornaliero/YYYY-MM-DD.md`, garantendo che le attività non urgenti-ma-importanti non cadano fuori dal radar.

## Forma canonica

| Campo | Valore |
|---|---|
| **Input** | (1) Essential intent serale + MIT massimo 3, (2) calendario lavorativo Angelini, (3) capture aperto da Inbox / `Da-processare`, (4) microattività ripianificate dalla giornata precedente, (5) attività future da non perdere ([[Scadenziere]]) |
| **Output** | Nota `10-Diario/Giornaliero/YYYY-MM-DD.md` con time-block esplicito, MIT prioritizzati, buffer reattivo dichiarato, check di fine giornata vuoto da compilare la sera |
| **Processo** | Skill [[Strumenti-Claude-Code\|Claude Code]] `/daily` con due flussi — A (sera prima: pianifica domani) e B (giornata in corso: riflessione mattutina + check serale) |
| **Owner operativo** | Founder. Slot serale ~22:00 dal divano via Obsidian iOS (Flusso A); skill `/daily` da Claude Code mattina e sera (Flusso B) |
| **Agganci pillar** | **P1 primario** ([[Strategia-Pillar-Leadership-Strategica]]), **S su [[Crescita-Pillar-Studio-Giuridico\|P5]]** (presidia lo slot studio giuridico non negoziabile), **S su [[Prodotto-Pillar-Delivery-Piloti\|P2]]** (alloca gli slot serali a AIOS/FT senza dispersione) |

## Origine

Sistema nato il **2026-04-14** dall'intervista [[Processo-Pianificazione-Giornaliera|v1→v2]] (sezione storica sotto) che ha mostrato il fallimento del sistema-a-memoria precedente (3 miss critici emersi solo su sollecitazione: padre per AIOS, framework Claude Code, debug FT). [[Decisione-Sistema-Pianificazione-Giornaliera]] del 2026-04-14 ha scelto **Obsidian Sync + Obsidian iOS + template `Pianificazione-Giornaliera`** (Templater) come implementazione operativa.

In attivo dal 2026-04-14. Prima review programmata 2026-04-28 (criteri di conferma in [[Decisione-Sistema-Pianificazione-Giornaliera#Verifica e revisione]]).

## Loss servita

> [!info] Loss primaria — #1 Finestra-competitiva-persa
> Il rischio endogeno #1 dichiarato in [[Strategia-Attuale#Rischi strategici]] è la dispersione su quattro filoni mentre un competitor più veloce occupa lo spazio. Il meccanismo concreto di erosione non è la velocità tecnica — è **l'attività importante che non entra mai in uno slot** perché non ha urgenza. Pianificazione Giornaliera è il sistema che chiude questo buco trasformando ogni MIT e microattività in time-block scritto.

Loss secondarie servite via agganci S:

- **#3 Identità-consulente-del-lavoro-non-costruita** (P5): senza slot scritto, lo studio giuridico salta nelle settimane critiche AIOS — proprio il rischio dichiarato nel [[OKR-Correnti#Pre-mortem (rischi identificati)|pre-mortem Q2]].
- **#8 Maturità-piloti-non-in-tempo** (P2): senza time-block, gli slot serali si sciolgono in scroll/inerzia invece che in lavoro su AIOS/FT.

## Il flusso a due tempi

### Flusso A — Sera prima (pianificazione di domani)

Trigger: founder dice *"pianifichiamo la giornata"* o *"pianifichiamo domani"* dal divano alle ~22:00 su Obsidian iOS.

Output: nota `10-Diario/Giornaliero/YYYY-MM-DD.md` (data di domani) compilata via template `_Sistema/Templates/Pianificazione-Giornaliera.md` (Templater).

Sezioni obbligatorie del template (confermate dall'uso reale dal 2026-04-14):
1. **Shutdown di oggi** — MIT chiusi/aperti, Inbox svuotato, microattività ripianificate.
2. **Essential intent di domani** — una frase, formato McKeown.
3. **MIT max 3** — tabella con filone + energy required.
4. **Time-block della giornata** — fasce mattina/pomeriggio/sera.
5. **Buffer reattivo esplicito** — cosa comprimere se MIT lungo.
6. **Capture aperto** — microattività + attività future da non perdere.
7. **Check di fine giornata** — checkbox da compilare la sera dopo, non al momento.

### Flusso B — Giornata in corso

Due ingaggi durante il giorno via skill `/daily` da Claude Code:
- **Mattina** — riflessione mattutina, conferma MIT, eventuale aggiustamento.
- **Sera** — check di fine giornata: essential intent realizzato? MIT chiusi? Cause di scivolamento? Microattività non chiuse → ripianificate.

> [!warning] Regola non negoziabile
> La microattività che non chiude oggi viene **ripianificata entro fine giornata**, al più lontano entro la settimana corrente. Mai lasciata fluttuare senza slot. Coerente con [[Valori-Fondamentali#1. Time-blocking fino alla microattività|regola operativa quotidiana #1]].

## Anti-pattern da evitare

- **Pianificare la mattina** invece della sera prima — il vincolo "pianifico in ufficio" era imposto dalla disponibilità del calendario lavorativo, ma AIOS/FT/studio giuridico vivono dopo il lavoro. Pianificarli la mattina = pianificare qualcosa che inizia 10h dopo, con la testa ancora sul giorno in corso.
- **Solo 3 MIT come "lista cose da fare"** senza time-block — togliere il MIT dallo slot orario riapre il sistema-a-memoria.
- **Microattività in testa** invece che in `Capture aperto` — la regola implicita *"se costo di scrittura > probabilità percepita di dimenticare, tengo a memoria"* ha probabilità mal calibrata e fa cadere l'importante non urgente.
- **Saltare il check serale** — senza il check di fine giornata, la causa di scivolamento (energia? interruzione? sotto-stimato? ambiguità?) non viene mai diagnosticata e il pattern si ripete.
- **Pianificare il weekend come i feriali** — il weekend ha vincoli diversi (debug FT, studio giuridico, recupero), non vale lo stesso template senza adattamento.

## Health check del sistema

Coerente con [[Sistemi-Sotto-Pillar]], il sistema è "sano" se:

- ✅ **Compilazione** — nota di pianificazione compilata ≥10 sere su 14 (criterio review 2026-04-28).
- ✅ **Aderenza** — almeno un miss del sistema vecchio evitato e attribuibile al nuovo sistema.
- ✅ **Sensazione soggettiva** — "mente meno satura" alla fine della giornata.
- ✅ **No carry-over silenzioso** — microattività non chiuse SEMPRE ripianificate (zero fluttuanti tra sessioni).

Review periodica: in [[Processo-Review-Cadence]] settimanale (dentro `/weekly`), verificare se le 3 spunte sono ✓ nella settimana chiusa.

## Storia v1 → v2 (sezione storica)

Il sistema attuale (v2) ha sostituito una v1 ingegnerizzata su memoria + calendario lavorativo + promemoria iPhone solo per urgenze. La v1 falliva perché la regola implicita *"se costo di scriverlo supera la probabilità percepita di dimenticarlo, lo tengo a memoria"* aveva la probabilità calibrata male: attività non urgenti oggi ma importanti domani cadevano fuori dal radar.

> [!failure] Caso concreto v1 — plugin esame università
> Conosciuta la necessità ~20 giorni prima dell'esame del 2026-04-17. Non scritta in calendario perché non urgente. Riemersa solo il 2026-04-13, senza tempo sufficiente per testare il funzionamento.

Altri tre miss emersi nell'intervista del 2026-04-14, tutti né in calendario né in promemoria:
1. Coinvolgere il padre per costruire il vault dello studio — blocker AIOS go-live 2026-05-10.
2. Importare framework globale Claude Code nel vault per memoria persistente cross-progetto.
3. Debug Football Trading previsto per la sera dell'intervista.

Non dettagli: un blocker strategico, un'architettura di sistema, un debug imminente. Il fatto che siano usciti solo su sollecitazione ha dimostrato che la v1 stava perdendo cose importanti, non solo microattività. Da qui [[Decisione-Sistema-Pianificazione-Giornaliera]].

## Implementazione come Skill Claude Code

Skill globale `~/.claude/skills/daily/SKILL.md` con due flussi:
- **Flusso A** — trigger *"pianifichiamo la giornata"* / *"pianifichiamo domani"* → applica template Pianificazione-Giornaliera nella nota di `10-Diario/Giornaliero/`.
- **Flusso B** — trigger *"apri il diario di oggi"* / *"chiudo la giornata"* → riflessione mattutina + check serale.

Doppio canale di trigger:
- **Da Claude Code** (desktop, WSL): skill `/daily`.
- **Da Obsidian iOS** (mobile, divano): Templater Folder Templates su `10-Diario/Giornaliero/` applica il template all'apertura/creazione della nota.

## Collegamenti

- [[Decisione-Sistema-Pianificazione-Giornaliera]] — scelta tool e architettura (2026-04-14)
- [[Strategia-Mappa-Pillar-Sistemi]] — aggancio P1 primario, S su P5 e P2
- [[Sistemi-Sotto-Pillar]] — forma canonica del sistema
- [[Strategia-Pillar-Leadership-Strategica]] — pillar primario, loss #1
- [[Crescita-Pillar-Studio-Giuridico]] — pillar consumer (slot studio giuridico)
- [[Prodotto-Pillar-Delivery-Piloti]] — pillar consumer (slot AIOS/FT)
- [[Processo-Review-Cadence]] — review settimanale del health check
- [[Valori-Fondamentali#1. Time-blocking fino alla microattività]] — radice nei valori
- [[Valori-Fondamentali#Affidabilità / Commitment]] — il commitment con sé stessi vale quanto quello con gli altri
- [[OKR-Correnti]] — Objective 3 protetto da questo sistema
- [[Crescita-Priorità-Correnti]] — guardrail anti-dispersione operato dal time-block
- [[Dashboard]]
