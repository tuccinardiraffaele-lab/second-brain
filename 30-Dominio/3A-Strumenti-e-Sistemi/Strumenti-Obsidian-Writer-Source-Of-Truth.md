---
tipo: processo
creato: 2026-04-16
aggiornato: 2026-04-16
stato: attivo
tags:
  - strumenti/vault
  - processo/filing
area: strumenti
---

# Obsidian Writer come single source of truth del filing

> [!info] In una frase
> La skill `obsidian-writer` è l'**unica fonte autoritativa** su dove va scritta ogni nota del vault. Ogni altra skill che tocca il filing (sprint, decision, brainstorm, session-close, meeting, weekly, daily, interview) si allinea a lei.

## Perché esiste questa regola

Il 2026-04-16 un [[Troubleshooting-UPS-Coding|audit UPS]] ha trovato 8 note in posizione errata nel vault. La root cause: `obsidian-writer` prescriveva la vecchia convenzione "un progetto = un file in root di `🔥-Attive/`", mentre `sprint` aveva introdotto la cartella progetto senza sincronizzare la skill di filing master. Le altre skill delegavano a `obsidian-writer` e ne ereditavano l'errore.

> [!danger] Regola non negoziabile
> Quando introduci o modifichi una **convenzione strutturale** nel vault (cartelle progetto, nuovi tipi di nota, nuove aree di dominio, naming), aggiorni **prima** la tabella destinazioni in `obsidian-writer.md`. Solo dopo alleni le altre skill a riflettere la nuova regola.

## Come applicare

1. **Modifica di struttura emerge in una skill di dominio** (es. `sprint` introduce le "note azione aperta").
2. **Stop**: prima di implementarla, aggiorna la tabella in `obsidian-writer.md:§1 Determina la destinazione`.
3. **Allinea**: aggiorna la skill di dominio per referenziare la nuova riga di `obsidian-writer` (non duplicare la regola).
4. **Verifica a freddo**: traccia il decision path su un caso-tipo; la nota deve atterrare nella posizione attesa senza ambiguità.
5. **Documenta**: se la convenzione ha un'eccezione o una motivazione non ovvia, annotala in questa nota come registro dei pattern.

## Anti-pattern da evitare

- Skill di dominio che dichiara un path senza che `obsidian-writer` lo preveda → due fonti di verità.
- Path inferito "per prossimità" (es. nota progetto-specifica che finisce in root perché è lì che sta la MOC vecchia convenzione).
- Classi di nota non esplicite nella tabella → cadono nel default = cartella parent = misfiling.

## Collegamenti

- [[Strumenti-Filing-Brain-Globale-Locale]] — regola più alta: globale (vault) vs locale (.brain di repo)
- [[Troubleshooting-UPS-Coding]] — metodo diagnostico che ha prodotto questa regola
- `~/Second Brain/.claude/skills/obsidian-writer/SKILL.md` — skill di riferimento
