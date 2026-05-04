---
tipo: debito-tecnico
creato: 2026-04-24
aggiornato: 2026-04-24
stato: attivo
tags:
  - debito/osservabilità
  - debito/codebase-hygiene
area: prodotto
progetto: "[[Football-Trading]]"
gravità: media
costo-stimato: "1-2h rilevamento, 30' eliminazione"
---

# FT — Pattern Zombie File Locali

## Fenomeno

Un file locale nel repo viene ancora letto da un consumer attivo (API, agent, tooling) ma non è più scritto da nessuna pipeline corrente. Sopravvive come relitto: il path al suo interno punta a una directory che non esiste più, alcuni campi attesi dal consumer mancano, e il consumer interpreta il dato rotto come "dato assente" invece di segnalare l'incoerenza.

## Esempio concreto — 2026-04-24

`models/xgboost_evaluation.json` nel repo `ai-football-trading`. Era il file di evaluation della pipeline di training XGBoost v1. Quando si è passati alla pipeline V2b (`scripts/train_xgboost_local.py` + bundle `.tar.gz` autocontenuto in `trained_models/`), nessuno ha rimosso il file legacy né aggiornato il consumer che lo leggeva (`dashboard/app/api/xgboost/status/route.ts`).

Sintomi osservati prima della rimozione:

- `model_path` interno puntava a `/home/raffaele/ai-football-trading/models/xgboost_pattern_discovery.pkl` — path pre-migrazione, senza `/projects/`
- 4 campi su 6 dichiarati dall'interfaccia TypeScript `EvalJson` erano assenti (`ece`, `calibration_slope`, `calibration_intercept`, `logloss`)
- La dashboard mostrava "Non persistita nel training corrente" per 4 metriche che **esistevano** dentro il bundle `tar.gz` in produzione, ma il consumer guardava nel posto sbagliato

Il file era uno zombie da settimane senza che nessuno se ne accorgesse: nessun errore di runtime, nessun allarme. L'unica conseguenza era una UI che mentiva.

## Pattern riusabile

> [!warning] Lo stato "esiste ma nessuno lo aggiorna" è sempre peggio
> Un file locale ha tre stati validi: (1) scritto e letto dalla pipeline corrente, (2) archiviato in modo esplicito con path `archive/` o suffisso `.legacy`, (3) eliminato. Lo stato "esiste nel path attivo ma è scritto da una pipeline dismessa" è il peggiore: non segnala la dismissione, confonde i consumer, erode la fiducia negli output.

### Come rilevarlo

1. Per ogni file letto da codice produttivo (grep di `readFile`, `open()`, `loadEvaluation`, `json.load`), verifica chi lo **scrive**. Se nessuna pipeline attiva lo scrive, è uno zombie.
2. Controlla i path interni ai file di configurazione/evaluation: se puntano a directory inesistenti, il file è stato generato pre-migrazione e non è più aggiornato.
3. Confronta i campi attesi dal consumer (interfaccia TypeScript, schema Pydantic) con quelli presenti: campi mancanti sistematici sono segnale di schema drift tra writer e reader.

### Come chiuderlo

- **Consumer ancora utile** → ripuntalo alla fonte di verità attuale (nel caso XGBoost: `xgboost_models.metadata_json` JSONB popolato da `upload_trained_model.py`). Elimina il file zombie con `git rm`.
- **Consumer non serve più** → rimuovi insieme sia il file che il ramo del consumer.
- **MAI lasciare come "deprecato"** con commento `# TODO legacy`. CLAUDE.md globale §6 è esplicito: *"se qualcosa è morto, eliminalo invece di marcarlo come deprecato"*.

### Prevenzione a monte

Validare lo schema dell'output della pipeline al momento della **scrittura**, non al momento della lettura. Esempio concreto introdotto nella stessa sessione: `scripts/train_xgboost_local.py::package_model` ora usa `TrainingMetadata` Pydantic REQUIRED: se un campo obbligatorio manca, il save aborta e il bundle non viene prodotto. Se avessimo avuto questo schema sul file `xgboost_evaluation.json` fin dalla v1, non sarebbe sopravvissuto alla migrazione V2b senza errori visibili.

## Collegamento ad altri pattern

Cugino della *zombie decision* (decisione documentata ma mai eseguita come default del codice): stessa matrice — il sistema di conoscenza/osservabilità contiene un'affermazione che non è più vera. La differenza:

- **Zombie file** mente ai **consumer runtime** (API che leggono dati stantii)
- **Zombie decision** mente al **founder al prossimo login** (`.brain/` che contiene aspirazioni presentate come fatti)

Entrambi si prevengono con validazione automatica all'output + cadenza di review (§16 `/weekly` del CLAUDE.md globale).

## Note collegate

- Sorgente: `.brain/planning/2026-04-24-training-window-2y-observability.md` nel repo `ai-football-trading`
- [[Football-Trading]] — MOC del progetto
