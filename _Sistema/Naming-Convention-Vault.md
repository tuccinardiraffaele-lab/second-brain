---
tipo: processo
creato: 2026-04-16
aggiornato: 2026-04-16
stato: attivo
tags:
  - operazioni/vault
  - processo/naming
area: operazioni
---

# Naming Convention — Vault

> [!info] In una frase
> Regola unica per nominare i file `.md` del vault in modo che siano auto-localizzabili, greppabili e MECE — senza che il titolo dipenda dal percorso cartella.

## Regola base

- **Formato**: `Kebab-Case-Iniziale-Maiuscola.md` — ogni parola inizia maiuscola, separate da `-`.
- **Nessuno spazio** nei filename né nelle cartelle create da oggi. Accenti italiani ammessi (`Identità`, `Relazioni`).
- **UTF-8 senza BOM**. Nessun emoji nei filename (le cartelle decorative tipo `🔥-Attive/` restano come sono).
- **Date nei nomi**: sempre `YYYY-MM-DD`.

## Pattern per dominio (`30-Dominio/*`)

**Default — dominio-prefix** (Pattern A):

```
<Dominio>-<Sottodominio>-<Dettaglio>.md
```

Esempi attivi: `Finanza-Business-Capitale-Iniziale`, `Vendite-Caso-Cinofilia`, `Finanza-Professionale-Piano-Accademico`.

**MOC di sottodominio**: suffisso `-MOC` → `Finanza-MOC.md`, `Vendite-MOC.md`.

## Tipi canonici cross-dominio (Pattern B, eccezione)

Solo quattro prefissi di tipo sopravvivono al dominio-prefix, perché la nota si legge per *tipo* e non per *area*:

| Prefisso | Uso |
|---|---|
| `Decisione-` | Decisioni registrate via `/decision` |
| `Processo-` | SOP operative ripetibili |
| `Pattern-` | Pattern osservati ricorrenti (business, relazionali, tecnici) |
| `Troubleshooting-` | Playbook diagnostici |

Tutto il resto in `30-Dominio/*` segue Pattern A.

## KR

Formato a sé (è un indice numerato, non un nome-nota):

```
KR<obj>.<kr> — <Descrizione sintetica>.md
```

Esempio: `KR1.2 — Metriche pilot fissate con padre.md`. L'em-dash ` — ` è voluto per l'ordinamento visivo.

## Iniziative (`20-Iniziative/**`)

- **MOC progetto**: nome del progetto come filename → `Sistema-Agentico-Studio.md`.
- **Note interne al progetto**: prefisso con sigla/nome progetto per auto-localizzazione.
	- Esempio AIOS: `AIOS-Audit-Primitive-Agentiche`, `AIOS-Brainstorm-Knowledge-Map-Padre`.
	- Esempio FT: `FT-Bug-Mercati-Sospesi-Prezzo-Differito`, `FT-Vincolo-Sportmonks-Piano-API`.
- Sotto-cartelle permesse quando il progetto supera ~8 note e ha cluster evidenti.

## Conoscenza (`40-Conoscenza/`)

Persone, aziende, fonti, concetti singoli: **nessun prefisso**. Il nome *è* l'identificatore. Esempio: `Angelini-Pharma.md`, `Claude-Code.md` (no spazi).

## Diario (`10-Diario/`)

- Giornaliero: `YYYY-MM-DD.md`
- Settimanale: `YYYY-Www.md` (es. `2026-W16.md`)
- Mensile: `YYYY-MM.md`
- Trimestrale: `YYYY-Qn.md`
- Riunioni: `YYYY-MM-DD-<Tema>.md`

## Procedura di verifica prima di salvare

1. Il filename rispetta il pattern del territorio (dominio / iniziativa / conoscenza / diario)?
2. Nessuno spazio, nessun emoji nel filename?
3. Se nota di dominio: ho messo il prefisso `<Dominio>-` (oppure uno dei 4 tipi canonici)?
4. Se nota di iniziativa: ho messo il prefisso progetto?
5. Wikilinks in ingresso esistenti puntano al nuovo nome? (rilevante solo in rinomina)

## Debito da migrazione

> [!success] Migrazione completata 2026-04-16
> Allineamento batch eseguito: 23 rinomine (spazi eliminati; prefissi `FT-`, `AIOS-`, `Strumenti-`, `Tecnologia-`, `Prodotto-`, `Crescita-` applicati; kebab-iniziale-maiuscola normalizzato). Wikilinks e `@-refs` di `CLAUDE.md` aggiornati in-place preservando alias (`|`) e sezioni (`#`). Zero orfani residui al check finale. Decisione presa: `3A-Strumenti-e-Sistemi/*` non canoniche portate sotto Pattern A con prefisso `Strumenti-`.

## Collegamenti

- [[Dashboard]]
- [[Strumenti-Filing-Brain-Globale-Locale]] — principio filing globale vs locale
