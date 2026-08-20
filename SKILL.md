---
name: web-design
description: "Generates responsive HTML/CSS pages from a brief: landing page, one-pager, static mini-site. Output: a self-contained, mobile-first `.html` file, readable on mobile + desktop. Use when the user asks for \"a landing page\", \"a web page\", \"a single-page site\" or the like."
---
# Web design — landing / one-pager statici

Genera una pagina HTML autocontenuta (HTML + CSS inline + minimo JS opzionale) da un brief. Pensata per landing page, one-pager prodotto/servizio, mini-sito statico. Per app interattive vere usa `artifacts-builder` (se installata) o delega al team frontend.

## Quando attivare

Trigger tipici:
- "fammi una landing per il prodotto X"
- "voglio una pagina web di presentazione"
- "genera un one-pager su questa offerta"
- `source-to-artifact` con `target_format=html` e `target_kind=site/landing`

NON attivare per:
- presentazioni che vogliono diventare slide → `deck`
- documenti formali → `docx` / `pdf-writer`
- componenti React/Vue / app vere → non è scope di questa skill

## Stage 1 — brief (interview)

Raccogli, una domanda alla volta:
1. **Obiettivo della pagina**: vendere un prodotto / raccogliere lead / spiegare un servizio / hub-and-link?
2. **Pubblico**: chi atterra qui? (B2B / B2C / interno aziendale)
3. **Sezioni necessarie**: hero, features, prezzi, testimonial, FAQ, footer? Quante?
4. **Brand**: hai un colore primario, un font, un logo? (URL/path al logo se ne hai uno)
5. **CTA principale**: cosa deve fare il visitatore? (compila form, scrivere email, chiamare, prenotare demo)

Salva il brief in `web-design-brief.md` nel workspace.

## Stage 2 — wireframe testuale

Produci `web-design-wireframe.md` con la struttura per sezione: titolo + 1-2 frasi descrizione + eventuali bullet/link. Mostralo all'utente e chiedi conferma prima di scrivere HTML.

## Stage 3 — HTML autocontenuto

Produci `<filename>.html` (default `landing.html`) con questi vincoli:
- **Single file**: HTML + CSS inline `<style>`; niente import esterni eccetto eventuale 1 font Google (`<link rel="preconnect">` + `<link rel="stylesheet">`).
- **Responsive mobile-first**: layout con CSS Grid / Flexbox + media query base (`@media (min-width: 768px)`).
- **Niente framework**: no Bootstrap/Tailwind/jQuery. Solo HTML5 semantico + CSS.
- **Performance**: target `<50KB` totali. Inline solo l'essenziale.
- **Accessibility baseline**: lang attribute, alt text su immagini, contrasto AA, focus visible.
- **Sezioni semantiche**: `<header> <main> <section> <footer>` invece di `<div>` everywhere.

Salva nel workspace, attacca alla risposta.

## Stage 4 — varianti opzionali (solo se richieste)

L'utente può chiedere:
- **PDF della landing** → encode HTML in base64 + `call_recipe("cerase-office-converter.convert_html_to_pdf", {input_b64: ...})` → salva `.pdf` in workspace
- **Versione dark/light theme** → genera 2 file `<filename>-light.html` + `<filename>-dark.html`
- **Modifiche al copy** → riapri il file, applica le modifiche, salva.

## Style rules

- **Tipografia**: max 2 famiglie di font (1 heading, 1 body). Heading più pesante (600-700), body 400. Line-height ≥ 1.5 per body.
- **Colori**: 1 primary + 1 accent + neutrali (bianco / 2-3 grigi + nero). Niente arcobaleno.
- **Hero**: 1 titolo (h1) + 1 sottotitolo + 1 CTA principale + immagine/illustrazione opzionale. Sopra il fold.
- **Spaziature generose**: `padding: 60px 24px` per section desktop, `padding: 40px 16px` per mobile.
- **Niente animazioni distraenti**: max 1 fade-in sulla hero, niente parallax / scroll-jacking.

## Don't

- Don't embed remote images senza fallback (l'utente potrebbe aprire la pagina offline / con immagini bloccate).
- Don't infilare tracker / pixel di terzi senza che l'utente lo abbia chiesto esplicitamente.
- Don't pretendere di essere un sito multi-pagina: questa skill è per pagine singole. Se servono più pagine, dillo all'utente e proponi di farne una alla volta.
- Don't usare lorem ipsum nel risultato finale. Se manca il copy reale, chiedi all'utente o usa placeholder marcati visibilmente (`[INSERIRE QUI: titolo cliente]`).
