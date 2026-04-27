---
tipo: processo
creato: 2026-04-27
aggiornato: 2026-04-27
stato: attivo
tags:
  - strumenti/obsidian
  - strumenti/claude-code
  - processo/qa
area: strumenti
---

# Check Orphan Wikilinks — guardrail brain locale

> [!info] In una frase
> Script eseguibile (`bash` + `python3`) che scansiona tutti i wikilink in un brain locale `.brain/`, applica una **whitelist di refs cross-vault** (note che vivono in `~/Second Brain/`) e fallisce con exit code 1 se trova orfani locali. Pensato come pre-commit hook o CI gate.

## Problema che risolve

Dopo un triage strutturale del brain (vedi [[Processo-Triage-Repo-Multi-Agent]]), restano residual orfani di tre tipi:
1. **Wikilink locali a note inesistenti** (bug, da fixare)
2. **Wikilink cross-vault verso `~/Second Brain/`** (corretti, ma il check tool non lo sa senza scanning del vault)
3. **Wikilink in note `99-Archivio/` deliberatamente obsolete** (non bug, ma rumorosi)

Senza distinzione, qualsiasi check fallisce sempre. Il pattern accettato è: **whitelist esplicita** dei cross-vault attesi, con verifica iniziale che le note whitelisted esistano davvero nel vault.

## Implementazione

```bash
#!/usr/bin/env bash
# .brain/00-Sistema/Check-Orphan-Wikilinks.sh
set -euo pipefail
cd "$(dirname "$0")/../.."

python3 - <<'PY'
import re, sys
from pathlib import Path

EXPECTED_EXTERNALS = {
    "Sistema-Agentico-Studio", "Strategia-Attuale", "OKR-Correnti",
    # ... whitelist verificata esistere in ~/Second Brain/ alla data X
}

refs = set()
for md in Path(".brain").rglob("*.md"):
    for m in re.finditer(r"\[\[([^\]|#]+)", md.read_text(encoding='utf-8')):
        refs.add(m.group(1).strip())

notes = {p.stem for p in Path(".brain").rglob("*.md")}
local_orphans = refs - notes - EXPECTED_EXTERNALS

if not local_orphans:
    print(f"✓ No local orphans ({len(refs)} refs, {len(notes)} notes)")
    sys.exit(0)
else:
    print(f"✗ {len(local_orphans)} local orphan(s):")
    for o in sorted(local_orphans): print(f"  - {o}")
    sys.exit(1)
PY
```

## Manutenzione della whitelist

Quando una nota viene **promossa dal brain locale al vault** (T2 in [[Bridge-Protocol]]), aggiungere la sua slug alla whitelist. Quando una nota cross-vault viene **rimossa o rinominata nel vault**, aggiornare la whitelist (la verifica via `find ~/Second\ Brain -name "<slug>.md"` lo conferma).

## Quando eseguire

- **Manualmente** dopo ogni intervento strutturale sul brain (triage, sprint che crea molte note, merge MOC).
- **Pre-commit hook** opzionale: blocca commit con orfani locali nuovi.
- **CI** del repo: gate che fallisce build se introduci link rotti.

## Trade-off

- **Pro**: deterministico, veloce (<1s), nessuna falsa positiva sui cross-vault, output leggibile.
- **Contro**: la whitelist va mantenuta manualmente. Variante migliore: scansionare anche `~/Second Brain/` dinamicamente per derivare la whitelist — ma costa più I/O e introduce dipendenza esterna nel check.

## Prima applicazione

AIOS Studio, 2026-04-27 — installato come `.brain/00-Sistema/Check-Orphan-Wikilinks.sh`. Stato post-triage: 0 orfani locali, 15 cross-vault whitelisted (verificati esistere nel vault).

## Note collegate

- [[Processo-Triage-Repo-Multi-Agent]]
- [[Strumenti-Filing-Brain-Globale-Locale]]
- [[Bridge-Protocol|Bridge T2 — promozione locale → globale]]
