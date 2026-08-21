# Einkorn Bakery Website — v3 "Bright"

A **third, independent design direction** for Will's at-home einkorn bakery.
Same content, same placeholders, a completely different look.

**Nothing here replaces v1 or v2.** All three are published and meant to be
compared side by side:

| | Design | Lives in | Published at |
|---|---|---|---|
| **v1** | Cream and gold, illustrated, 11 sections | `/index.html` | `…github.io/einkorn-bakery-website/` |
| **v2** | Paper and ink, minimal and editorial, 6 sections | `/v2/index.html` | `…/einkorn-bakery-website/v2/` |
| **v3** | Bright color panels, bold and graphic | `/v3/index.html` | `…/einkorn-bakery-website/v3/` |

**Status: v3.0 mockup — not launched.** Brand name, contact details, prices,
photos, and the cottage-food statement are all placeholders (listed below).

---

## What this is

- **One file.** The entire site is `index.html` — styling, behavior, and artwork
  all inside it. Double-click it to view; no build step, nothing to install.
- **One external request** (the webfonts — see [Fonts](#fonts)).
- **40 KB of HTML.** With fonts, an English visitor downloads about **117 KB**
  cold and nothing at all on repeat visits.

## The design, and why it looks like this

The brief was "bright and colorful, designed differently." So the organizing
idea is the opposite of v2's: instead of one calm continuous sheet, **every
section is a big rounded panel in its own saturated color**, stacked on a warm
cream page with gaps between them.

- **Marigold** hero → **deep green** for the grain story → cream with **four
  differently-tinted product cards** → **bright tomato** for Will → **blue** for
  ordering → cream questions → near-black footer.
- **Chunky display type.** Bricolage Grotesque at a single heavy weight does the
  shouting; DM Sans carries the reading text.
- **Everything is outlined.** 3px ink borders, pill buttons, a rotated "Baked
  fresh Fridays" sticker, price tags as dark pills, numbered circles for the
  ordering steps. Flat and graphic, no gradients or drop shadows.
- **Colored chips** under the hero carry the four short selling points that v1
  had as a plain list.

What did **not** change, on purpose: the einkorn-is-not-gluten-free disclosure
still appears in three places (the Grain panel, the allergy note under the
bread cards, and the footer). That content is not negotiable in a redesign.

## The color contract — read this before changing any color

This is the one genuinely fragile thing about a design this colorful, so it is
built as a contract rather than a set of loose values.

Each panel class sets three scoped custom properties, and everything inside
inherits them:

| Token | Meaning |
|---|---|
| `--on` | text color for this panel |
| `--ring` | focus-ring color for this panel (needs 3:1 against the panel) |
| `--chip` | the panel's button and card fill |

Plus `--panel-bg`, which `.btn-fill` uses to color its label. **A card that sits
on top of a panel and changes its own background — `.callout`, `.contact` — must
re-scope all four**, not just `--on`. Both already do.

Measured ratios (recompute if you change a value, do not eyeball it):

| Pair | Ratio |
|---|---|
| ink on marigold | 11.11:1 |
| cream on leaf green | 6.22:1 |
| ink on tomato | 5.09:1 |
| cream on blue | 6.18:1 |
| ink on cream / cream on ink | 16.74:1 |
| ink on the four card tints | 13.72–14.59:1 |
| cream on the darkened figure cards | 7.31:1 |

Three traps that were hit while building this, all now fixed and worth knowing:

1. **The tomato panel uses DARK text on purpose.** Cream on tomato is only
   3.29:1 and fails. Do not "fix" it to cream.
2. **Don't fade small text with `opacity`.** The section eyebrows at 75% opacity
   measured 3.59:1 on tomato and 4.2:1 on blue — failures created purely by the
   fade. They now run at full strength.
3. **An ink border is not safe on every panel.** Ink against the leaf green is
   2.69:1, under the 3:1 non-text minimum. Cards sitting on a *dark* panel are
   delineated by their cream fill instead (that is why `.callout` and `.contact`
   have no outline, while every card on a light background does).

## Fonts

The one external dependency, and the only network request the page makes:

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,700&family=DM+Sans:wght@400&display=swap">
```

**Each family is requested at exactly one weight, and that is load-bearing:**

- Asking Bricolage for a second weight makes Google serve the full variable
  file — measured, 77 KB instead of 40 KB for the latin subset. So never set a
  `font-weight` other than 700 on a display element.
- DM Sans is loaded at **400 only**. `<strong>` is therefore restyled onto the
  display face rather than asking DM Sans for bold, which would either be
  synthesized faux-bold or cost another 37 KB for about ten words of allergy
  copy. If you add a bold body style, you must add the weight to the URL too.

It **degrades cleanly** — both stacks have system fallbacks, and `display=swap`
means text is never invisible while fonts load. **To remove the webfonts
entirely:** delete the `<link rel="stylesheet">` line and the two `preconnect`
lines above it. Nothing else needs to change.

**Privacy note:** requesting the fonts discloses the visitor's IP address, user
agent, and referring page to Google. Ordinary for a small business site, but a
real reason someone might prefer to self-host the two font files instead.

## Renaming the bakery

The brand name is the exact, **case-sensitive** string `Ancient Grains`. It
appears **exactly 8 times** in `v3/index.html`:

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
replacements — a different number means stop and look.

**The counts differ per design: 9 in v1, 8 in v2, 8 in v3.** If you rename the
bakery, do all three files separately and check each count.

## Placeholders to replace before launch

| Placeholder | What it is | Notes |
|---|---|---|
| `hello@example.com` | Order email | 2 places; the `mailto:` links use the same string |
| `(860) 555-0134` | Phone | 2 places; **also update the `tel:+18605550134` links** (2 places, digits only) |
| `@yourbakeryhandle` | Instagram | The link points at the instagram.com **homepage** — set the real profile URL too |
| `Hartford County, Connecticut` | Pickup area | Also "Hartford County, CT" in the footer |
| `Fridays` | Bake day | Step 3, and the hero sticker says it too |
| `Wednesday` | Order deadline | Step 2 |
| `$12` `$10` `$13` `$18` | The four prices | Delete the "prices are placeholders" line below the cards at launch |
| Footer cottage-food statement | Legal disclosure | **MUST be verified against current Connecticut Department of Consumer Protection cottage-food requirements before launch.** The wording is shaped like CT's statement but is a placeholder. |
| Both photo slots | Hero + portrait | See below |

As in v1 and v2: the einkorn nutrition claims are deliberately hedged. v3 states
only defensible facts (age, 100% einkorn, three ingredients) and makes no
nutritional claims at all. If you add any back, add real citations chosen with
Will — never invent them.

## Swapping in real photos

Two slots, both `<figure class="frame frame-tall">` (4:5). Delete everything
inside the `<figure>` — the `<div class="frame-note">` and its SVG — and put an
`<img>` in its place:

```html
<figure class="frame frame-tall reveal">
  <img src="will.jpg" alt="Will shaping dough at his kitchen bench.">
</figure>
```

`object-fit: cover` and a fixed aspect ratio are already set, so the layout will
not shift whatever the photo's dimensions are.

**Note on the hero photo:** the rotated sticker deliberately overlaps its
top-right corner. Choose a photo whose subject is not in that corner.

**Alt text:** describe what is actually in the picture, for someone who cannot
see it — "Will shaping dough at his kitchen bench", not "bakery photo". Use
`alt=""` only if a photo is purely decorative.

**File guidance:** roughly 1000px wide, compressed as `.webp` or quality-80
`.jpg`. Uncompressed phone photos will make the page slow for no visible gain.

## Publishing

Already published by the same GitHub Pages setup that serves v1 and v2 — Pages
deploys from `main` at `/ (root)`, and subdirectories are served automatically.
No settings change was needed.

**If v3 ever becomes the site,** move `v3/index.html` to the repo root rather
than pointing Pages at a subfolder — that keeps the top-level URL clean.

Custom domain steps are unchanged and documented in the root `README.md`.

**Source of truth is this git repo — full stop.** Pull before editing, commit
and push when done; uncommitted local work has no backup.

## Optional hardening for launch

Not needed for a mockup with no forms and no user input, but for launch — and
note this must go **near the top of `<head>`**, before the favicon and font
links, because a CSP delivered by meta tag only governs resources requested
after the parser reaches it:

```html
<meta http-equiv="Content-Security-Policy"
      content="default-src 'none'; script-src 'unsafe-inline'; style-src 'unsafe-inline' https://fonts.googleapis.com; font-src https://fonts.gstatic.com; img-src 'self' data:; object-src 'none'; base-uri 'none'; form-action 'none'">
<meta name="referrer" content="strict-origin-when-cross-origin">
```

- `style-src 'unsafe-inline'` covers the `<style>` block and the inline `style=`
  attributes; there is no separate directive for style attributes.
- `img-src 'self'` is for the real photos when they land. Keep it or they will
  silently fail to load.
- Inline `<svg>` needs no directive — it is parsed, not fetched.

**Not achievable on this host:** `frame-ancestors` and `sandbox` are ignored
when delivered via meta tag, and GitHub Pages cannot send custom response
headers, so clickjacking protection would need a CDN in front. Acceptable for a
page with no login, no forms, and no payments. Subresource Integrity is also not
viable — the Google Fonts endpoint serves different CSS per browser, so no fixed
hash matches every visitor.

## Known, consciously deferred

- **The FAQ `+`/`−` glyph is CSS generated content**, so Chromium folds it into
  the control's accessible name ("Is einkorn gluten-free? +"). Not a WCAG
  failure — just slightly noisy for some screen readers.
- **The headline reflows once on first visit** as Bricolage replaces the
  fallback face. Correcting it needs per-OS font metric overrides, which is
  disproportionate here; repeat visits are unaffected.
- **Verified in Firefox and Chromium, not Safari.**

## Quality status / changelog

**v3.0 — 2026-08-21 — bright, color-panel design direction.**

Reviewed by three independent agents — code review, accessibility (WCAG 2.1/2.2
AA), and combined security/supply-chain/performance. Every finding resolved:

- Section eyebrows at 75% opacity measured **3.59:1** on tomato and 4.2:1 on
  blue — small-text failures created purely by the fade. Opacity removed.
- The figure cards lightened the green panel behind them, pulling their own
  label text down to 4.17:1. They now darken the panel instead (7.31:1).
- The FAQ open/closed state was signalled by fill color alone (SC 1.4.1), and
  the closed marigold fill was 1.51:1 against the card. Now a `+`/`−` glyph
  change, so state reads without relying on hue.
- The gluten-disclaimer card's ink border measured **2.69:1** against the green
  panel, under the 3:1 non-text minimum. Now borderless, delineated by its cream
  fill, matching how the contact card behaves on the blue panel.
- `.callout` and `.contact` re-scoped only two of the four panel tokens, so a
  button placed inside either would have inherited the surrounding panel's chip
  colors and rendered nearly invisible. Latent, not live; now complete.
- Dropped DM Sans 700, cutting the font payload **113.6 KB → 76.6 KB (−32%)**.
  `<strong>` now uses the already-downloaded display face, which is both free
  and more emphatic than bold body text.
- Removed `.reveal` from the chip row, the one element close enough to the fold
  for a load-time reveal flash to be visible.

Playtested in real Firefox at 320px, 375px, and 1440px: no horizontal overflow
at any width, no interactive target under 24px, no focused element obscured by
the floating nav, all 13 reveal elements firing on a normal read-through, native
`<details>` operation, the JavaScript-disabled path, and the WCAG text-spacing
override. **Every border in the rendered page was checked programmatically
against its actual backdrop** — not just the ones I thought to list.

The site is fully usable with JavaScript disabled — scroll reveal and the header
shadow are progressive enhancement and nothing else depends on them.

---

*Site designed and built by Jeremy Christman with Claude (Anthropic).*
