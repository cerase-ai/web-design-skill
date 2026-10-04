---
name: web-design
description: "Generates responsive HTML/CSS pages from a brief: landing page, one-pager, static mini-site. Output: a self-contained, mobile-first `.html` file, readable on mobile + desktop. Use when the user asks for \"a landing page\", \"a web page\", \"a single-page site\" or the like."
---
# Web design — static landing pages and one-pagers

Generate a self-contained HTML page (HTML + inline CSS + optionally a little JS) from a brief. Written for landing pages, product or service one-pagers and small static sites. A genuinely interactive application is not a page: say so, and that the work belongs to a developer.

## When to use it

Typical triggers:
- "build me a landing page for product X"
- "I want a web page introducing us"
- "generate a one-pager about this offer"
- `source-to-artifact` with `target_format=html` and `target_kind=site/landing`

Do NOT use it for:
- material that wants to become slides → `deck`
- formal documents → `docx` / `pdf-writer`
- React or Vue components and real applications → out of scope here

## Stage 1 — brief (interview)

Ask one question at a time, and collect:
1. **What the page is for**: sell a product, collect leads, explain a service, or hub and link?
2. **Audience**: who lands here — B2B, B2C, or people inside the company?
3. **Sections needed**: hero, features, pricing, testimonials, FAQ, footer? How many?
4. **Brand**: is there a primary colour, a typeface, a logo? Take the URL or path of the logo if there is one.
5. **Main call to action**: what should the visitor do — fill a form, send an email, phone, book a demo?

Save the brief as `web-design-brief.md` in the workspace.

## Stage 2 — wireframe in text

Produce `web-design-wireframe.md` holding the structure section by section: a title, one or two sentences of description, and any bullets or links. Show it to the colleague and get their agreement before writing any HTML.

## Stage 3 — self-contained HTML

Produce `<filename>.html`, default `landing.html`, under these constraints:
- **Single file**: HTML plus inline CSS in `<style>`. No external import except at most one Google font (`<link rel="preconnect">` and `<link rel="stylesheet">`).
- **Responsive, mobile first**: CSS Grid or Flexbox with a base media query (`@media (min-width: 768px)`).
- **No framework**: no Bootstrap, no Tailwind, no jQuery. Semantic HTML5 and CSS.
- **Performance**: aim under 50KB in total. Inline only what is needed.
- **Accessibility baseline**: a lang attribute, alt text on images, AA contrast, a visible focus state.
- **Semantic sections**: `<header> <main> <section> <footer>` rather than a `<div>` for everything.

Save it in the workspace with your write tool and attach it: `[[attach: <filename>.html]]`.

## Stage 4 — optional variants, only when asked for

The colleague may ask for:
- **the landing as a PDF** → `call_recipe("cerase-office-converter.convert_html_to_pdf", {"path": "<filename>.html", "output_filename": "<filename>.pdf"})`. It prints the page the way a browser does, keeping the grid, the flexbox layout and the background colours, on A4 portrait; add `"orientation": "landscape"` for a wide page. It answers `{path, filename, size_bytes}`: attach it with `[[attach: outputs/<filename>.pdf]]`. An image the page names by a relative path is not found by the converter, so for the PDF put images inline as `data:` URIs or link them by https URL
- **a dark and a light version** → produce two files, `<filename>-light.html` and `<filename>-dark.html`
- **copy changes** → reopen the file, apply them, save.

## Style rules

- **Type**: at most two families, one for headings and one for body. Headings heavier (600-700), body 400. Body line-height 1.5 or more.
- **Colour**: one primary, one accent, and neutrals — white, two or three greys, black. No rainbow.
- **Hero**: one `h1`, one subtitle, one main call to action, optionally an image or illustration. Above the fold.
- **Generous spacing**: `padding: 60px 24px` per section on desktop, `padding: 40px 16px` on mobile.
- **No distracting animation**: at most one fade-in on the hero. No parallax, no scroll-jacking.

## Don't

- Don't embed a remote image with no fallback — the page may be opened offline, or with images blocked.
- Don't slip in a third-party tracker or pixel unless it was asked for explicitly.
- Don't pretend to be a multi-page site. This skill makes single pages; when more are needed, say so and offer to do them one at a time.
- Don't leave lorem ipsum in the result. When the real copy is missing, ask for it or use a placeholder that is visibly marked, such as `[INSERIRE QUI: titolo cliente]`.
