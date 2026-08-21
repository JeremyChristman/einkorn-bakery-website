# Einkorn Bakery Website (working title: "Ancient Grains")

A one-page website mockup for Will's upcoming at-home einkorn bakery in Connecticut.

**Status: v0.1 mockup — not launched.** The design and structure are done; the brand
name, contact info, prices, and a few facts are placeholders (all listed below).

> ### There are two designs in this repo
>
> This file documents **v1**, the design in `index.html` at the repo root, live at
> `https://jeremychristman.github.io/einkorn-bakery-website/`.
>
> **[`v2/`](v2/README.md) is a separate, independent design direction** — same
> content, quieter and more typographic, live at
> `https://jeremychristman.github.io/einkorn-bakery-website/v2/`. Neither one
> replaces the other; they exist to be compared. v2 has its own README.
>
> If you rename the bakery, do it in **both** files — the occurrence counts
> differ (9 here, 8 in v2).

> **Name ideas:** "Ancient Grains" is a placeholder, not a decision. *Einkorn*
> literally means "one grain" in German, which is fertile naming territory —
> One Grain Bakery, Single Grain, First Wheat, etc. Final name is Will's call.

---

## What this is

- **One file.** The entire site is `index.html`. All styling (CSS), interactivity
  (JavaScript), and artwork (inline SVG illustrations) live inside it.
- **Zero dependencies.** No frameworks, no fonts to download, no external images.
  It makes zero network requests and works completely offline.
- **How to view it:** double-click `index.html`. It opens in any modern browser on
  any machine — nothing to install.

The file has a table of contents in a comment block at the very top (lines 4–39)
that maps every section, plus the rename/placeholder notes repeated in brief.

## Renaming the bakery (the find-and-replace contract)

The brand name is the exact, **case-sensitive** string `Ancient Grains`. It appears
**exactly 9 times** in the file:

| # | Where |
|---|-------|
| 1–2 | Inside the header comment block (lines 23 and 26) |
| 3 | The `<title>` tag |
| 4 | The meta description |
| 5 | The JSON-LD structured data (`"name"`) |
| 6 | The header wordmark (next to the wheat logo) |
| 7 | One sentence in Our Story ("Ancient Grains is Will's answer…") |
| 8 | The footer wordmark |
| 9 | The footer copyright line |

It **never** appears in class names, IDs, anchors, or CSS — so a case-sensitive
find-and-replace of `Ancient Grains` → new name is guaranteed complete. Your editor
should report 9 replacements; if it reports a different number, stop and look.

**After renaming:** re-read the `<title>` and meta description out loud and make
sure they still read naturally with the new name (grammar around the name can shift).

## Placeholders to replace before launch

All of these are also listed in the file's header comment. Search for each string:

| Placeholder | What it is | Notes |
|---|---|---|
| `hello@example.com` | Order email | 2 places (contact block + footer); the `mailto:` links use the same string, so find-and-replace catches both |
| `(860) 555-0134` | Phone | 2 places; **also update the matching `tel:+18605550134` links** (2 places, digits-only format) |
| `@yourbakeryhandle` | Instagram | The link currently points at the instagram.com **homepage** — set the real profile URL too |
| `Hartford County, Connecticut` | Pickup area | Also appears as "Hartford County, CT" in the footer |
| `Fridays` | Bake day | In the "Pick up fresh" step |
| `Wednesday night` | Order deadline | In the "Claim your loaves" step |
| `$12 / $10 / $11 / $14 / $13 / $18` | All six prices | One per bread card; the "prices are placeholders" note below the grid should be removed at launch |
| Footer cottage-food statement | Legal disclosure | **MUST be verified against current Connecticut Department of Consumer Protection cottage-food requirements before launch.** The current wording is shaped like CT's statement but is a placeholder. |

## Pre-launch content TODO

- **Nutrition citations.** The "Why Einkorn" facts (more protein, carotenoids,
  minerals, simpler gluten) are deliberately hedged and currently cite **no
  sources**. Before launch, add 2–3 real citations chosen with Will. Do **not**
  invent citations — find actual published papers or drop the specific claims.
- **Final product lineup and real prices** — decide with Will. The six current
  breads are plausible suggestions, not his menu.

## Swapping in real photos

Each bread card has a fixed 4:3 photo slot (`.card-media`, styled around line 259).
Right now each slot holds a placeholder line-art `<svg>`. To use a real photo:

1. Delete the inline `<svg>…</svg>` inside that card's `<div class="card-media" …>`.
2. Put in its place: `<img src="boule.jpg" alt="describe the bread">` — write alt
   text that actually describes the loaf.
3. Done. The aspect ratio is fixed in CSS, so the layout will not shift regardless
   of the photo's dimensions.

Photo guidance: roughly 800×600 or larger, compressed — `.webp` or a quality-80
`.jpg`. Uncompressed phone photos will make the page slow for no visual gain.

## Retheming (colors, type, spacing)

All colors, fonts, sizes, and spacing are CSS custom properties in `:root` at the
top of the `<style>` block (starting line 57, labeled "DESIGN TOKENS"). Change a
value there and it applies everywhere it's used.

**Caveat:** the illustration gold `#D9A441` is **hardcoded** inside the inline SVGs
and the favicon data URI — SVG presentation attributes can't use `var()`. A full
palette change therefore also requires find-and-replacing:

- `#D9A441` (21 occurrences, mostly SVG artwork)
- `%23D9A441` — the URL-encoded copy inside the favicon (covered by the count
  above; just don't miss it)
- The favicon also hardcodes the stem color `%238A5A14` (the `--gold-deep` value)

## Publishing to GitHub Pages

Done 2026-07-07: this repo (`JeremyChristman/einkorn-bakery-website`) serves the
site via GitHub Pages — Settings → Pages → "Deploy from a branch" → `main`,
folder `/ (root)` — at `https://jeremychristman.github.io/einkorn-bakery-website/`.

**Custom domain:**

1. Buy the domain, then add it in the same Pages settings screen (GitHub creates a
   `CNAME` file in the repo).
2. Point DNS at GitHub: apex domain → A records to GitHub Pages' IPs, and/or
   `www` → CNAME to `<user>.github.io` (GitHub's docs list the current IPs).
3. Once the certificate provisions (can take a bit), check **"Enforce HTTPS"**.

**Source of truth: this git repo — full stop.** The site does not live in Dropbox.
Local clones sit at `C:\Claude\repos\einkorn-bakery-website` on each machine
(same path on both by convention). Workflow: **pull before editing, commit and
push when done** — uncommitted local work has no backup, so don't sit on it.

## Optional security hardening for launch

Not needed for the mockup (it makes no requests and has no forms), but from the
security review, for launch:

```html
<meta http-equiv="Content-Security-Policy"
      content="default-src 'none'; img-src 'self' data:; style-src 'unsafe-inline'; script-src 'unsafe-inline'; base-uri 'none'; form-action 'none'">
<meta name="referrer" content="strict-origin-when-cross-origin">
```

GitHub Pages cannot send custom response headers, so meta tags are the only
available mechanism. Clickjacking protection (`frame-ancestors`) cannot be set via
meta tag at all — not achievable on Pages, and acceptable for a no-form marketing page.

## Known optional polish (consciously deferred)

All reviewer-approved as non-blocking:

- **Skip-link focus ring:** where the ring overlaps the cream page background,
  `--gold-deep` would contrast better than `--gold` (a WCAG AAA-level nicety;
  AA passes as-is).
- **Contact block paragraphs:** the two `<p>`s have no inter-paragraph margin
  (cosmetic).
- **Card hover shadow:** could be moved to a pseudo-element opacity transition for
  compositor-only animation (performance nicety; imperceptible at this page size).

## Quality status / changelog

**v0.1 — 2026-07-07 — initial mockup.**

Built and reviewed through a multi-agent pipeline: architecture review (approved
with revisions, all incorporated), then independent code review, security,
accessibility (WCAG 2.1/2.2 AA), performance, and requirements-validation agents —
all APPROVED on the final code after one fix round. Playtested in a real browser at
375 px / 768 px / 1440 px, including keyboard-only navigation, JavaScript-disabled,
and reduced-motion paths (the site is fully usable without JS; scripting is
progressive enhancement only).

File: ~46 KB, zero network requests, single file.
