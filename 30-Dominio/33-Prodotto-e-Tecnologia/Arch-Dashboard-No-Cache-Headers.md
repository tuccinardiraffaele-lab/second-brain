---
tipo: architettura
creato: 2026-04-28
aggiornato: 2026-04-28
stato: attivo
tags:
  - architettura/frontend
  - architettura/caching
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
---

# Dashboard — middleware no-cache su tutte le response dinamiche

## Contesto
La dashboard del prodotto (es. human-review-service) serve sia pagine HTML root sia partial HTMX (`/list-partial`, `/count`, ecc.) sotto lo stesso dominio. Dopo ogni rebuild dell'immagine Docker, il template root cambia (nuovi `hx-trigger`, nuovi listener, nuovi id target). Se il browser serve da cache la versione precedente, i listener registrati non corrispondono ai nuovi handler server e gli `HX-Trigger` server-emessi cadono nel vuoto.

## Pattern
Middleware HTTP che applica a **tutte** le response, eccetto `/static/`:
```python
@app.middleware("http")
async def _no_cache_dashboard(request: Request, call_next):
    response = await call_next(request)
    path = request.url.path
    if not path.startswith("/static/"):
        response.headers["Cache-Control"] = (
            "no-store, no-cache, must-revalidate, max-age=0"
        )
        response.headers["Pragma"] = "no-cache"
        response.headers["Expires"] = "0"
    return response
```

Tre header insieme perché Chrome, Firefox e Edge interpretano diversamente: `Cache-Control: no-store` è il più severo (Chrome), `Pragma: no-cache` per HTTP/1.0 fallback, `Expires: 0` per BFCache su Safari/Firefox.

## Cosa cachare invece
Solo `/static/` (CSS, JS, font, lucide icons). Versionare via filename (es. `aios-studio.v2.css`) quando si fanno breaking change.

## Trade-off
Costo: ogni navigazione ricarica HTML+JS della shell (kilobyte). Beneficio: zero rischio di drift template/handler dopo deploy. Per dashboard interna single-tenant <10 utenti il trade-off è banale.

## Quando NON usarlo
- Dashboard pubbliche con migliaia di utenti concorrenti (CDN edge cache è troppo prezioso).
- Pagine puramente static-rendered senza HTMX/AJAX.

## Note collegate
- Si combina con [[Arch-HTMX-Refresh-Inline-Script]] per chiudere completamente la classe di bug "fix server invisibile per cache client".
- Sorgente brain locale: `.brain/60-Pattern/Pattern-Dashboard-No-Cache-Headers.md`
- Sessione di emersione: AIOS Studio Phase 10 UI sprint, 2026-04-28.
