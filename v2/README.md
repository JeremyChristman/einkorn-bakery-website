# Einkorn Bakery Website — v2 "Slim"

A **second, independent design direction** for Will's at-home einkorn bakery.
Same content, same placeholders, completely different site.

**This does not replace v1.** The original design still lives at the repo root and
is still published. The two are meant to be looked at side by side:

| | Design | Lives in | Published at |
|---|---|---|---|
| **v1** | Cream and gold, illustrated, 11 sections | `/index.html` | `https://jeremychristman.github.io/einkorn-bakery-website/` |
| **v2** | Paper and ink, typographic, 6 sections | `/v2/index.html` | `https://jeremychristman.github.io/einkorn-bakery-website/v2/` |

**Status: v2.0 mockup — not launched.** Brand name, contact details, prices,
photos, and the cottage-food statement are all placeholders (listed below).

---

## What this is

- **One file.** The entire site is `index.html` — styling, behavior, and artwork
  all inside it.
- **How to view it:** double-click `index.html`. No build step, no install,
  nothing to run.
- **One external request** (the webfonts — see [Fonts](#fonts)). Everything else
  is inline. v1 made zero requests; this is the single deliberate difference.
- **35 KB of HTML**, down from v1's 46 KB. With the two fonts, an English
  visitor downloads about **119 KB** cold and nothing at all on repeat visits.

The file opens with a table of contents comment mapping every section.

## The design, and why it looks like this

The brief was "less busy, simpler, sleeker." Concretely, versus v1:

- **11 sections → 6.** Our Story and the pull quote merged into *The Baker*; the
  six bread cards became a four-item list; eleven "why einkorn" cards became
  three figures and two paragraphs; six FAQ entries became four.
- **No alternating background bands.** v1 separated sections with cream/flour
  color blocks. v2 uses whitespace and 1px rules, so the page reads as one
  continuous sheet instead of a stack of panels.
- **One accent, not a palette.** Warm paper, near-black ink, and a single clay
  red used only for links, the step numbers, the disclaimer rule, and focus
  rings. One dark band, the footer.
- **Type carries the design.** Fraunces (a warm, high-contrast serif) for
  display, Inter for text. No shadows, no gradients, no rounded card grid.
- **Two photo slots instead of eight.** One wide slot under the hero, one
  portrait beside Will's story. Fewer, larger, better.
- **No hamburger menu.** On phones the header keeps the wordmark and one "Order"
  link; the full navigation lives in the footer. That removed the only piece of
  JavaScript the page structurally depended on.

What did **not** change, on purpose: the einkorn-is-not-gluten-free disclosure
still appears in three places (the Grain section, the allergy note under the
bread list, and the footer). That content is not negotiable in a redesign.

## Fonts

The one external dependency, and the only network request the page makes:

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fraunces:opsz@9..144&family=Inter:wght@400;500&display=swap">
```

**Do not add a weight to the Fraunces request, and do not set `font-weight` on
anything using it.** Fraunces is asked for at a single weight with only its
optical-size axis variable. The moment a second weight is needed, Google serves
the full variable file instead — measured, that is 67 KB rather than 35 KB for
the latin subset. Setting `font-weight: 500` on Fraunces now would also produce
a synthesized faux-bold, which looks worse than the real thing.

- It **degrades cleanly.** Both stacks have full system fallbacks
  (`ui-serif`/Georgia, and the native UI sans), so the site is complete and
  readable offline or if Google Fonts is blocked. `display=swap` means text is
  never invisible while fonts load.
- **To remove it entirely:** delete the `<link rel="stylesheet">` line and the
  two `<link rel="preconnect">` lines above it. Nothing else needs to change —
  the `--display` and `--text` tokens already name the fallbacks. You lose the
  typographic character; you gain zero-request parity with v1.
- **Privacy note:** requesting the fonts discloses the visitor's IP address, user
  agent, and referring page to Google. For a Connecticut home bakery this is
  ordinary, but it is a real (if small) reason someone might choose to remove it
  or self-host the two font files instead.

## Renaming the bakery

The brand name is the exact, **case-sensitive** string `Ancient Grains`. It
appears **exactly 8 times** in `v2/index.html`:

| # | Where |
|---|-------|
| 1 | Inside the header comment block |
| 2 | The `<title>` tag |
| 3 | The meta description |
| 4 | The JSON-LD structured data (`"name"`) |
| 5 | The header wordmark |
| 6 | One sentence in The Baker ("Ancient Grains is his answer…") |
| 7 | The footer wordmark |
| 8 | The footer copyright line |

It never appears in class names, IDs, anchors, or CSS, so a case-sensitive
find-and-replace is guaranteed complete. Your editor should report 8
replacements — if it reports a different number, stop and look.

**Note the count differs from v1's 9.** If you rename both sites, do them
separately and check each count.

After renaming, re-read the `<title>` and meta description aloud so the grammar
around the new name still works.

## Placeholders to replace before launch

| Placeholder | What it is | Notes |
|---|---|---|
| `hello@example.com` | Order email | 2 places; the `mailto:` links use the same string |
| `(860) 555-0134` | Phone | 2 places; **also update the `tel:+18605550134` links** (2 places, digits only) |
| `@yourbakeryhandle` | Instagram | The link points at the instagram.com **homepage** — set the real profile URL too |
| `Hartford County, Connecticut` | Pickup area | Also "Hartford County, CT" in the footer |
| `Fridays` | Bake day | In step 03 |
| `Wednesday` | Order deadline | In step 02 |
| `$12` `$10` `$13` `$18` | The four prices | Delete the "prices are placeholders" line below the list at launch |
| Footer cottage-food statement | Legal disclosure | **MUST be verified against current Connecticut Department of Consumer Protection cottage-food requirements before launch.** The wording is shaped like CT's statement but is a placeholder. |
| Both photo slots | Hero + portrait | See below |

Carried over from v1 and still true: the einkorn nutrition claims are
deliberately hedged and cite **no sources**. v2 states only defensible facts
(age, 100% einkorn, three ingredients) and makes no nutritional claims at all.
If you add any back, add real citations chosen with Will — never invent them.

## Swapping in real photos

There are two slots, both `<figure class="frame">`:

1. **Hero** — `.frame-wide`, 16:7 on desktop and 4:3 on phones.
2. **Portrait of Will** — `.frame-portrait`, 4:5.

To use a real photo, delete everything inside the `<figure>` (the
`<div class="frame-note">` and its SVG) and put an `<img>` in its place:

```html
<figure class="frame frame-wide hero-figure reveal">
  <img src="hero.jpg" alt="A dark-baked einkorn boule, scored across the top, cooling on a wire rack.">
</figure>
```

The CSS already sets `object-fit: cover` and a fixed aspect ratio, so the layout
will not shift whatever the photo's dimensions are.

**Alt text:** describe what is actually in the picture, for someone who cannot
see it — "Will shaping dough at his kitchen bench", not "bakery photo" and not
"image of bread". If a photo is purely decorative and adds nothing, use
`alt=""` instead of removing the attribute.

**File guidance:** roughly 1600px wide for the hero and 900px for the portrait,
compressed as `.webp` or quality-80 `.jpg`. Uncompressed phone photos will make
the page slow for no visible gain.

## Retheming

Every color, font, and rhythm value is a CSS custom property in `:root` at the
top of the `<style>` block, under "TOKENS". Change a value there and it applies
everywhere.

**Unlike v1, the artwork is not hardcoded.** The wheat mark and both placeholder
illustrations are drawn in `currentColor`, so a palette change needs no SVG
edits. The only literal color outside `:root` is `%231A1917` in the favicon data
URI (favicons can't read CSS variables) — update it by hand if the ink color
changes.

Two tokens are load-bearing for accessibility, so change them with care:

- `--rule-ui` is the border that identifies the outlined button as a control. It
  is set to meet the WCAG 3:1 non-text contrast minimum against `--paper`. The
  lighter `--rule` is for decorative hairlines only.
- Every text/background pair in the file was checked against WCAG AA. If you
  change `--paper`, `--ink-mute`, or `--clay`, re-check them.

## Publishing

This directory is already published by the same GitHub Pages setup that serves
v1 — Pages is configured to deploy from `main` at `/ (root)`, and a subdirectory
is served automatically. No settings change was needed; pushing `v2/` published
it at `https://jeremychristman.github.io/einkorn-bakery-website/v2/`.

**If v2 ever becomes the site,** move `v2/index.html` to the repo root
(replacing v1) rather than pointing Pages at a subfolder — that keeps the
top-level URL clean and avoids breaking any link already shared.

Custom domain steps are unchanged and documented in the root `README.md`.

**Source of truth is this git repo — full stop.** Pull before editing, commit and
push when done; uncommitted local work has no backup.

## Optional hardening for launch

Not needed for a mockup with no forms and no user input, but for launch:

```html
<meta http-equiv="Content-Security-Policy"
      content="default-src 'none'; style-src 'unsafe-inline' https://fonts.googleapis.com; font-src https://fonts.gstatic.com; img-src 'self' data:; script-src 'unsafe-inline'; connect-src https://fonts.googleapis.com https://fonts.gstatic.com; base-uri 'none'; form-action 'none'; object-src 'none'">
<meta name="referrer" content="strict-origin-when-cross-origin">
```

Each directive is there for a reason, so don't trim it blind:

- `style-src 'unsafe-inline'` covers the `<style>` block, the handful of inline
  `style=` attributes, and the sentinel's `style.cssText` set from JS. A hash
  isn't practical for a hand-edited file with no build step.
- `connect-src` is what keeps the two `preconnect` hints working — that
  directive governs preconnect, not just fetch.
- `img-src 'self'` is for the real photos when they replace the placeholder
  slots. Keep it, or they will silently fail to load.
- `script-src 'unsafe-inline'` is the low-maintenance choice. A `sha256-` hash
  of the inline script is stricter, but it breaks the moment anyone edits one
  character of that script, and the failure is silent.

Note this is looser than v1's CSP in exactly two places — the Google Fonts
stylesheet and the font files. If you remove the webfonts, drop `style-src` back
to `'unsafe-inline'` alone and delete `font-src` and `connect-src` entirely.

**Subresource Integrity is not viable here** — the Google Fonts `css2` endpoint
serves different CSS per browser, so no single hash matches every visitor, and an
SRI mismatch blocks the stylesheet outright rather than degrading. This was
checked against the live endpoint, not assumed.

**Clickjacking protection is not achievable on this host.** `frame-ancestors` is
ignored by spec when delivered via `<meta>`, and GitHub Pages cannot send custom
response headers (no `_headers` file support). It would need a CDN in front. For
a page with no login, no forms, and no payments, that gap is not worth chasing.

## Known, consciously deferred

- **The FAQ `+`/`–` glyph is CSS generated content**, so Chromium folds it into
  the control's accessible name ("Is einkorn gluten-free? +"). Not a WCAG
  failure — the name is still correct and complete, just slightly noisy for some
  screen readers. Moving the glyph into an `aria-hidden` element would fix it at
  the cost of extra markup on every question.
- **Focus-scroll behavior was verified in Firefox and Chromium, not Safari.**
  `scroll-padding-top` is broadly supported, so this is a small residual gap.
- **The hero headline reflows once on first visit** as Fraunces replaces the
  fallback serif. Correcting it needs per-OS font metric overrides, which is
  disproportionate for a one-page site; repeat visits are unaffected.

## Quality status / changelog

**v2.0 — 2026-08-21 — new design direction.**

Reviewed by three independent agents — code review, accessibility (WCAG 2.1/2.2
AA), and combined security/supply-chain/performance. Every finding was resolved:

- The nav rendered both the desktop and mobile link lists at once, because
  `.site-nav ul` (class + element) out-specified the bare `.nav-wide`/
  `.nav-narrow` rules meant to hide them. Caught in the first playtest.
- `<meta charset>` sat at byte ~3000, outside the HTML5 1024-byte sniff window,
  pushed there by the header comment. Moved to the top of `<head>`.
- The copyright-year update was gated behind an `IntersectionObserver` support
  check it had nothing to do with. Hoisted above it.
- The outlined button's border was 1.31:1 against the page — below the 3:1
  non-text contrast minimum for a border that identifies a control. Added the
  dedicated `--rule-ui` token at 3.19:1.
- Footer and contact links measured 18–22px tall, passing SC 2.5.8 only via the
  spacing exception. Padded to clear 24px outright — these are the primary
  navigation and the primary calls to action on a phone.
- Fraunces was requested across a full variable weight range but rendered at
  only two weights. Pinning it to one weight cut the latin subset from 67 KB to
  35 KB, measured against the live endpoint.
- Dropped an incorrect `servesCuisine` value from the JSON-LD.

Playtested in real Firefox at 320px, 375px, 768px, and 1440px: no horizontal
overflow at any width, no interactive target under 24px, no focused element
obscured by the sticky header across all 24 focusable elements, native
`<details>` operation, the JavaScript-disabled path, the WCAG text-spacing
override, and a webfont-blocked render. Every text and UI color pair was
contrast-checked numerically rather than by eye.

The site is fully usable with JavaScript disabled — scroll reveal and the
header hairline are progressive enhancement and nothing else depends on them.

---

*Site designed and built by Jeremy Christman with Claude (Anthropic).*
