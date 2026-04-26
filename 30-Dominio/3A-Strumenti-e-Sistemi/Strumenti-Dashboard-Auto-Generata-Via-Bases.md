---
tipo: decisione
creato: 2026-04-13
aggiornato: 2026-04-13
stato: attivo
tags:
  - decisione/strumenti
area: strumenti
reversibilità: media
impatto: basso
scadenza-revisione: 2026-07-13
---

## Contesto

La Dashboard (`_Sistema/Dashboard.md`) deve essere il cockpit operativo del vault, con in cima tre blocchi sempre freschi: stato dei filoni strategici, OKR del trimestre con % di avanzamento, cockpit giornaliero. Se l'aggiornamento dipende da edit manuali, la nota muore in fretta: diventa disallineata e smette di essere affidabile, quindi smette di essere usata.

## Decisione

**La Dashboard è costruita come shell di embed su file `.base`, che pescano dinamicamente da note-fonte atomiche con frontmatter strutturato (`tipo: filone | kr | progetto`). Non è una nota curata a mano.**

I tre blocchi in cima sono embed di tre basi separate (`filoni.base`, `okr.base`, `cockpit.base`) in `_Sistema/bases/`.

## Alternative considerate

1. **Dashboard curata a mano** — scartata: l'attrito di aggiornamento è la causa numero uno di morte delle dashboard. A 2 settimane smetti di aggiornarla, a 4 smetti di guardarla.
2. **Dashboard auto-generata ma da un unico schema monolitico** (una sola query gigante) — scartata: viola MECE, le stesse note-fonte non sono riutilizzabili in altre viste (per es. una futura review trimestrale che voglia rileggere gli stessi KR).

## Rationale

- **Separazione presentazione/dati.** La Dashboard è solo layout; i dati vivono dove devono vivere (i KR in `32-Strategia-Business/KR/`, i filoni in `32-Strategia-Business/Filoni/`, i progetti in `20-Iniziative/🔥-Attive/`).
- **Riuso.** Le stesse note atomiche alimenteranno domani la review settimanale, la review trimestrale, le viste per area.
- **Disciplina forzata.** Per far "accendere" la Dashboard servono frontmatter strutturati sulle note-fonte — cosa che serve comunque al vault, indipendentemente dalla Dashboard.

## Rischi e trade-off

- **Costo upfront** — prima che la Dashboard si popoli, vanno create/aggiornate le note-fonte (4 filoni, KR atomici, frontmatter progetti). Mitigazione: checklist di accensione in fondo alla Dashboard, con ordine suggerito (progetti → filoni → OKR).
- **Dipendenza dalla disciplina di frontmatter** — se i campi non sono compilati correttamente, i blocchi restano vuoti e la Dashboard sembra rotta. Mitigazione: schema documentato nella checklist stessa.
- **Vincolo su Obsidian Bases** — se cambia il comportamento dei `.base` con aggiornamenti futuri di Obsidian, va sistemato. Trade-off accettato: il valore del riuso supera il rischio di maintenance.

## Revisione

Rivedere entro [[Scadenziere#2026-07-13]] — criteri di successo:

- La Dashboard viene aperta e consultata nella pratica quotidiana (non ignorata).
- I tre blocchi in cima mostrano dati reali e aggiornati, non placeholder.
- Il costo di mantenere i frontmatter delle note-fonte è sostenibile (non percepito come burocrazia).

Se uno dei tre fallisce, valutare ritorno a Dashboard manuale o ibrida.

## Note collegate

- [[Dashboard]] — l'artefatto costruito da questa decisione
- [[Strategia-Attuale]] · [[OKR-Correnti]] · [[Crescita-Priorità-Correnti]]
- [[Valori-Fondamentali]] — questa decisione serve *produttività = velocità × efficacia*
