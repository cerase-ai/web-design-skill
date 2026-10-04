# web-design-skill

A Cerase skill that has the assistant build a single responsive web page from a
brief: a landing page, a one-page presentation of a product or service, or one
page of a small static site. The output is one self-contained `.html` file.
The assistant uses it for requests such as "build me a landing page for
product X" or "a web page introducing us", and when `source-to-artifact` asks
for HTML. Slides go to `deck`, formal documents to `docx` or `pdf-writer`, and
React or Vue components and real applications are out of scope.

## What the assistant does

1. **Brief.** Asks, one question at a time, for the purpose of the page, the
   audience, the sections, the brand (colour, typeface, logo) and the main call
   to action, and saves the answers as `web-design-brief.md`.
2. **Wireframe.** Writes `web-design-wireframe.md`, section by section, and
   waits for agreement before writing any HTML.
3. **HTML.** Writes `landing.html` (or the requested name) and attaches it:
   one file with inline CSS and at most one Google font; mobile-first with
   Grid or Flexbox; no framework; under 50 KB; a `lang` attribute, alt text,
   AA contrast and a visible focus state; semantic `header`, `main`,
   `section` and `footer`.
4. **Variants, only on request:** a light and a dark file, copy changes, or a
   PDF of the page.

Style rules: two type families at most, body line height of 1.5 or more, one
primary and one accent colour plus neutrals, a hero with one `h1`, one
subtitle and one call to action, generous section padding, and at most one
fade-in. No remote image without a fallback, no tracker unless asked for, no
lorem ipsum: missing copy gets a visibly marked placeholder. A request for
several pages is done one page at a time.

For the PDF variant the assistant calls
`cerase-office-converter.convert_html_to_pdf` with the page's workspace path,
so that variant needs the `cerase-office-converter` connector. The converter
prints the page with headless Chromium, keeping the grid, the flexbox layout
and the background colours, on A4 portrait, or landscape for a wide page. It
writes the PDF to `outputs/` in the workspace and returns its path, and the
assistant attaches it with `[[attach: <path>]]`. The converter receives the
HTML file alone, so for the PDF images go inline as `data:` URIs or are linked
by https URL.

## Files

| File | Purpose |
|---|---|
| `SKILL.md` | The instructions the assistant loads: `name` and `description` frontmatter, then the four stages and the style rules. |
| `cerase.json` | Marketplace manifest: namespace `studio.guidance`, name `web-design`, display name, description, licence. |
| `i18n.yaml` | Italian display name and description for the Marketplace; not sent to the assistant. |
| `LICENSE` | MIT licence text. |

## Installation

Published in the Cerase Marketplace as `studio.guidance/web-design`
([marketplace page](https://marketplace.cerase.ai/en/p/studio.guidance/web-design)).
A Cerase appliance also ships it in its image. It reaches an assistant through
a template that includes it, as the appliance's starter general-assistant
template does, or when an administrator attaches it.

## License

MIT. See [LICENSE](LICENSE).
