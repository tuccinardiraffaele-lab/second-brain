---
tipo: architettura
creato: 2026-04-28
aggiornato: 2026-04-28
stato: attivo
tags:
  - architettura/frontend
  - architettura/htmx
area: prodotto
progetto: "[[Sistema-Agentico-Studio]]"
---

# HTMX — refresh post-submit via script inline

## Contesto
Dopo il submit di un form HTMX (es. "Conferma firma", "Approva proposta"), il form deve scomparire e la lista contenitore aggiornarsi. La response del POST sostituisce il wrapper del form (target principale) con un alert success; resta da decidere come triggerare il refresh della lista.

## Anti-pattern (fragile)
```html
<div class="alert alert--success"
     hx-trigger="load delay:1500ms"
     hx-get="/.../list-partial"
     hx-target="#listing"
     hx-swap="innerHTML">…</div>
```

Dipende dal fatto che il template della pagina root abbia un container `#listing` con un listener compatibile registrato al `load`. Se il browser serve la pagina root da cache (anche dopo hard reload, BFCache, memory-cache), il listener nuovo non è mai registrato e l'evento si perde silenziosamente. Sintomo: backend OK, ma la card non sparisce.

## Pattern preferito (deterministico)
```html
<div class="alert alert--success">…</div>
<script>
(function(){
  setTimeout(function(){
    if (window.htmx) {
      htmx.ajax("GET", "/.../list-partial",
        {target: "#listing", swap: "innerHTML"});
      htmx.ajax("GET", "/.../count",
        {target: "a#nav-x .nav-badge", swap: "innerHTML"});
    }
  }, 1500);
})();
</script>
```

`htmx.ajax(...)` viene eseguito al swap del fragment, indipendente da listener registrati. Funziona anche con pagina root cached, BFCache, no-cache violato.

## Quando usarlo
- Refresh di lista o badge dopo submit form.
- Pattern di submit con stato lato server processato asincronamente (event-driven): il `setTimeout` dà tempo al consumer di transizionare lo stato prima del GET.

## Quando NON usarlo
- Refresh tempo-reale puro (websocket / SSE migliori).
- Refresh che dipende da multiple condizioni server-side: meglio HX-Location o redirect.

## Note collegate
- Pattern complementare: [[Arch-Dashboard-No-Cache-Headers]] (riduce ulteriormente il rischio di template stale).
- Sorgente brain locale: `.brain/60-Pattern/Pattern-HTMX-Refresh-Inline-Script.md`
- Sessione di emersione: AIOS Studio Phase 10 UI sprint, 2026-04-28.
