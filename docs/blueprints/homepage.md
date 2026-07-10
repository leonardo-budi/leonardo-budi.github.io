# HOMEPAGE — PRODUCTION BLUEPRINT

The complete production checklist for every media asset on `index.html`. Built by inspecting the entire page (a single self-contained file, no separate HTML partials, matching the site's no-build architecture) against `IMAGE_STYLE_GUIDE.md`, `FIGMA_PRODUCTION_GUIDE.md`, `IMAGE_ASSETS.md`, and `MASTER_ASSET_TRACKER.md`.

Fourth blueprint of the set, following the structure established in `docs/blueprints/currency-exchange.md`, `docs/blueprints/mybca.md`, and `docs/blueprints/toko-mama.md`. No HTML modified, no redesign, no images generated, blueprint only.

**This blueprint is fundamentally different from the three case-study blueprints that came before it**: the homepage's job is almost entirely to *reuse* production assets that already exist, not commission new photography. Four of six visible media slots can be sourced from Currency Exchange, Toko Mama, and myBCA's own delivered heroes, since all three are now fully produced (`MASTER_ASSET_TRACKER.md` confirms 17/17 implemented). Only the About portrait (already real) and two `<head>`-level assets (favicon, OG image) need anything close to original production.

---

## Production status

**Not started.** All 6 visible media slots are still CSS gradient placeholders except the About portrait, which is a real photo but embedded as inline base64 rather than a proper file. Favicon and OG image don't exist at all (no `<link rel="icon">` or `<meta property="og:image">` tags anywhere in `<head>`), confirming `IMAGE_ASSETS.md`'s "Known gaps" finding.

---

## Before you start: what the homepage actually needs, and what it doesn't

Read top to bottom, the homepage has exactly **6 visible media slots** in the DOM:

1. **Hero background** (`.hero-bg`) — **not a content image slot.** Checked directly: it's a CSS `radial-gradient` + `linear-gradient` combination, decorative art with no image dependency. Confirmed by `IMAGE_ASSETS.md`'s prior audit and reconfirmed here. Not listed as an HP item below.
2. **About portrait** (`.about-img-placeholder`) — real, already live, inline base64 JPEG.
3-5. **Selected Work cards** (`.pip-currency`, `.pip-pos`, `.pip-mybca`) — 3 project-card thumbnails, currently CSS gradients.
6-7. **Other Explorations cards** (`.exp-img-accounthub`, `.exp-img-aryaduta`) — 2 exploration-card thumbnails, currently CSS gradients.

Beyond the DOM, two more media assets are needed but live in `<head>`, not the visible page: **favicon** and **OG image**. Neither exists yet. This blueprint numbers them HP-07 and HP-08 for completeness, since "every media asset used on the Homepage" reasonably includes what search engines and browser tabs show, even though neither has a `.shot-frame`-equivalent slot to inspect.

**The core production question for this page isn't "what do we shoot," it's "what do we reuse."** Three of the five placeholder card slots (Currency Exchange, Toko Mama, myBCA) can be sourced from hero images that already exist and are already verified in production. The other two (Account Hub, Aryaduta) can't be resolved yet, those pages have no blueprint and no assets of their own to reuse from.

**Shared constants for the 5 card-type slots** (3 Selected Work + 2 Other Explorations, all `.pip`/`.exp-img`, confirmed identical `aspect-ratio: 3/2` in CSS):

- **Aspect ratio**: 3:2
- **Figma artboard**: 2400 x 1600px (`FIGMA_PRODUCTION_GUIDE.md` section 1)
- **Export size**: 2400 x 1600px
- **Export format**: JPG
- **Corner radius**: none in CSS for `.pip`/`.exp-img` themselves (any rounding is on the parent card container, not the image)

---

## HP-01 — About Portrait

**Section**: `.about` (`#about`), `.about-img-wrap` / `.about-img-placeholder`.
**Purpose**: Establish a real person behind the work. The only human photograph anywhere on the site.
**Status**: **Already real and live.** A base64-encoded JPEG is inline in the `src` attribute today (confirmed: `alt="Leonardo Budi"`, the base64 payload alone is ~137KB of the page's HTML, source image is 712x1067px per prior documentation).

**Media type**: JPG.
**Aspect ratio**: 4:3 (locked via CSS `.about-img-placeholder { aspect-ratio: 4/3; object-fit: cover; object-position: center 35%; }`).
**Figma artboard**: Not applicable, this isn't a Figma composition, it's a photograph.
**Export size**: 2400 x 1800px recommended (`FIGMA_PRODUCTION_GUIDE.md` section 3), 2x of the ~600px max in-page display width. Source is only 712x1067 natively, upscaling to 2400x1800 would degrade quality; more realistic is to export at the source's own resolution (712x1067, already close to 4:3 at 0.667 vs the target 0.75, will need the same `center 35%`-equivalent crop) or request a higher-resolution original from Leo if one exists outside what's currently embedded.

**Reused from another case study?** No, this is homepage-original and does not appear anywhere else in the site.
**Source filename (if reused)**: Not applicable.
**Crop strategy**: Already resolved in CSS (`object-fit: cover; object-position: center 35%`), no new crop decision needed, just extract the existing base64 payload to a real file at its native crop.
**Focal point**: Face/upper body, already weighted toward the top of frame via `35%` vertical object-position.
**Responsive behavior**: Single `<img>`, CSS `aspect-ratio: 4/3` holds across breakpoints (confirmed `@media (max-width:768px)` still applies `aspect-ratio: 4/3` explicitly).

**Dependencies**: None. Pure technical cleanup: decode the base64 payload, save as `assets/images/about-leo-portrait.jpg`, replace the `src` with a normal file path, keep the existing `alt="Leonardo Budi"`. This is the one item on this page that is genuinely **not** a production task, it's an extraction task.

**Priority**: Medium. Doesn't block anything visually (it already renders correctly today), but the ~137KB of inline base64 is bloating the page's HTML payload by roughly a third and should be resolved before any performance pass.

---
↓
---

## HP-02 — Currency Exchange Card

**Section**: `.work` (`#work`), first `.project-card.featured`, `.pip.pip-currency`.
**Purpose**: Featured project-card thumbnail. The first case-study visual any homepage visitor sees, above the fold on most viewports.

**Media type**: JPG.
**Aspect ratio**: 3:2.
**Figma artboard**: 2400 x 1600px.
**Export size**: 2400 x 1600px.

**Reused from another case study?** **Yes.** Currency Exchange's own hero shot, `ce-01-hero.jpg`, already produced and verified (`MASTER_ASSET_TRACKER.md`: CE-01 implemented, pending only an art-direction review unrelated to this reuse).
**Source filename**: `study-case/currency-exchange/assets/ce-01-hero.jpg` (2400x1350, 16:9).
**Dedicated homepage crop needed?** **Yes.** The source is 16:9 (1.778 ratio), the card needs 3:2 (1.5 ratio), these are different shapes, not just different sizes. **Do not pixel-crop the flattened delivered JPG** (it's only 1350px tall; cropping to a taller 3:2 frame from a 16:9 source means narrowing the width, which is fine, but the delivered file's own height is already the ceiling, there's no room to crop taller without upscaling). The correct approach: re-export directly from CE-01's original Figma composition at a new 2400x1600 3:2 artboard, keeping the same phone-centered composed-slide treatment and backdrop, just on a taller canvas. This preserves full resolution and visual quality, and is a small incremental job since the composition, backdrop gradient, and phone content all already exist.

**Crop strategy**: Center the same phone composition horizontally, same as CE-01; the extra vertical room in the 3:2 canvas (versus 16:9) should extend the backdrop gradient above and below, not shrink the phone.
**Focal point**: The phone screen, centered, matching CE-01's own focal point exactly.
**Responsive behavior**: `.pip` holds `aspect-ratio: 3/2` at every breakpoint (no responsive override found in the CSS's `@media` blocks for `.pip` itself).

**Dependencies**: None beyond CE-01 already existing, which it does.
**Reuse elsewhere**: This same card file is also the source for the "more work" cross-link thumbnail reused on Toko Mama's, myBCA's, and Account Hub's pages (`IMAGE_ASSETS.md`, confirmed 3 reuse sites), so this single 3:2 export serves four locations total once produced.
**Priority**: **Highest.** Featured card, first case study seen, reused in the most places.

---
↓
---

## HP-03 — Toko Mama Card

**Section**: `.work` (`#work`), second `.project-card`, `.pip.pip-pos`.
**Purpose**: Project-card thumbnail for the Toko Mama case study.

**Media type**: JPG.
**Aspect ratio**: 3:2.
**Figma artboard**: 2400 x 1600px.
**Export size**: 2400 x 1600px.

**Reused from another case study?** **Yes.** `docs/blueprints/toko-mama.md` already flagged both TM-01 (Hero) and TM-04 (Solution) as candidates for this exact reuse, recommending "TM-01 is the strongest candidate... since it's the single most representative shot of the product," and left both exported with extra crop headroom specifically anticipating this decision. **This blueprint resolves that open question: use TM-01 (Hero).** Reasoning: TM-01 establishes the product in its normal working state (a busy tablet POS), which reads as a stronger single-glance thumbnail than TM-04's tab-switching detail, which needs the surrounding case-study narrative to make sense at a glance. TM-04 remains a fallback candidate if TM-01's crop doesn't read well at card size once actually produced.
**Source filename**: `study-case/toko-mama/assets/tm-01-hero.jpg` (2400x1350, 16:9).
**Dedicated homepage crop needed?** **Yes**, same reasoning as HP-02: re-export from TM-01's original Figma composition at a 2400x1600 3:2 artboard, don't pixel-crop the flattened JPG. Both TM-01 and TM-04 were deliberately exported with extra breathing room around the tablet for exactly this reason (`docs/blueprints/toko-mama.md`: "export with the tablet screen slightly smaller within the frame... so a 3:2 crop can be pulled from the composition later"), so this should be a low-effort re-export, not a from-scratch rebuild.

**Crop strategy**: Center the tablet composition horizontally; extend backdrop vertically for the taller 3:2 canvas, matching HP-02's approach.
**Focal point**: The tablet screen, centered.
**Responsive behavior**: Same as HP-02, `.pip` holds 3:2 at every breakpoint.

**Dependencies**: None, TM-01 already exists and was produced with this reuse in mind.
**Reuse elsewhere**: Same file reused on Currency Exchange's, myBCA's, and Account Hub's "more work" cross-link cards (3 reuse sites, per `IMAGE_ASSETS.md`).
**Priority**: High.

---
↓
---

## HP-04 — myBCA Card

**Section**: `.work` (`#work`), third `.project-card`, `.pip.pip-mybca`.
**Purpose**: Project-card thumbnail for the myBCA case study.

**Media type**: JPG.
**Aspect ratio**: 3:2.
**Figma artboard**: 2400 x 1600px.
**Export size**: 2400 x 1600px.

**Reused from another case study?** **Yes.** myBCA's hero shot, `mb-01-hero.jpg`, already produced and verified.
**Source filename**: `study-case/mybca/assets/mb-01-hero.jpg` (2400x1350, 16:9).
**Dedicated homepage crop needed?** **Yes**, same reasoning as HP-02/HP-03: re-export from MB-01's Figma composition at 2400x1600, don't pixel-crop the flattened JPG. Unlike Toko Mama, myBCA's blueprint didn't explicitly flag extra crop headroom on MB-01 in advance, worth double-checking the safe-area margins hold once this crop is actually attempted, per `docs/blueprints/mybca.md`'s MB-01 entry (central 65% safe area, minimum 5% clear margin).

**Crop strategy**: Center the phone composition horizontally, extend backdrop vertically.
**Focal point**: The phone screen (the no-balance transfer screen), centered.
**Responsive behavior**: Same as HP-02/HP-03.

**Dependencies**: None, MB-01 already exists.
**Reuse elsewhere**: Same file reused on Currency Exchange's and Toko Mama's "more work" cross-link cards (2 reuse sites, per `IMAGE_ASSETS.md`).
**Priority**: High.

---
↓
---

## HP-05 — Account Hub Card

**Section**: `.explorations`, first `.exp-card`, `.exp-img.exp-img-accounthub`.
**Purpose**: Exploration-card thumbnail for the Account Hub concept.

**Media type**: JPG (planned).
**Aspect ratio**: 3:2.
**Figma artboard**: 2400 x 1600px.
**Export size**: 2400 x 1600px.

**Reused from another case study?** **Intended, but blocked.** `IMAGE_ASSETS.md` already recommends "can likely reuse the Account Hub case study's own lead/hero image, recropped to 3:2," and this blueprint agrees with that direction. **However, Account Hub has no production blueprint and no delivered assets yet** (unlike Currency Exchange, Toko Mama, and myBCA, all three of which are fully implemented per `MASTER_ASSET_TRACKER.md`). There is currently no source file to reuse.
**Source filename**: Not yet determined, will be whichever file Account Hub's own future blueprint designates as its lead/hero image (a Gallery-template page, so the equivalent of a "hero" is its `.shot-frame.lead` slot, per `IMAGE_STYLE_GUIDE.md`'s Gallery/Rail distinction).
**Dedicated homepage crop needed?** Almost certainly yes, same reasoning as HP-02 through HP-04, but cannot be specified precisely until the source exists.

**Crop strategy**: Cannot be finalized until Account Hub's own blueprint exists and its lead image is produced.
**Focal point**: TBD.
**Responsive behavior**: Same 3:2 hold as every other card slot.

**Dependencies**: **Blocked on Account Hub's own production blueprint and asset delivery.** This is not a homepage production task today, it's a downstream consequence of Account Hub's page work.
**Reuse elsewhere**: Would also be reused on Aryaduta's "more work" cross-link card (per `IMAGE_ASSETS.md`).
**Priority**: Medium, below the fold, lighter section of the homepage, and genuinely blocked regardless of priority.

---
↓
---

## HP-06 — Aryaduta Card

**Section**: `.explorations`, second `.exp-card`, `.exp-img.exp-img-aryaduta`.
**Purpose**: Exploration-card thumbnail for the Aryaduta hospitality concept.

**Media type**: JPG (planned).
**Aspect ratio**: 3:2.
**Figma artboard**: 2400 x 1600px.
**Export size**: 2400 x 1600px.

**Reused from another case study?** **Intended, but blocked**, identical situation to HP-05. `IMAGE_ASSETS.md` recommends reusing "Aryaduta's own lead/hero image, recropped to 3:2." Aryaduta has no blueprint and no delivered assets yet (it's also documented as the single largest remaining production burden in the site, 22 in-page slots, lowest individual hiring weight, per `IMAGE_ASSETS.md`).
**Source filename**: Not yet determined.
**Dedicated homepage crop needed?** Almost certainly yes, cannot be finalized yet.

**Crop strategy**: Cannot be finalized until Aryaduta's own blueprint exists.
**Focal point**: TBD.
**Responsive behavior**: Same 3:2 hold.

**Dependencies**: **Blocked on Aryaduta's own production blueprint and asset delivery**, and per `IMAGE_ASSETS.md`'s existing recommendation, worth "a scope conversation before producing all 17 phone screens" on that page before this card even becomes reachable.
**Reuse elsewhere**: Would also be reused on Currency Exchange's and Account Hub's "more work" cross-link cards.
**Priority**: Medium, same reasoning as HP-05.

---
↓
---

## HP-07 — Favicon

**Section**: Not in the visible DOM. Belongs in `<head>` as `<link rel="icon">` (and optionally `<link rel="apple-touch-icon">`). No such tag exists in `index.html` today.
**Purpose**: Browser tab icon, bookmark icon, and (via apple-touch-icon) home-screen icon on iOS.

**Media type**: PNG (ICO as a legacy fallback if desired; modern browsers accept PNG favicons directly).
**Aspect ratio**: 1:1.
**Figma artboard**: 512 x 512px recommended (scales cleanly down to the smaller sizes actually needed).
**Export size**: Multiple: 32x32 (standard tab icon), 180x180 (apple-touch-icon). Export once at 512x512 and downsize, don't re-draw per size.

**Reused from another case study?** No, this is homepage/sitewide, not case-study content.
**Source filename**: None yet.
**Dedicated homepage crop needed?** Not applicable, this is a new original mark, not a crop of existing photography.
**Crop strategy**: Not applicable.
**Focal point**: Not applicable. Recommend a simple mark consistent with the site's own brand system, most likely the lime accent dot from the "Leo." wordmark (the `.` in Shrikhand with `color: var(--accent)`, already the site's one recurring brand mark) rather than a literal photographic crop, since a favicon at 16-32px needs to read as a single simple shape.
**Responsive behavior**: Not applicable, browsers handle favicon sizing natively.

**Dependencies**: None, this can be produced independently of every other item on this page.
**Priority**: Low. Explicitly tracked in `TODO.md` as an "After Publish" item, not a blocker for launch.

---
↓
---

## HP-08 — OG Image

**Section**: Not in the visible DOM. Belongs in `<head>` as `<meta property="og:image">`. No such tag exists in `index.html` today.
**Purpose**: The preview image shown when the homepage link is shared on LinkedIn, Slack, email, or any Open Graph-aware surface. First impression for anyone who receives a shared link rather than visiting directly.

**Media type**: JPG (PNG only if a specific design needs transparency, unlikely here).
**Aspect ratio**: 1200:630 (the standard OG ratio, roughly 1.91:1).
**Figma artboard**: 1200 x 630px (this is one of the few slots on the site where the artboard size isn't the 2x-export convention used elsewhere, since 1200x630 is itself already the fixed, universally-expected OG delivery size, over-producing it doesn't add value the way it does for in-page retina images).
**Export size**: 1200 x 630px.

**Reused from another case study?** No, and **should not be a raw screenshot or case-study crop.** This should be a composed graphic in the site's own dark/lime editorial system (name, title, maybe the "Leo." wordmark, on the site's `--bg`/`--bg-card` palette), matching how a considered portfolio typically handles its own share card, not a repurposed piece of case-study photography that wouldn't make sense out of context.
**Source filename**: None yet.
**Dedicated homepage crop needed?** Not applicable, new composite, not a crop.
**Crop strategy**: Not applicable.
**Focal point**: Typographic: name and title should read clearly even at the small size most social platforms render OG previews at. **Could optionally reuse the About portrait (HP-01) as a compositional element** (a small crop of it alongside the wordmark and title), which would make this the one HP-08 dependency worth noting, but a text-only composition on the brand palette is equally valid and simpler to produce well.
**Responsive behavior**: Not applicable, this is a static share-preview image, not a responsive in-page asset.

**Dependencies**: Soft dependency on HP-01 (About portrait) only if the composition decision includes the portrait; otherwise none.
**Priority**: Low. Also explicitly tracked in `TODO.md` as "After Publish," not a launch blocker.

---

## Homepage Asset Reuse Matrix

| Card / Asset | Reuse source | Dedicated homepage crop? |
|---|---|---|
| Currency Exchange Card | Reuse CE-01 Hero (`ce-01-hero.jpg`) | **Yes** — re-export from the Figma source at 2400x1600 (3:2), don't pixel-crop the flattened JPG |
| Toko Mama Card | Reuse TM-01 Hero (`tm-01-hero.jpg`) | **Yes** — same re-export approach; TM-01 was already produced with extra crop headroom for this |
| myBCA Card | Reuse MB-01 Hero (`mb-01-hero.jpg`) | **Yes** — same re-export approach; verify safe-area margins hold at 3:2 |
| Account Hub Card | Intended reuse of Account Hub's future lead image | **Blocked** — no source exists yet, Account Hub has no blueprint |
| Aryaduta Card | Intended reuse of Aryaduta's future lead image | **Blocked** — no source exists yet, Aryaduta has no blueprint |
| About Portrait | Existing portrait (already real, live today) | No new photography; technical extraction from base64 to a file only |
| Favicon | New | New original mark, recommend deriving from the existing lime "Leo." accent dot |
| OG Image | New composite | New composed graphic in the site's own dark/lime system; optionally incorporates the About portrait as one element |

**Net effect**: of 6 visible card/photo slots, 3 are fully reusable today (Currency Exchange, Toko Mama, myBCA), 2 are blocked on unrelated pages' own production, and 1 is already finished pending a technical extraction. Of the 2 `<head>`-only assets, both are entirely new and both are explicitly non-blocking for launch.

---

## Effort estimate per asset

| Asset | Effort | Why |
|---|---|---|
| HP-01 About Portrait | **Small** | Pure extraction, no new photography or Figma work |
| HP-02 Currency Exchange Card | **Small** | Re-export from an existing, already-approved Figma composition at a new canvas size |
| HP-03 Toko Mama Card | **Small** | Same as HP-02; extra crop headroom was already anticipated when TM-01 was produced |
| HP-04 myBCA Card | **Small** | Same as HP-02, with one open verification (safe-area margins at 3:2) |
| HP-05 Account Hub Card | **Blocked** | Cannot be scoped until Account Hub has its own blueprint and assets |
| HP-06 Aryaduta Card | **Blocked** | Cannot be scoped until Aryaduta has its own blueprint and assets |
| HP-07 Favicon | **Small** | Single simple mark, one artboard, downsized to two export sizes |
| HP-08 OG Image | **Medium** | New composed graphic, needs a real design decision (typographic-only vs. incorporating the portrait), not just a re-export |

**Total actionable now: 5** (HP-01 through HP-04, HP-07). **Total blocked: 2** (HP-05, HP-06, pending other pages). **One deferred by explicit priority, not blocked: HP-08** (technically actionable today, but `TODO.md` places it after publish).

## Recommended production order

1. **HP-02, HP-03, HP-04 (the three case-study card re-exports)** — build first and together, since they're the same task repeated three times (re-export an existing composition at a new canvas size) and unlock the homepage's above-the-fold visual completeness immediately. Highest priority, lowest effort, zero new creative decisions.
2. **HP-01 (About Portrait extraction)** — do any time, fully independent, a good filler task. Should land before a performance pass regardless of when in this sequence it happens.
3. **HP-07 (Favicon)** — low effort, no dependencies, can be done whenever convenient, but per `TODO.md` doesn't need to happen before launch.
4. **HP-08 (OG Image)** — do after HP-01 if the composition ends up incorporating the portrait; otherwise fully independent. Deferred to After Publish per `TODO.md`, not urgent.
5. **HP-05, HP-06 (Account Hub / Aryaduta cards)** — cannot be started until those two pages get their own production blueprints and at least a lead/hero image each. Revisit this blueprint once that happens rather than guessing at a source now.

---

## Summary

- **Total media slots (visible DOM)**: 6 — About Portrait, 3 Selected Work cards, 2 Other Explorations cards.
- **Total media assets tracked in this blueprint (including `<head>`-only)**: 8 (HP-01 through HP-08).
- **Total unique homepage output files needed**: 8 (each HP item is a distinct file, even where the source photography is reused).
- **Total reused assets (sourced from existing case-study production)**: 3 confirmed now (HP-02, HP-03, HP-04), 2 more planned but blocked (HP-05, HP-06) — 5 of 8 total assets trace back to case-study photography rather than needing original homepage-specific production.
- **Genuinely new, homepage-original assets**: 3 — HP-01 (real, extraction only), HP-07 (favicon), HP-08 (OG composite).

## Implementation checklist

- [ ] Extract HP-01 (About Portrait) from its current base64 payload to `assets/images/about-leo-portrait.jpg`, preserve the existing `alt="Leonardo Budi"` and `object-position: center 35%` framing
- [ ] Re-export HP-02 from CE-01's Figma composition at 2400x1600 (3:2), save as `assets/images/cards/currency-exchange-card.jpg`
- [ ] Re-export HP-03 from TM-01's Figma composition at 2400x1600 (3:2), save as `assets/images/cards/toko-mama-card.jpg`
- [ ] Re-export HP-04 from MB-01's Figma composition at 2400x1600 (3:2), verify safe-area margins hold, save as `assets/images/cards/mybca-card.jpg`
- [ ] Design and export HP-07 (favicon) at 512x512, downsize to 32x32 and 180x180
- [ ] Decide HP-08's composition (typographic-only vs. incorporating the About portrait), then produce at 1200x630
- [ ] Confirm HP-05/HP-06 remain blocked until Account Hub and Aryaduta each get their own production blueprint; do not guess at source files in the meantime
- [ ] Verify each of HP-02/HP-03/HP-04 at actual homepage card display size (not just full export size) before calling them final, since the whole point of the reuse strategy is that these need to read clearly at thumbnail scale, not just at their native resolution
- [ ] Update `IMAGE_ASSETS.md`'s homepage table and `MASTER_ASSET_TRACKER.md` once files are delivered
- [ ] Wire into HTML only after Leo confirms each export (no HTML changes made as part of this blueprint)
