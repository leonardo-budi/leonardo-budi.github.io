# FIGMA_PRODUCTION_GUIDE

The single source of truth for every Figma-side production decision that applies across the whole portfolio: artboard sizes, export settings, naming, spacing, and reusable components. This document exists so that individual creative briefs don't have to repeat the same rules 48 times. A brief should only ever document what's unique to that one asset, everything reusable lives here.

**How the documents divide up:**
- `IMAGE_STYLE_GUIDE.md` is the *visual design system*: why the portfolio's images should look the way they do (no shadows, flat-on perspective, the Rail/Gallery distinction, color treatment, annotation philosophy). Read it for the reasoning.
- `FIGMA_PRODUCTION_GUIDE.md` (this document) is the *production system*: the concrete Figma artboard sizes, export settings, file structure, and reusable components that implement that reasoning. Read it for the numbers.
- `IMAGE_ASSETS.md` is the *checklist*: every asset, its status, and its priority.
- Each individual creative brief (for example the Currency Exchange hero brief) only covers what's specific to that one image: narrative purpose, required UI, cropping, hierarchy, composition, annotations, filename. It should reference this document rather than restate it.

If a future brief needs a production rule that isn't here yet, add it here first, then reference it, don't let it live only inside one brief.

---

## 1. Approved production ratios (the canonical system, read this first)

**Revised 2026-07-03.** The portfolio now standardizes on a small, fixed set of production ratios, chosen independently of any single page's HTML. This replaces the earlier "frame type" system below, which had one real flaw: Gallery phone's spec (393:852, 786x1704) was derived directly from a CSS placeholder value already sitting in the HTML, not chosen as a deliberate production ratio. Going forward, **the HTML adapts to the production asset, not the other way around.** Every new asset (Account Hub, Aryaduta, and any future page) is built to one of the five ratios below; the corresponding CSS `aspect-ratio` is set to match once real assets are wired in, not the reverse.

| Ratio name | Ratio | Recommended artboard / export size | Used for |
|---|---|---|---|
| **Landscape Showcase** | 16:9 | 2400 x 1350px | Hero, Context, Challenge, Landscape, Exploration, Solution, Final Design, Comparison, editorial showcase. Covers every Rail hero/section shot and every Gallery lead/wide shot. |
| **Portfolio Card** | 3:2 | 2400 x 1600px | Homepage cards, More Work / Related Projects cross-link cards, any future portfolio listing. |
| **Portrait Device Showcase** | 9:16 | 1350 x 2400px | Any slot where a single mobile device is the primary subject. **Supersedes the old Gallery phone spec (393:852, 786x1704).** |
| **Editorial Portrait** (optional) | 3:4 | 1800 x 2400px | Only when a composition genuinely benefits from a more editorial portrait frame than a bare device screen. Not the default; prefer Portrait Device Showcase (9:16) unless there's a specific reason to deviate (see section 1a). |
| **Motion** | 16:9 (MP4) | 2400 x 1350px | Interaction demos, walkthroughs, complete flows, before/after interactions, animated showcases. **Exception**: when the video's primary subject is a single mobile device (portrait), export at Portrait Device Showcase's ratio (9:16, 1350x2400) instead of forcing a landscape canvas, see section 1a. |

**Mapping from the old CSS-class-based frame types to the new system**, so existing pages and new blueprints speak the same language:

| Old frame type | CSS class | Old spec | New spec |
|---|---|---|---|
| Rail hero | `.shot-frame.ts-hero` | 16:9, 2400x1350 | **Landscape Showcase** (unchanged) |
| Rail section | `.shot-frame.ts-sec` (incl. `.ts-alt`) | 16:9, 2400x1350 | **Landscape Showcase** (unchanged) |
| Gallery lead | `.shot-frame.lead` | 16:9, 2400x1350 | **Landscape Showcase** (unchanged) |
| Gallery wide | `.shot-frame.wide` | 16:9, 2400x1350 | **Landscape Showcase** (unchanged) |
| Gallery phone | `.shot-frame.phone` | 393:852, 786x1704 | **Portrait Device Showcase, 9:16, 1350x2400** (**changed**, see below) |
| Card / cross-link thumbnail | `.pip`, `.exp-img`, `.more-img` | 3:2, 2400x1600 | **Portfolio Card** (unchanged) |
| About portrait | `.about-img-placeholder` | 4:3, 2400x1800 | **Not part of this system.** Already real and shipped (inline base64), predates this ratio standardization, and is out of scope for this revision. Left as-is; not retroactively migrated. |

**What actually changes**: only Gallery phone. Every other existing frame type already matched one of the five approved ratios, this was mostly a matter of naming the system explicitly rather than reshaping it. Gallery phone moves from 393:852 (the literal device-pixel ratio of a modern phone screen, which happened to already be sitting in the placeholder CSS) to the cleaner, rounder 9:16. **This is a genuine ratio change**, not just a relabeling: 393:852 ≈ 0.4613 width-to-height, while 9:16 = 0.5625, a visibly wider crop. Any Gallery phone asset already scoped against the old 393:852/786x1704 spec (see `docs/blueprints/account-hub.md` and `docs/blueprints/aryaduta.md` before their 2026-07-03 revision) needs to be re-scoped to 9:16/1350x2400. Both blueprints have been updated to reflect this.

**HTML consequence, not yet made**: `.shot-frame.phone`'s CSS (`aspect-ratio: 393 / 852`) in both `visual-lab/account-hub/index.html` and `visual-lab/aryaduta/index.html` will need updating to `aspect-ratio: 9 / 16` once real assets are produced and wiring begins. This is a deliberate, tracked follow-up, not an oversight, no HTML has been touched as part of this documentation revision.

### 1a. When to deviate from the default ratio (explain first, don't assume)

Two judgment calls worth stating explicitly rather than leaving implicit:

- **Editorial Portrait (3:4) vs. Portrait Device Showcase (9:16)**: reviewed every current Gallery phone slot on both Account Hub and Aryaduta for a case that would benefit from the more editorial 3:4 frame (typically: a device shown with light environmental context, rather than a bare edge-to-edge screen capture). **Found none.** Every phone slot on both pages is a pure UI screen capture, no environmental/lifestyle framing anywhere in either page's copy or existing composition notes. Portrait Device Showcase (9:16) is recommended for every phone slot on both pages; Editorial Portrait remains available for a future page that genuinely calls for it, but isn't invoked here.
- **Motion's default 16:9 vs. Portrait Device Showcase (9:16) for phone-subject video**: the Motion category's default recommendation is 16:9, matching the site's existing MP4 precedents (Currency Exchange's CE-09, Toko Mama's TM-03/TM-05), all of which show landscape-context flows. But if a future motion asset's primary subject is a single portrait phone screen (the one live candidate is Account Hub's AH-03, see `docs/blueprints/account-hub.md`), forcing that recording into a 16:9 canvas would mean padding a portrait screen inside a landscape mat, breaking Gallery's established "flat mat, real screen aspect" philosophy the same way the old 393:852 spec was trying to preserve. In that specific case, export at 9:16 (1350x2400) instead of the Motion default, treating it as a Portrait Device Showcase asset that happens to be MP4 rather than JPG. This is the only documented exception to Motion's default ratio.

## 2. Export aspect ratios (locked, do not deviate)

These are fixed in the live CSS via `aspect-ratio` plus `object-fit: cover`, so a wrong-ratio export gets cropped unpredictably by the browser rather than rejected outright, making this an easy mistake to ship without checking. Always design at the exact ratio, never "close enough."

- **16:9 (Landscape Showcase)**: Rail hero, Rail section, Gallery lead, Gallery wide, and any Motion asset whose subject isn't a single portrait device.
- **9:16 (Portrait Device Showcase)**: Gallery phone. **Supersedes the old 393:852 spec.** Also used for any Motion asset whose primary subject is a single portrait mobile device (see section 1a).
- **3:2 (Portfolio Card)**: Homepage project/exploration cards, all cross-link "more work" cards.
- **3:4 (Editorial Portrait)**: optional, not currently used anywhere in the site; available if a future composition genuinely benefits from it over 9:16.
- **4:3**: About portrait only. Predates this ratio system, not part of it, left as-is.

## 3. Export resolution and the 2x strategy

Export everything at **2x the maximum real in-page display size**, for retina sharpness on the displays this audience actually uses (European hiring managers on current professional hardware, `IMAGE_STYLE_GUIDE.md` section 15).

| Frame type | Max real display width (CSS-derived) | Export size |
|---|---|---|
| Landscape Showcase (Rail hero/section) | ~1200-1300px in-page (`.case-shot` margin against `--maxw: 1440px`); 1000px max in the lightbox | **2400 x 1350px** |
| Landscape Showcase (Gallery lead/wide) | 1080px max in the lightbox (`width: min(92vw, 1080px)`) | **2400 x 1350px** (rounds up generously, gives headroom) |
| Portrait Device Showcase (Gallery phone) | 240px in the filmstrip (200px mobile); up to 720px tall in the lightbox | **1350 x 2400px** (standardized production ratio, 9:16, not derived from the filmstrip's own current display size, see section 1) |
| Portfolio Card | Roughly 600-700px wide at desktop card width | **2400 x 1600px** (generous headroom since cards also reappear at varying widths across breakpoints) |
| Editorial Portrait (optional, not currently used) | N/A, no live slot yet | **1800 x 2400px** |
| Motion (16:9 default) | Same real display context as its Landscape Showcase equivalent | **2400 x 1350px** |
| Motion (portrait-device exception, see section 1a) | Same real display context as Portrait Device Showcase | **1350 x 2400px** |
| About portrait (predates this system) | Roughly 600px wide in the two-column About grid | **2400 x 1800px** |

Export everything at one consistent 2x multiple, don't mix 1.5x or 3x across assets. If a specific image needs more headroom (for example a screenshot with fine text that must stay sharp when lightboxed), go up to 2x of the artboard above rather than inventing a one-off multiplier, keep the underlying ratio identical either way. **Do not derive a new export size from a page's current placeholder CSS.** Every export size should trace back to one of the five approved ratios in section 1, not to whatever dimension happens to already be sitting in the HTML, that derivation is exactly what produced the now-superseded 393:852 spec.

## 4. Naming conventions

Already established in `PROJECT_STRUCTURE.md` and `IMAGE_ASSETS.md`, restated here as the production-facing version:

- All lowercase, hyphen-separated. In-page case-study assets use asset-ID prefix: `<id>-<description>.ext`, for example `ce-01-hero.jpg`, `ce-04-challenge.jpg`. Site-wide assets (card thumbnails, about portrait) keep the project prefix: `<project>-<description>.ext`, for example `currency-exchange-card.jpg`, `aryaduta-staff-incoming.jpg`.
- One file per unique image. If two slots share an image (confirmed case: every homepage card = its cross-link "more work" thumbnails), name the file after its primary/first appearance and reference that same file from the second slot. Never duplicate the file under two names.
- Card thumbnails that get reused across pages live under `assets/images/cards/<project>-card.jpg`, not inside any individual project's own `assets/` folder, since they're genuinely site-wide (`PROJECT_STRUCTURE.md`'s root-vs-per-project `assets/` distinction).
- Every other in-page image lives in its own project's folder: `study-case/<project>/assets/` or `visual-lab/<project>/assets/`.
- Use the exact filenames already assigned in `IMAGE_ASSETS.md` for each slot. If a brief needs a new filename not yet in that document, add it there at the same time, don't let the two documents drift.

## 5. Folder structure (where exports land)

```
/assets/images/cards/                          5 reusable homepage card thumbnails (3:2)
/assets/images/about-leo-portrait.jpg          About portrait (4:3, already real, needs extraction)
/study-case/currency-exchange/assets/          9 unique files
/study-case/toko-mama/assets/                  5 unique files (3 JPG, 2 MP4, revised 2026-07-01)
/study-case/mybca/assets/                      3 unique files
/visual-lab/account-hub/assets/                7 unique files
/visual-lab/aryaduta/assets/                   22 unique files
```

This matches the folder architecture already locked in `PROJECT_STRUCTURE.md`. No new top-level folders, no build step, every export is a plain file referenced by a plain `<img src>` once wiring begins.

## 6. Export formats (WebP / JPG / PNG)

Per `IMAGE_STYLE_GUIDE.md` section 15, recommended and pending final confirmation:

- **WebP** for all screenshots and composed slides (the large majority of assets): better compression-to-quality ratio than JPEG for UI content (flat color areas, sharp text edges), and supported in every evergreen browser this audience uses. Quality ~80-85 as a starting point.
- **JPEG** for the About portrait and any future real photography: photographic images don't get as large a size win from WebP, and the portrait is already a JPEG today.
- **PNG** only if a specific asset genuinely needs transparency or lossless flat color (favicon, Open Graph image if it ever needs a transparent variant). None of the 48 outstanding case-study assets need this.
- If WebP isn't confirmed by the time production starts, JPEG (quality ~85-90) is the fallback, not PNG, PNG is oversized for photographic/screenshot content and should stay reserved for the transparency case.
- **MP4, now a first-class production format alongside JPG, not a one-off exception.** Originally introduced for Currency Exchange's CE-09 (`ce-09-full-transaction-flow.mp4`, see `docs/blueprints/currency-exchange.md`) as a single confirmed case. Toko Mama's revised plan (`docs/blueprints/toko-mama.md`, 2026-07-01) uses it for two of its five assets (TM-03 Friction, TM-05 Outcome), demonstrating both the original problem and the completed interaction as real recorded sequences rather than static composites. Any asset whose caption or surrounding copy describes a multi-step flow, a before/after interaction, or a demonstrated behavior (not just a resolved static screen) is a candidate for MP4 over a static composite. Playback treatment is locked from CE-09's precedent: native `<video controls playsinline preload="metadata">`, never the `.shot-frame`/lightbox system, since native controls already provide the play/pause/seek interaction a lightbox would otherwise add. **Performance discipline carries over**: CE-09 shipped at 49MB and was flagged as too heavy; every future video asset should be produced with a compression pass and a tight trim in mind from the start, not exported at maximum quality and fixed later.

## 7. Margins and spacing rules

Two different spacing systems, by template, both already established in `IMAGE_STYLE_GUIDE.md`:

- **Rail (composed slides)**: the screen content occupies roughly **78-85% of the artboard height**, centered on both axes, with the remainder split evenly as dark backdrop above and below. Width follows naturally from the screen's own aspect ratio, most of a 2400px-wide canvas stays empty backdrop by design (see the Currency Exchange hero brief for a worked example).
- **Gallery (matted screens)**: the screen capture sits inset within its frame on a flat dark mat, inset amount calibrated by frame type (decided 2026-06-30, see `IMAGE_STYLE_GUIDE.md` section 4):
  - **Phone frames**: light inset, **~4-6% margin** on all sides.
  - **Lead/wide frames**: generous inset, **~8-12% margin** on all sides.
  - Center the screen within the mat on both axes. Build the mat directly into the exported image canvas (don't rely on a future CSS change), this keeps every export self-contained and matches the no-build architecture.
- Keep whichever spacing rule applies **identical across every asset of that frame type**, on every page. A reader moving between Currency Exchange, Toko Mama, and myBCA, or between Account Hub and Aryaduta, should feel one continuous system, not per-page variation.

## 8. Background treatments

- **Rail backdrop**: each Rail page has its own locked placeholder gradient already in the live CSS, use it as the literal backdrop color so the real image sits exactly where the current placeholder does:
  - Currency Exchange & Toko Mama, `.ts-sec`: `linear-gradient(135deg, #0d1f05, #1a3a08, #0a100a)`. `.ts-hero`: `linear-gradient(135deg, #051a08, #0a3010, #060f07)`. Shared `.ts-alt`: `linear-gradient(135deg, #1a1208, #3a2410, #0f0a06)`.
  - myBCA, all three: blue family, `.ts-hero`: `linear-gradient(135deg, #04132e, #0a3a6b, #050d1c)`. `.ts-sec`: `linear-gradient(135deg, #06182f, #0c3a66, #050f1e)`. `.ts-alt`: `linear-gradient(135deg, #0a2747, #14528c, #07182b)`.
  - **Only the hero variant** gets the two faint decorative radial highlights (circle at 30%/30%, lime at 8% opacity; circle at 75%/70%, lime at 4% opacity). Section shots stay flat, no glow. This is a real, deliberate hero-vs-section distinction, don't apply the glow everywhere.
- **Gallery mat**: flat `--bg-card` fill (`#111111`), no gradient, no texture, identical across both Gallery pages and every frame type.
- **No contextual photography backgrounds anywhere** (desks, hands, devices in environments). The only genuinely environmental/contextual image in the whole site is the About portrait, a different category entirely (a real person, not a product).

## 9. Screenshot inset rules

Consolidating section 7 into one explicit rule per frame type, since this is the most consequential single number in any given brief:

| Frame type | Inset | Reasoning |
|---|---|---|
| Landscape Showcase (Rail hero/section) | Screen at 78-85% of artboard height, backdrop fills the rest | Composed slide convention, see `IMAGE_STYLE_GUIDE.md` section 3 |
| Portrait Device Showcase (Gallery phone, 9:16) | ~4-6% margin, mat-filled | Legibility-sensitive, smallest display size in the portfolio (240px in filmstrip). Inset percentage is unaffected by the 393:852→9:16 ratio change, only the canvas proportions changed, not the mat rule. |
| Landscape Showcase (Gallery lead/wide) | ~8-12% margin, mat-filled | Lower information density, larger display size, room for editorial rhythm |
| Portfolio Card (3:2) | Edge-to-edge, no mat | These are cropped detail shots of a larger hero/slide image, not separately composed, no inset rule applies |
| About portrait (4:3) | Edge-to-edge, real photograph | Already real, `object-fit: cover; object-position: center 35%` handles framing in CSS |

## 10. Reusable Figma components

Build these once as Figma components/styles and reuse across every brief, rather than rebuilding per asset:

- **Rail slide backdrop component**: a 2400x1350px frame with the locked gradient fills from section 8, one variant per page (Currency Exchange/Toko Mama shared, myBCA separate), plus a hero variant with the two radial highlights. Every Rail in-page shot starts from this component.
- **Gallery mat component**: a frame at each Gallery ratio (16:9 lead/wide, **9:16 phone**, superseding the old 393:852 spec) filled with `#111111`, with an inner content area pre-inset at the locked percentage (4-6% phone, 8-12% lead/wide) where the screen capture gets placed. Build two variants, one per inset percentage, reuse across both Gallery pages.
- **Caption/label style** (if any in-image annotation is used): Inter, neutral white/gray, thin hairline connector lines, never the lime accent (`IMAGE_STYLE_GUIDE.md` section 10). Only needed for the two flagged annotated slots (Currency Exchange Challenge section, myBCA toggle).
- **Color styles**: register the Rail gradients (section 8), the Gallery mat fill, and `--bg`/`--bg-card`/`--border`/`--accent` from `DESIGN_DECISIONS.md` as Figma color styles once, so every artboard pulls from the same swatches instead of re-entering hex values per file.

## 11. Other reusable production decisions

- **No box-shadow, no border-radius baked into any export.** Confirmed nowhere in the live CSS does any image carry its own shadow; Rail frames are sharp-cornered, Gallery frames get their rounding from CSS (`border-radius` on `.shot-frame`), not from the image content. Don't round corners inside the exported file itself, even for Gallery, the CSS already does it.
- **Flat, front-on perspective only.** No device tilt, no 3D rotation, anywhere in the portfolio. Confirmed by the absence of any perspective transform in the CSS.
- **Screenshots keep each product's real UI colors.** Never re-tint or desaturate toward the site's lime-on-black palette. The lime accent (`#C8F135`) must never appear inside exported image content, full stop, it exists only as a CSS hover state.
- **Reuse, don't re-export.** Any image referenced from more than one slot (homepage cards on cross-link rows, Currency Exchange hero/Final Design) is one file, produced once. Check `IMAGE_ASSETS.md`'s "Dependencies" column before starting a new asset, in case it's already covered by an earlier one.
- **Rest-state UI only.** No open keyboards, no loading spinners, no error toasts mid-animation, unless the caption explicitly calls for that state (for example myBCA's insufficient-balance error, which is a deliberate exception). Default to the calm, resolved version of any screen.

---

## How to use this with a creative brief

Each future brief (Toko Mama hero, myBCA toggle, Account Hub lead, every Aryaduta phone screen, and so on) should reference this document by section number rather than restate it, and contain only:

1. **Narrative purpose**: why this image exists, tied to the copy around it.
2. **Required UI**: exactly what must be visible, sourced from the page's own copy.
3. **Cropping**: what's excluded (status bars, keyboards, nav chrome), specific to this screen.
4. **Visual hierarchy**: order of attention, specific to this image's content.
5. **Composition**: which `FIGMA_PRODUCTION_GUIDE.md` frame type and inset rule applies (a one-line reference, for example "Rail section, see sections 1, 3, 7, 8").
6. **Annotations**: yes/no, and if yes, what specifically gets marked (most slots: no).
7. **Filename**: the exact path from `IMAGE_ASSETS.md`.

A brief that re-explains artboard sizes, export resolution, or mat percentages is duplicating this document and should be trimmed back to a reference instead.
