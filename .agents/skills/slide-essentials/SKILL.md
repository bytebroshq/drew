---
name: slide-essentials
description: Build zero-dependency, single-file HTML slide decks that work everywhere — laptop, tablet, and iPhone Safari. Use when creating, editing, or converting a presentation/deck/talk. Covers the fixed 16:9 stage, the navigation engine, fullscreen, mobile/iOS support, and composition.
---

# Slide Essentials

Self-contained HTML decks: one file, inline CSS/JS, no npm, no build step, no external assets (fonts via CDN are fine). Everything below is the working engine distilled from real decks — copy `reference/skeleton.html` and fill in slides.

## Non-negotiables

1. **One file.** All CSS/JS inline. No frameworks, no bundler. Fonts via Fontshare/Google Fonts only.
2. **Fixed 16:9 stage.** Author every slide at **1920×1080**. The whole stage scales as one block to the viewport (letter/pillarboxes). Never reflow slide content to fit a device — no responsive breakpoints rearranging slides, no `clamp()` inside the stage.
3. **Switch slides with `visibility`/`opacity`, never `display`.** A later layout rule like `.slide-content { display: flex }` overrides `display:none` and shows every slide at once. Use the `.active`/`.visible` classes.
4. **One idea per slide. Split before you shrink.** If content overflows, add a slide — don't reduce type below comfortable reading size or overlap panels.
5. **Include `prefers-reduced-motion`.** The skeleton already does.

## Start here

Copy [`reference/skeleton.html`](reference/skeleton.html) → rename → edit `:root` theme vars, swap the fonts, author slides inside `.deck-stage`. The skeleton ships with two example slides and the full engine wired up. Keep the `<head>` meta block intact — it carries the mobile behavior.

## The engine (what each part does)

A single `SlidePresentation` class wires scaling + every input surface. Each `setup*` method **self-gates to the device it targets** via capability checks, so the same file is correct on laptop, tablet, and iPhone with zero user-agent sniffing.

| Method | Job | Gate |
| --- | --- | --- |
| `setupStageScale` | Scale 1920×1080 → viewport | Uses `visualViewport` when present (tracks iOS toolbar collapse; `resize` lies there) |
| `setupKeyboardNav` | ←/→/Space/Home/End, `F` fullscreen | — |
| `setupMouseWheel` | Wheel = prev/next (600ms lock) | — |
| `setupTouchNav` | **Tap** to advance (left quarter = back) | Stationary tap only (>12px move = ignored), skips taps on controls |
| `setupFsHint` | Idle-reveal fullscreen button | Removed where `requestFullscreen` is undefined (iPhone) |
| `setupTapHints` | Idle-reveal ‹ › edge chevrons | `pointer: coarse` only |
| `setupRotateNudge` | One-time "rotate to landscape" overlay | Phones only (short edge ≤480px) + portrait |
| `setupIosRoom` | Adds `.ios-room` for the scroll hack | `pointer: coarse` **and** no Fullscreen API |

### Capability gates (the device map)

- **iPhone Safari** = `matchMedia('(pointer: coarse)').matches` **and** `!document.documentElement.requestFullscreen`. iPhone Safari is the only mainstream target with no Fullscreen API, so its absence *is* the iPhone signal. (iPad has it.)
- **Phone vs tablet** = short edge `Math.min(innerWidth, innerHeight) <= 480`.
- Always feature-detect, never sniff the UA string.

## Fullscreen

- `F` toggles `requestFullscreen`/`exitFullscreen`. The toggle no-ops where the API is missing, so it's safe to call anywhere.
- The **fullscreen helper** is an idle-reveal button (appears after ~3s of no input, hides on activity and in fullscreen). It removes itself on iPhone — never show a dead button.

## Mobile / iOS support

iPhone Safari can't go truly fullscreen without Add-to-Home-Screen. The deck gets as close as possible **without installation**:

- **Scroll-to-minimize (`.ios-room` + `.ios-spacer`).** iOS only collapses its toolbars on a real scroll — *not* on rotate, *not* via `scrollTo`, *not* via `100dvh`. So on iPhone Safari we make the document scrollable by exactly the toolbar height with a `height: 100lvh` spacer (`lvh` = large-viewport height, toolbar-collapsed max). One swipe hides the chrome; the fixed `.deck-viewport` stays put on top. `visualViewport` rescales the stage into the reclaimed space.
- **Tap, not swipe.** With scroll-room active a horizontal swipe fights the collapse gesture, so navigation is tap-to-advance. Left quarter = back, rest = forward. Drags (>12px) and taps on controls are ignored.
- **Idle-reveal tap chevrons** make tap nav discoverable on touch.
- **Rotate nudge** (portrait phones only) — landscape gives the 16:9 stage far more area.
- **Add-to-Home-Screen meta** (`apple-mobile-web-app-capable`, status-bar `black-translucent`, `theme-color` = darkest bg, `viewport-fit=cover`) gives the chrome-free path for anyone who installs, and makes the status bar blend in.

When editing the deck's dark background, **keep `theme-color` in sync** with it.

## Composition (don't make AI slop)

- **Distinctive type.** No Inter/Roboto/Arial/system. Pick faces with character; commit to a display + mono pair.
- **Committed palette.** CSS variables, dominant color with sharp accents — not timid evenly-spread color. Vary light/dark per deck.
- **Atmosphere over flat fills.** Layered gradients, geometric patterns, subtle texture beats a solid background.
- **One orchestrated load.** Staggered reveals (`.reveal` + `data-d="1..N"` delays) on slide-in create more delight than scattered micro-interactions.
- **Density: pick one.** *Speaker-led* = big type, 1–3 bullets, more slides. *Reading-first* = self-contained grids/tables, 4–8 bullets, tighter but never cramped. If mixed, pick the closer mode; never invent a middle.

## When editing an existing deck (highest-risk failures)

1. Count elements against the density before adding — overflow is the #1 bug.
2. Adding text/images that won't fit → split into another slide, don't shrink.
3. After **any** change, verify the stage stays 16:9 with no overflow/overlap at 1280×720 **and** one phone viewport.
4. Never switch slides with `display` (see non-negotiable #3).

## Delivery

- **Open:** `open <deck>.html`.
- **Deploy (drew):** static hosting via Cloudflare Workers — `npx wrangler deploy`. `decks/` serves at root; `decks/index.html` lists decks. (No Worker script.)
- **PDF export:** `bash scripts/export-pdf.sh <deck>.html [out.pdf]` — headless screenshots each `.slide` at 1920×1080 into a PDF (no animation). Add `--compact` for smaller files. Needs Playwright (auto-installs).
- **PPTX → web:** `python scripts/extract-pptx.py <in.pptx> <out_dir>` pulls text/images/notes; then build slides from that content.

## Files

| Path | What |
| --- | --- |
| [`reference/skeleton.html`](reference/skeleton.html) | Copy-paste starter — full engine + mobile support + 2 example slides |
| [`scripts/export-pdf.sh`](scripts/export-pdf.sh) | HTML → PDF via headless Chromium |
| [`scripts/extract-pptx.py`](scripts/extract-pptx.py) | PPTX → text/images/notes |
