---
tipo: processo
creato: 2026-04-26
aggiornato: 2026-04-26
stato: attivo
tags:
  - strumenti/backup
  - strumenti/github
area: strumenti
pillar_primario: "P1"
pillar_secondari: []
forma_aggancio: asset
sistema_owner: "[[Processo-Cattura-E-Retrieval-Informazioni]]"
---

# GitHub Backup Vault

> [!info] Setup
> Il vault Obsidian è versionato su GitHub come repo privata. Funge da backup e storico delle modifiche al secondo cervello.

## Configurazione

- **Repo**: `tuccinardiraffaele-lab/second-brain` (privata)
- **URL SSH**: `git@github.com:tuccinardiraffaele-lab/second-brain.git`
- **Branch**: `main`
- **Auth**: SSH via chiave `id_ed25519_github`

## File esclusi (.gitignore)

- `.obsidian/workspace.json` — stato macchina-specifico di Obsidian
- `.obsidian/workspace-mobile.json`
- `.obsidian/cache`
- `.claude/settings.local.json` — configurazioni locali Claude Code

## Workflow di aggiornamento

```bash
cd ~/Second\ Brain
git add -A
git commit -m "update: YYYY-MM-DD breve descrizione"
git push
```

## Note collegate

- [[Processo-Cattura-E-Retrieval-Informazioni]]
- [[Strumenti-Claude-Code]]
