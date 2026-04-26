---
tipo: decisione
creato: 2026-04-14
aggiornato: 2026-04-14
stato: attivo
tags:
  - decisione/sistemi
  - decisione/produttività
  - operazioni
area: strumenti
---

# Decisione — Sistema di pianificazione giornaliera (Obsidian Sync + template Pianificazione-Giornaliera)

> [!info] In una frase
> Adottare **Obsidian Sync (1 mese di prova) + Obsidian iOS + template `Pianificazione-Giornaliera` con Templater**, compilato la sera prima dal divano sul telefono, come sistema di pianificazione che sostituisce il "tutto a memoria" attuale.

## Contesto

L'intervista del 2026-04-14 sul [[Processo-Pianificazione-Giornaliera]] ha mostrato che il sistema attuale (calendario lavorativo + memoria + promemoria iPhone solo per urgenze) **non regge il carico**: tre item critici — coinvolgere il padre per AIOS, importare framework Claude Code nel vault, debug Football Trading — emersi solo su sollecitazione, nessuno schedulato. La regola implicita *"se costo di scrittura > probabilità percepita di dimenticare, tengo in testa"* ha probabilità mal calibrata e fa cadere attività non urgenti-ma-importanti.

## Decisione presa

Adottare un sistema con tre componenti:

1. **Obsidian iOS** sul telefono come interfaccia serale dal divano.
2. **Obsidian Sync** (~8€/mese, 1 mese di prova) come metodo di sincronizzazione vault WSL ↔ iPhone.
3. **Template `_Sistema/Templates/Pianificazione-Giornaliera.md`** con Templater (community plugin), basato su best practice consolidate (Newport, Covey, McKeown, Pink). Compilato la sera prima per la giornata di domani. Nota generata in `10-Diario/Giornaliero/YYYY-MM-DD.md`.

Trigger automatizzato lato Claude Code via skill aggiornata `daily` (Flusso A su *"pianifichiamo la giornata"*). Trigger lato Obsidian iOS via Templater Folder Templates su `10-Diario/Giornaliero/`.

## Alternative considerate

| Opzione | Pro | Contro | Esito |
|---|---|---|---|
| **Restare al sistema attuale** (memoria + calendario lavorativo) | Zero costo, zero attrito setup | Dimostrato non regge il carico (3 miss critici emersi nell'intervista) | Scartata |
| **Promemoria iPhone con soglia urgenza più bassa** | Gratis, già installato | Crea sistema parallelo a calendario, frammentazione, no time-blocking | Scartata |
| **Time-blocking esteso su Outlook aziendale** | Tool già usato | Legato a tool aziendale che si perderà nella transizione a consulente | Scartata |
| **Vault solo PC + copia-incolla manuale dal telefono** | Gratis | Azione manuale = trappola identica a quella attuale ("non urgente → cade") | Scartata |
| **Git + Working Copy su iPhone** | Gratis, cronologia versioni | Setup di un'oretta + commit/push da gestire ad ogni sessione = attrito ricorrente | Scartata |
| **Obsidian Sync 1 mese di prova** | Zero attrito, source of truth nel vault, reversibile | Costo ricorrente (~8€/mese) se confermato | **Scelta** |

## Rationale

Tre criteri hanno guidato la scelta:

1. **Niente azioni manuali**. Il principio emerso esplicitamente nell'intervista: *"ciò che mi crea attrito è fare azioni manuali"*. Ha eliminato copia-incolla e Git con commit/push manuali.
2. **Source of truth nel vault**. Coerente con principio del vault e con l'architettura v2 immaginata in [[Processo-Pianificazione-Giornaliera]]. Esclude tool legati ad Angelini (Outlook) destinati a sparire nella transizione.
3. **Decisione reversibile a basso costo**. 8€ per un mese di prova è trascurabile rispetto al costo dei miss attuali (es. coinvolgere padre = blocker AIOS go-live 10 maggio).

## Ipotesi sotto la decisione

- L'utente aprirà davvero Obsidian iOS dal divano la sera (verificabile in 2 settimane).
- Il template basato su Newport/Covey/McKeown/Pink è proporzionato al carico — non troppo pesante per essere compilato ogni sera, non troppo leggero per essere utile.
- Obsidian Sync non introdurrà conflitti significativi tra modifiche desktop e mobile.

## Verifica e revisione

- **Data review**: 2026-04-28 (2 settimane). Tracciata in Da-processare item #3.
- **Criteri di conferma**:
	- Nota di pianificazione compilata ≥10 sere su 14.
	- Almeno un miss del sistema vecchio evitato e attribuibile al nuovo sistema.
	- Sensazione soggettiva di "mente meno satura" alla fine della giornata.
- **Esiti possibili**:
	- ✅ Confermo Obsidian Sync e template.
	- 🔄 Confermo Obsidian Sync, alleggerisco/modifico il template.
	- ❌ Disdico Obsidian Sync, valuto se il problema è il sistema o l'abitudine.

## Output operativi prodotti in questa sessione

- [[Processo-Pianificazione-Giornaliera]] — nota di processo (v1 attuale, v2 target).
- `_Sistema/Templates/Pianificazione-Giornaliera.md` — template con sintassi Templater.
- `.claude/skills/daily/SKILL.md` — skill aggiornata con Flusso A (pianificazione di domani) e Flusso B (gestione nota di oggi).
- Da-processare — capture inbox dei follow-up.

## Collegamenti

- [[Processo-Pianificazione-Giornaliera]]
- [[Valori-Fondamentali]] — affidabilità, time-blocking
- [[Identità]] — transizione fuori dalla cornice corporate (motiva il vincolo "no tool aziendali")
- [[OKR-Correnti]] — pianificazione protegge Objective 3 (fondamenta della transizione)
- Da-processare
