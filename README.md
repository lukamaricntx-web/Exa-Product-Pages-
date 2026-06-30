[README_1.md](https://github.com/user-attachments/files/29514344/README_1.md)
# Exaware — AS4625-54T Product Page

A self-contained, single-file product page for the Edgecore **AS4625-54T (EPS121)**
enterprise switch, built on Exaware branding (exact brand blue `#348BFF` + traced
`exaware` wordmark) and structured like a commerce product page (gallery,
configurable buy box, highlights, tabbed specs, ordering, compliance, downloads).

---

## Files

| File | What it is |
|---|---|
| `as4625-54t.html` | The product page. Everything is inlined — CSS, JavaScript, product images (base64), and the logo. No build step, no server, no dependencies. |
| `exaware-wordmark-blue.svg` | Traced `exaware` logotype, brand blue. Reusable in other docs/decks. |
| `exaware-wordmark-white.svg` | Same logotype, white (for dark backgrounds). |
| `exaware-wordmark-white.png` | High-res transparent PNG fallback for tools that won't take SVG. |

---

## Open & edit offline (no setup)

1. **Preview:** double-click `as4625-54t.html` — it opens in any browser.
2. **Edit:** open it in a code editor (VS Code recommended; Sublime, Notepad++, BBEdit all fine).
3. **See changes:** save the file, then refresh the browser tab.

That's the whole loop. (VS Code's *Live Server* extension auto-refreshes on save, but a manual refresh works identically.)

> Do **not** edit in Word, Google Docs, or any rich-text editor — they corrupt the markup. Use a plain code/text editor.

---

## How the file is laid out

One HTML document with four regions:

- **`<style>` in `<head>`** — all the CSS. The `:root { … }` block at the very top is your color control panel.
- **`<symbol id="exawareWM">`** (right after `<body>`) — the traced wordmark, defined once and reused in the header and footer.
- **The body** — broken into labeled sections. Search the comment to jump to one:
  `<!-- hero -->`, `<!-- highlight band -->`, `<!-- service strip -->`,
  `<!-- OVERVIEW -->`, `<!-- SPECS -->`, `<!-- INTERFACES -->`,
  `<!-- ORDERING -->`, `<!-- COMPLIANCE -->`, `<!-- DOWNLOADS -->`.
- **`<script>` at the bottom** — the configurator data and all interactions (tabs, gallery, quantity, cart/quote).

---

## Common edits (with search terms)

| To change… | Search for… | Notes |
|---|---|---|
| Price | `From $1,295` | Plain text in the buy box. |
| SKU | `EXA-4625-54T` | |
| Brand blue | `--cyan-500:#348BFF` | See the naming note below. |
| Link / hover blue | `--cyan-600:#1E74E8` | |
| Blue highlights band | `.hl{background:var(--cyan-500)` | |
| Specs content | `<!-- SPECS -->` | Plain HTML tables. |
| Ordering rows | `<!-- ORDERING -->` | Visible table — see sync note below. |
| Configurator data | `PART = {` | Script object that drives the live readout. |
| Quote button action | `quoteBtn` | Currently a placeholder — see "Wire up actions". |
| Headline / subtitle | `AS4625-54T 54-Port` | In the buy box. |

### ⚠️ Color variable naming
When the palette was remapped to Exaware blue, the brand value kept the variable
*name* `--cyan-500`. So **`--cyan-500` is your brand blue (`#348BFF`)**, and
`--cyan-600` is the darker link/hover shade. Change them in `:root` and the whole
page follows. (The name is cosmetic — rename throughout if it bothers you, but it's
not required.)

### ⚠️ Keep the configurator in sync
Part numbers live in **two** places that must match:
1. The **visible table** in `<!-- ORDERING -->`.
2. The **`PART = { 'F-US':'F0PEC4654413A', … }`** object in the script, which powers
   the live Model/Part number readout when someone picks airflow + region.

If you add or change a variant, update both.

---

## Wire up actions (before going live)

The buttons are demo stubs:

- **Request a quote** — search `quoteBtn`. It currently fires a placeholder `alert()`.
  Replace with a `mailto:`, a redirect to your quote form, or a CRM call.
- **Add to cart** — search `addBtn`. It's a visual demo (increments the header badge),
  not a real cart. Wire to your store backend or remove it if quote-only.
- **Datasheet download** — search `dsLink`. Point `href` at the hosted PDF.

---

## About the images (important)

The three product photos are embedded as `data:image/jpeg;base64,…` strings. That's
what makes the file fully portable (one file, works anywhere) — but those strings are
thousands of characters and **not hand-editable**.

To swap a photo, you have two options:

- **Stay single-file:** replace the entire `data:…` string with a new base64 blob.
- **Easier for ongoing work (recommended for a real site):** change the `src` to a
  normal path, e.g. `src="images/front.jpg"`, and keep an `images/` folder next to
  the HTML. You lose single-file portability but gain sane image editing — which is
  how you'd run it on a live site anyway.

There are three images: the gallery **Front**, **Port panel**, and **Rear / PSU** shots
(also reused in the Interfaces tab).

---

## Deploying

It's static HTML — host it anywhere:

- Drop the file (and an `images/` folder if you externalize images) onto any web host,
  S3/CloudFront, Netlify, GitHub Pages, or an internal server.
- No backend is required for the page itself; only the quote/cart/datasheet actions
  need wiring to your systems.

---

## Brand reference

- **Brand blue:** `#348BFF` (sampled from the official banner)
- **Wordmark:** white on blue/dark, brand blue on white — provided as SVG (preferred)
  and PNG. The traced vector preserves the connected **"ex"** ligature exactly and stays
  sharp at any size.
- **Headings:** kept on a dark ink (not blue) for readability; accents, CTAs, links,
  and the highlights band carry the brand blue.
- **Contrast note:** white-on-`#348BFF` is ~3:1 — fine for the large bold CTA and band
  headings (it's the brand's own banner choice), so body copy and small labels are kept
  on dark ink rather than blue.

---

## Want a different format?

- **Split / project version** — `index.html` + `style.css` + `script.js` + `images/`,
  much friendlier to edit and version-control.
- **Embeddable snippet** — just the buy-box + tabs block to paste into an existing CMS,
  rather than a standalone page.

Ask and I'll generate either.
