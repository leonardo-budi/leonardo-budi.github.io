# MASTER ASSET TRACKER

A single cross-page ledger of implementation status, one row per asset. This is distinct from the per-page blueprints (`docs/blueprints/`), which document production specs, and from `IMAGE_ASSETS.md`, which is the full per-slot inventory with purpose/dependency detail. This document answers one question only: **is this asset wired into the live HTML, right now?**

Created 2026-07-02 as part of the first implementation pass across Currency Exchange, Toko Mama, and myBCA. Update this file whenever an asset's wired status changes; it should always be reconcilable against a live inspection of each page's HTML.

## Status legend

- **Implemented** — file exists, wired into HTML, verified (loads, correct aspect ratio, lightbox/hover/autoplay behavior as applicable).
- **Blocked** — wired into HTML, but a known content or file problem prevents it from being production-ready.
- **Not implemented (mismatch)** — HTML slot exists but was deliberately left untouched because the expected file doesn't exist under the documented name.
- **Not implemented (placeholder)** — still a CSS gradient, no production work started.

---

## Currency Exchange

| ID | Filename | Status | Note |
|---|---|---|---|
| CE-01 | `ce-01-hero.jpg` | Implemented | Pending art-direction review from an earlier session (photographic background, device tilt/chrome flagged), not a wiring issue |
| CE-02 | `ce-02-context.jpg` | Implemented | Content flag: delivered export is a building/signage photo, not an app screen as briefed |
| CE-03 | `ce-03-landscape.jpg` | Implemented | Clean |
| CE-04 | `ce-04-challenge.jpg` | Implemented | Composition flag: shows two phones, brief specified one |
| CE-05 | `ce-05-exploration-a.jpg` | Implemented | Composition flag: tilted/annotated, brief specified flat |
| CE-06 | `ce-06-exploration-b.jpg` | Implemented | Same flag as CE-05 |
| CE-07 | `ce-07-exploration-c.jpg` | Implemented | Same flag as CE-05 |
| CE-08 | `ce-08-final-design.jpg` | Implemented | **Confirmed intentional (2026-07-02):** byte-for-byte identical to CE-04 on purpose, both slots share the same media asset, only the surrounding narrative differs between the Exploration and Final Design sections. Previously flagged as a bug; that finding is retracted. |
| CE-09 | `ce-09-full-transaction-flow.mp4` | Implemented | `autoplay muted loop playsinline`, wired inside `.shot-frame`/lightbox, confirmed 2026-07-02. 49MB, compression pass still recommended |

**9 of 9 implemented cleanly.**

---

## Toko Mama

| ID | Filename | Status | Note |
|---|---|---|---|
| TM-01 | `tm-01-hero.jpg` | Implemented | Clean |
| TM-02 | `tm-02-context.jpg` | Implemented | New `.shot-frame` slot added to `#context`, per the revised blueprint |
| TM-03 | `tm-03-friction.mp4` | Implemented | **Filename mismatch resolved (2026-07-02)**, file now present on disk under the correct name. Wired as `autoplay muted loop playsinline` inside `.shot-frame`/lightbox, matching CE-09 and TM-05's pattern. |
| TM-04 | `tm-04-solution.jpg` | Implemented | Clean |
| TM-05 | `tm-05-outcome.mp4` | Implemented | New `.shot-frame`/`<video>` slot added to `#outcome`, `autoplay muted loop playsinline`, per the revised blueprint |

**5 of 5 implemented cleanly.**

---

## myBCA

| ID | Filename | Status | Note |
|---|---|---|---|
| MB-01 | `mb-01-hero.jpg` | Implemented | Clean |
| MB-02 | `mb-02-gap.jpg` | Implemented | Delivered as the two-state composite the blueprint called for |
| MB-03 | `mb-03-toggle.jpg` | Implemented | Delivered as the before/after composite the blueprint called for |

**3 of 3 implemented cleanly.**

---

## Homepage

| ID | Filename | Status | Note |
|---|---|---|---|
| HP-01 | `assets/images/about-leo-portrait.jpg` | Implemented (2026-07-09) | Extracted from inline base64 to a real file (712x1067, matches the original source). `<img src>` updated, `alt` unchanged, `index.html` dropped from 188KB to 51KB. |
| HP-02 | `hp-ce-card.jpg` | Implemented | Wired into `.pip-currency` 2026-07-02. Delivered at `assets/images/hp-ce-card.jpg`, not the `assets/images/cards/currency-exchange-card.jpg` path originally recommended in `IMAGE_ASSETS.md`, docs updated to match the actual delivered path. Confirmed 2400x1600 (3:2), hover/hint/lightbox-style overlay applied, click-through navigation unchanged. Also reused on the cross-link "more work" cards on Toko Mama, myBCA, and Account Hub. |
| HP-03 | `hp-tm-card.jpg` | Implemented | Same as HP-02: wired, verified. Also reused on the cross-link "more work" cards on Currency Exchange and Account Hub. |
| HP-04 | `hp-mb-card.jpg` | Implemented | Same as HP-02: wired, verified. Also reused on the cross-link "more work" cards on Currency Exchange and Toko Mama. |
| HP-05 | `hp-ah-card.jpg` | Implemented (2026-07-06) | Wired into `.exp-img-accounthub`. **Ratio flag**: delivered at 2400x1350 (16:9), not the locked 3:2 (2400x1600) Portfolio Card spec the other four homepage cards use. Confirmed byte-identical (same MD5) to `visual-lab/account-hub/assets/ah-01-lead.jpg`, so this is the lead image reused directly, not a dedicated 3:2 re-export as `docs/blueprints/account-hub.md` recommended. The existing `.exp-img { aspect-ratio: 3/2 }` box will center-crop this wider image via `object-fit: cover`. Not corrected, filenames/files used exactly as delivered; flagged for Leo rather than silently accepted. |
| HP-06 | `hp-ar-card.jpg` | Implemented (2026-07-06) | Wired into `.exp-img-aryaduta`. Same ratio flag as HP-05: delivered at 2400x1350 (16:9), not 3:2. Confirmed as a distinct file from `ar-01-lead.jpg` (different MD5, so not a literal duplicate like HP-05), but still not the locked Portfolio Card ratio. Same center-crop consequence as HP-05, same not-corrected treatment. |
| HP-07 | `assets/favicon/favicon.svg` (+ `favicon-16x16.png`, `favicon-32x32.png`, `favicon-48x48.png`, `apple-touch-icon.png`, `favicon-mono.svg`) | Implemented (2026-07-09) | Built from the exact "Leo." wordmark: Shrikhand glyph outlines for "L" and "." extracted directly from the actual font file (fontTools), not redrawn or simplified as new artwork. Same design tokens as the live nav logo (`#0A0A0A` bg, `#F0EFE9` "L", `#C8F135` dot, 0.1em gap matching the site's `margin-left:4px` at 40px). Verified legible at 16x16 and 32x32. `favicon-mono.svg` is a single-color, transparent-background variant wired as `rel="mask-icon"` for Safari pinned tabs. Linked via `<link>` tags in all six HTML files (relative paths adjusted per folder depth). |
| HP-08 | OG image | Not implemented | New asset, not yet started, non-blocking (After Publish per `TODO.md`) |

**8 of 8 implemented (HP-01 through HP-07). HP-08 not started, explicitly deferred (After Publish).**

---

## Cross-link "More Work" cards (site-wide)

All cross-link cards that have a real source image to reuse are now wired, sitewide. None are new exports; all reuse the 3 homepage card files.

| Page | Card → destination | Status | Note |
|---|---|---|---|
| Currency Exchange | → Toko Mama (`hp-tm-card.jpg`) | Implemented | |
| Currency Exchange | → Aryaduta (`hp-ar-card.jpg`) | Implemented (2026-07-06) | |
| Toko Mama | → Currency Exchange (`hp-ce-card.jpg`) | Implemented | |
| Toko Mama | → myBCA (`hp-mb-card.jpg`) | Implemented | |
| myBCA | → Currency Exchange (`hp-ce-card.jpg`) | Implemented | |
| myBCA | → Toko Mama (`hp-tm-card.jpg`) | Implemented | |
| Account Hub | → Currency Exchange (`hp-ce-card.jpg`) | Implemented (2026-07-03) | |
| Account Hub | → Toko Mama (`hp-tm-card.jpg`) | Implemented (2026-07-03) | |
| Aryaduta | → Account Hub (`hp-ah-card.jpg`) | Implemented (2026-07-06) | |
| Aryaduta | → Currency Exchange (`hp-ce-card.jpg`) | Implemented (2026-07-06) | |

**10 of 10 possible cross-link cards implemented.** Every cross-link card on every page now shows a real thumbnail; none remain placeholder.

---

## Account Hub (`visual-lab/account-hub/index.html`, Gallery template)

**Fully implemented 2026-07-06.** Interaction/layout was refined and standardized 2026-07-03; the blueprint (`docs/blueprints/account-hub.md`) was added the same day. All 7 production assets were delivered and validated against the blueprint before wiring (filenames matched exactly; pixel dimensions confirmed AH-01 at 2400x1350/16:9 and AH-02 through AH-07 all at 1350x2400/9:16, matching the locked ratio system precisely).

| ID | Filename | Status | Note |
|---|---|---|---|
| AH-01 | `ah-01-lead.jpg` | Implemented | 2400x1350 (16:9, Landscape Showcase), confirmed |
| AH-02 | `ah-02-before-home.jpg` | Implemented | 1350x2400 (9:16, Portrait Device Showcase), confirmed |
| AH-03 | `ah-03-before-drawer.jpg` | Implemented | Delivered as JPG (the blueprint's default recommendation), not the borderline MP4 alternative it flagged |
| AH-04 | `ah-04-direction-one-nav.jpg` | Implemented | 1350x2400, confirmed |
| AH-05 | `ah-05-direction-one-personal.jpg` | Implemented | 1350x2400, confirmed |
| AH-06 | `ah-06-direction-two-minimal.jpg` | Implemented | 1350x2400, confirmed |
| AH-07 | `ah-07-direction-two-variant.jpg` | Implemented | 1350x2400, confirmed |

**7 of 7 in-page assets implemented.** **2 of 2 cross-link cards implemented** (→ Currency Exchange, → Toko Mama, both from a prior session).

One necessary HTML change made during implementation: `.shot-frame.phone`'s CSS `aspect-ratio` updated from the old `393 / 852` to `9 / 16`, matching the delivered assets' actual ratio (this was the tracked, deliberate follow-up flagged when the ratio system was first standardized).

Design-review observations from the preceding preview pass (lead image's tilted-device treatment vs. the documented flat-mat spec; the phone mat rendering as light gray rather than the locked `#111111`; AH-02/AH-04 and AH-06/AH-07 visual differentiation) were not treated as blockers and were not changed as part of this implementation pass, since Leo proceeded to full implementation with the assets as delivered. See `SESSION_LOG.md`, 2026-07-05 entry, for the full design-review record.

---

## Aryaduta (`visual-lab/aryaduta/index.html`, Gallery template)

**Fully implemented 2026-07-06.** This page had no blueprint until 2026-07-03 (`docs/blueprints/aryaduta.md`) and had never been through the sitewide `.shot-frame` interaction standardization at all before this pass, it carried the same pre-standardization implementation Account Hub had before its own refinement (lime-tint border hover, no overlay/hint/scale, unconditional lightbox-click binding on every `.shot-frame` including More Work `<div>` cards). All of that was corrected as part of this implementation, alongside wiring all 22 production assets. Every filename validated against the blueprint before wiring; every pixel dimension confirmed against the locked ratio system (AR-01 and AR-19 through AR-22 at 2400x1350/16:9, AR-02 through AR-18 all at 1350x2400/9:16).

| ID | Filename | Status |
|---|---|---|
| AR-01 | `ar-01-lead.jpg` | Implemented |
| AR-02 | `ar-02-guest-home.jpg` | Implemented |
| AR-03 | `ar-03-guest-my-stays.jpg` | Implemented |
| AR-04 | `ar-04-guest-room-detail.jpg` | Implemented |
| AR-05 | `ar-05-guest-digital-key.jpg` | Implemented |
| AR-06 | `ar-06-guest-feedback.jpg` | Implemented |
| AR-07 | `ar-07-request-choose.jpg` | Implemented |
| AR-08 | `ar-08-request-food-beverage.jpg` | Implemented |
| AR-09 | `ar-09-request-item-detail.jpg` | Implemented |
| AR-10 | `ar-10-request-order-summary.jpg` | Implemented |
| AR-11 | `ar-11-request-sent.jpg` | Implemented |
| AR-12 | `ar-12-request-my-requests.jpg` | Implemented |
| AR-13 | `ar-13-staff-incoming.jpg` | Implemented |
| AR-14 | `ar-14-staff-request-detail.jpg` | Implemented |
| AR-15 | `ar-15-staff-accepted.jpg` | Implemented |
| AR-16 | `ar-16-staff-in-progress.jpg` | Implemented |
| AR-17 | `ar-17-staff-completed.jpg` | Implemented |
| AR-18 | `ar-18-staff-room-view.jpg` | Implemented |
| AR-19 | `ar-19-reception-reservations.jpg` | Implemented |
| AR-20 | `ar-20-reception-guest-detail.jpg` | Implemented |
| AR-21 | `ar-21-reception-rate-feedback.jpg` | Implemented |
| AR-22 | `ar-22-reception-feedback-detail.jpg` | Implemented |

**22 of 22 in-page assets implemented.** **2 of 2 cross-link cards implemented** (→ Account Hub via `hp-ah-card.jpg`, → Currency Exchange via `hp-ce-card.jpg`).

Standardization work done as part of this pass (mirroring Account Hub's own refinement exactly): canonical `.shot-frame` CSS/JS block (byte-identical to the other five files), lightbox overlay/hint suppression rules added, JS lightbox-open listener scoped to `<button>` only, `.shot-frame.phone`'s `aspect-ratio` corrected from `393 / 852` to `9 / 16`, dead `.more-img::before` hover-zoom rule removed and replaced with the canonical `.more-img.shot-frame` margin override. Verified in-browser at desktop, tablet, and mobile: no console errors, all 24 images (22 in-page + 2 More Work) load at full resolution, lightbox opens correctly with real images and captions, More Work cards correctly trigger real navigation rather than the lightbox, `.wide-grid` collapses to one column at tablet/mobile, `.phone-row` filmstrip scrolls horizontally with a visible scrollbar at mobile width.

**Note left unresolved, not a blocker**: this page's meta grid is still 3 columns (`Client`, `Role`, `Status`), the same non-standard pattern Account Hub had before its own layout polish. Not touched this pass since the task was scoped to asset implementation and interaction standardization, not layout changes; worth revisiting if Leo wants full 4-column consistency across every case-study page.

---

## Outstanding blockers, across all pages with any implementation

**None on Currency Exchange, Toko Mama, myBCA, Account Hub, or Aryaduta.** Every in-page asset and every cross-link card on every page in the portfolio is now implemented. Two previously flagged issues remain resolved:

1. **Currency Exchange CE-08**: confirmed intentional reuse of CE-04's asset, not a bug.
2. **Toko Mama TM-03**: filename mismatch resolved on disk, implemented.

**Homepage**: all 6 visible media slots implemented (About portrait now a real file, 3 Selected Work cards, 2 Other Explorations cards). HP-07 (favicon) and HP-08 (OG image) remain, both non-blocking/deferred.

**Two real, non-blocking flags carried forward from this pass, not fixed, reported for Leo's own judgment**:
1. **HP-05 and HP-06's ratio deviation**: both delivered at 16:9 (2400x1350) rather than the locked 3:2 (2400x1600) Portfolio Card spec. HP-05 (`hp-ah-card.jpg`) is a byte-identical copy of `ah-01-lead.jpg`, not a dedicated re-export. Both will be center-cropped by the existing `aspect-ratio: 3/2` card CSS via `object-fit: cover`.
2. **Aryaduta's meta grid remains 3 columns**, not yet brought to the sitewide 4-column standard Account Hub already received.

**Every page's in-page media, every homepage card, and every cross-link card across the entire six-page site is now implemented and verified.** This is the first point in the project where that sentence is true.

**All 20 in-page implemented assets** (9 Currency Exchange + 5 Toko Mama + 3 myBCA + 3 Homepage Selected Work cards) **plus all 8 possible cross-link cards are verified and clean.**
