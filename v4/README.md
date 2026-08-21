# Einkorn Bakery Website — v4 "Overnight" (dark)

A **fourth, independent design direction** for Will's at-home einkorn bakery.
Same content, same placeholders, a completely different look — this one dark.

**Nothing here replaces v1, v2 or v3.** All four are published and meant to be
compared:

| | Look | Lives in | Published at |
|---|---|---|---|
| **v1** | Cream and gold, illustrated | `/index.html` | `…github.io/einkorn-bakery-website/` |
| **v2** | Paper and ink, minimal, editorial | `/v2/index.html` | `…/einkorn-bakery-website/v2/` |
| **v3** | Bright color panels, bold and graphic | `/v3/index.html` | `…/einkorn-bakery-website/v3/` |
| **v4** | Warm dark, atmospheric, timeline | `/v4/index.html` | `…/einkorn-bakery-website/v4/` |

**Status: v4.0 mockup — not launched.** Brand name, contact details, prices,
photos, the timeline hours, and the cottage-food statement are all placeholders.

---

## What this is

- **One file.** The entire site is `index.html`. Double-click it to view; no
  build step, nothing to install.
- **One external request** (the webfonts — see [Fonts](#fonts)).
- **42 KB of HTML.** With fonts, an English visitor downloads about **91 KB**
  cold — the lightest of the four designs — and nothing on repeat visits.

## The design, and why it looks like this

The brief was "dark, and completely new." So the dark is not a palette swap
applied to a light layout — **the dark is the subject.** This bread really is
made overnight: mixed around 20:00, baked before dawn, on the counter by 07:00.
The site is set during that night.

- **A warm ember glow** sits behind the hero, standing in for the oven door. The
  ground is a warm near-black, never a cold gray or pure `#000`.
- **The signature device is a vertical timeline** — a lit spine with time markers
  down the left, carrying the "why slow" story that v1–v3 told as prose or cards.
  It is the one section none of the other designs has.
- **Three type voices**: Instrument Serif for headlines (high contrast, elegant
  — it reads as *night*), Karla for text, and IBM Plex Mono for every time,
  price, label, and button. The mono is what makes the schedule feel like a
  schedule.
- **A thin ember scroll-progress line** under the header. Purely decorative.
- No cards, no color blocks, no illustrations — structure comes from hairlines
  and the glow.

What did **not** change, on purpose: the einkorn-is-not-gluten-free disclosure
still appears in three places (the Grain section, the allergy note under the
bread list, and the footer).

## Designing in the dark — the rules that are load-bearing

Dark designs fail in ways that look completely fine on screen. These are not
style preferences; breaking them reintroduces measured failures.

1. **Never fade small text with `opacity` to make it "secondary."** Use the
   `--crumb-mute` token, which is measured at 7.94:1. In v3, a 75% opacity fade
   on a section label shipped as a 3.59:1 failure that looked perfect to the eye.
2. **A muted border must never be the thing that identifies a control.** The warm
   browns in this palette measure **1.37–2.91:1** against the page — under the
   3:1 non-text minimum. Every control (buttons, the nav pill) is outlined in
   `--ember` at **9.05:1**. Muted `--line` is for decorative dividers only, where
   SC 1.4.11 does not apply.
3. **Light text on dark optically thickens.** Every face is loaded at one regular
   weight, the body line-height is a little open (1.7), and nothing is bold.

### Measured contrast

| Pair | Ratio |
|---|---|
| body text on page | 16.62:1 |
| body text on cards | 14.52:1 |
| muted text on page / on cards | 7.94:1 / 6.94:1 |
| ember on page / on cards | 9.05:1 / 7.91:1 |
| ember-soft on page | 12.41:1 |
| page on ember (button label) | 9.05:1 |
| focus ring on page | 9.05:1 |

Recompute these if you change `--night`, `--crumb`, `--crumb-mute`, or `--ember`.
Do not eyeball them.

## Fonts

The one external dependency, and the only network request the page makes:

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Instrument+Serif&family=Karla:wght@400&family=IBM+Plex+Mono:wght@400&display=swap">
```

**Each family is requested at exactly one weight, and that is load-bearing.**
Asking for a second weight makes Google serve a variable file instead — Karla
alone goes from 13 KB to 24 KB *per weight*. Total as shipped: **48.9 KB**.

**So nothing in this page may set `font-weight`.** Two traps, both already
handled, both of which render as ugly synthetic faux-bold if you undo them:

- `h1, h2, h3` have a UA default of bold — the stylesheet resets them to 400.
- `<strong>` has a UA default of 700. It is explicitly set back to 400 **and**
  restyled onto the mono face, tinted `--ember-soft`.

That `<strong>` treatment is deliberate: it gives emphasis **two** cues, shape
and color, so it does not depend on color alone. It was chosen over mono alone
(too flat to read as emphasis), color alone (one cue), and an ember underline —
the underline looked like a link, which is the last thing an allergy disclaimer
should look like.

It **degrades cleanly** — all three stacks have system fallbacks and
`display=swap` means text is never invisible. **To remove the webfonts:** delete
the `<link rel="stylesheet">` and the two `preconnect` lines above it.

**Privacy note:** requesting the fonts discloses the visitor's IP address, user
agent, and referring page to Google. Ordinary for a small business site, but a
real reason someone might prefer to self-host the three files instead.

## Renaming the bakery

The brand name is the exact, **case-sensitive** string `Ancient Grains`. It
appears **exactly 8 times** in `v4/index.html`:

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

**The counts differ per design: 9 in v1, 8 in v2, 8 in v3, 8 in v4.** Do each
file separately and check each count.

## Placeholders to replace before launch

| Placeholder | What it is | Notes |
|---|---|---|
| `hello@example.com` | Order email | 2 places; the `mailto:` links use the same string |
| `(860) 555-0134` | Phone | 2 places; **also update the `tel:+18605550134` links** (2 places, digits only) |
| `@yourbakeryhandle` | Instagram | The link points at the instagram.com **homepage** — set the real profile URL too |
| `Hartford County, Connecticut` | Pickup area | Also "Hartford County, CT" in the footer |
| `Fridays` | Bake day | Step 3 |
| `Wednesday` | Order deadline | Step 2 |
| `$12` `$10` `$13` `$18` | The four prices | Delete the "prices are placeholders" line at launch |
| **The timeline hours** | 20:00 / 22:30 / 02:00 / 04:30 / 07:00 | **Unique to v4.** These are illustrative, not Will's real schedule. The section says so; replace them with his actual times and delete that caveat. Also update the hero's `Mixed / Baked / On the counter` line, which repeats three of them. |
| Footer cottage-food statement | Legal disclosure | **MUST be verified against current Connecticut Department of Consumer Protection cottage-food requirements before launch.** |
| Both photo slots | Hero + portrait | See below |

The einkorn nutrition claims stay deliberately hedged: v4 states only defensible
facts (age, 100% einkorn, three ingredients) and makes no nutritional claims. If
you add any back, add real citations chosen with Will — never invent them.

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

**Photos for a dark site:** pick shots that are *actually* dim — warm low light,
a dark background, the loaf lit from one side. A bright daylight photo dropped
into this page will glare and break the mood. Slightly underexposed is right.

**Alt text:** describe what is in the picture for someone who cannot see it —
"Will shaping dough at his kitchen bench", not "bakery photo". Use `alt=""` only
if a photo is purely decorative.

**File guidance:** roughly 1000px wide, compressed as `.webp` or quality-80
`.jpg`.

## Publishing

Already published by the same GitHub Pages setup that serves the others — Pages
deploys from `main` at `/ (root)`, and subdirectories are served automatically.
No settings change was needed.

**If v4 ever becomes the site,** move `v4/index.html` to the repo root rather
than pointing Pages at a subfolder.

**Source of truth is this git repo — full stop.** Pull before editing, commit
and push when done.

## Optional hardening for launch

Not needed for a mockup with no forms, but for launch — and it must go **near
the top of `<head>`**, before the favicon and font links, because a CSP
delivered by meta tag only governs resources requested after the parser reaches
it:

```html
<meta http-equiv="Content-Security-Policy"
      content="default-src 'none'; script-src 'unsafe-inline'; style-src 'unsafe-inline' https://fonts.googleapis.com; font-src https://fonts.gstatic.com; img-src 'self' data:; object-src 'none'; base-uri 'none'; form-action 'none'">
<meta name="referrer" content="strict-origin-when-cross-origin">
```

**Not achievable on this host:** `frame-ancestors` and `sandbox` are ignored via
meta tag, and GitHub Pages cannot send custom response headers, so clickjacking
protection would need a CDN in front. Fine for a page with no login, no forms,
and no payments. Subresource Integrity is not viable either — the Google Fonts
endpoint serves different CSS per browser, so no fixed hash matches everyone.

## Known, consciously deferred

- **The FAQ `+`/`−` glyph is CSS generated content**, so Chromium folds it into
  the control's accessible name. Not a WCAG failure, just slightly noisy for
  some screen readers.
- **The headline reflows once on first visit** as Instrument Serif replaces the
  fallback serif. Per-OS metric overrides would be disproportionate here.
- **Verified in Firefox and Chromium, not Safari.**

## Quality status / changelog

**v4.0 — 2026-08-21 — dark, overnight-themed design direction.**

Reviewed by independent code-review and accessibility agents, plus an
instrumented browser pass. Findings resolved:

- `<strong>` inherited the UA default weight of **700** while the mono face is
  loaded at 400 only, so emphasis rendered as synthetic faux-bold. Caught by an
  automated sweep of every element's computed `font-weight` — not by eye.
- **The print stylesheet was badly illegible.** It reset `body` to black on
  white, but every rule that sets `color:` *directly* — links, eyebrows, times,
  prices, captions, the footer, the legal text — kept its dark-theme color on
  white paper: ember at **2.16:1** and muted text at **2.46:1**. Printing or
  saving to PDF is a normal thing to do with a menu. Fixed by overriding the
  color tokens inside `@media print` rather than patching each selector.
- **`.btn` had `white-space: nowrap`.** Measured at 320px, the longest button
  label leaves only **7px** of slack once the WCAG text-spacing override is
  applied. It passed, but a marginally longer label would have overflowed with
  no way to break, so the `nowrap` is gone.
- **The timeline spine overshot the last dot by ~120px** — a bare line trailing
  into empty space at the bottom of the signature section. The spine was one
  element on the `<ol>`, anchored to the list's content bottom, so it ran the
  full height of the final item's text. It is now drawn per item, dot to dot,
  and suppressed on the last one — which makes the overshoot impossible by
  construction rather than by tuning a number.
- **`.baker`'s two-column split beat `.split` only by source order**, both being
  single-class selectors. Reordering the stylesheet would have silently reverted
  the layout with nothing to flag it. Now `.split.baker`.
- Replaced `<cite>` with `figure`/`figcaption` for the pull quote — per the HTML
  spec `<cite>` is the title of a work, not the name of the person quoted.
- The emphasis treatment was chosen by rendering four candidates side by side
  rather than picking one on instinct (see [Fonts](#fonts)).

Playtested in real Firefox at 320px and 1440px: no horizontal overflow at any
width, no interactive target under 24px, all 16 reveal elements firing on a
normal read-through, the scroll-progress line tracking 0→100%, the
JavaScript-disabled path fully visible, and the timeline dots verified to sit on
the spine by measuring both pseudo-elements rather than looking at them. **Every
control border was checked programmatically against its actual backdrop**, and
every loaded font face confirmed to be weight 400.

The site is fully usable with JavaScript disabled — scroll reveal, the header
hairline, and the progress line are progressive enhancement and nothing else
depends on them.

---

*Site designed and built by Jeremy Christman with Claude (Anthropic).*
