# IMAGE_ASSETS

Complete inventory of every visual asset used (or referenced but missing) across all six pages, built by inspecting every HTML file directly on 2026-06-30. This is the production checklist for replacing placeholders with real exports. No HTML was modified to produce this document.

This is a living document. Update the Status column as each asset is replaced, and re-run a page inspection if any HTML changes (new section, new shot, new card).

## How to read this

- **Current filename**: what's referenced today. Almost everything is a CSS gradient (no file), so this is usually "none (CSS gradient)." One asset is the exception, see below.
- **Status**: `Placeholder` = a real slot exists in the markup (a `.shot-frame` button or `.pip`/`.exp-img`/`.more-img` div) and is wired to the lightbox/hover system already, just rendering a gradient instead of a photo. `Missing` = no slot exists in the HTML at all yet. `Ready` = a real export exists in `assets/` but isn't wired in. `Final` = real, wired, and confirmed done.
- **Dependencies**: anything that should happen first, or other places the same image is reused.
- **Priority**: relative to hiring impact and reading order, not file-production difficulty.

## Headline finding: one real image already exists

The homepage About section (`index.html`) does **not** use a gradient placeholder like every other image slot in the site. It has a real photo of Leo embedded directly as a base64-encoded JPEG inside the `src` attribute (712x1067px, ~103KB). It is functionally finished, real, and already showing on the page today. The only outstanding work on it is technical, not visual: extract it to a real file in `/assets` so it isn't bloating the page's HTML by ~33% (base64 overhead) and can be cached, lazy-loaded, and given normal `width`/`height`/`alt` attributes like every other image will be. See the homepage table below.

## Summary counts

| Page | Image slots | All currently |
|---|---|---|
| Homepage | 6 (4 real, 2 placeholder) | 3 Selected Work cards implemented (2026-07-02), 1 real photo (inline base64, not yet extracted), Account Hub/Aryaduta cards still gradient |
| Currency Exchange | 9 in-page slots, 9 unique files + 2 reused cross-link cards | All 9 implemented and verified (CE-01 through CE-09); CE-04/CE-08 intentionally share one asset |
| Toko Mama | 5 in-page slots, 5 unique assets (2 of them MP4) + 2 reused cross-link cards | All 5 implemented and verified (TM-01 through TM-05) |
| myBCA | 3 in-page + 2 reused cross-link cards | All 3 implemented and verified (MB-01 through MB-03) |
| Account Hub | 7 in-page + 2 reused cross-link cards | All 7 gradient |
| Aryaduta | 22 in-page + 2 reused cross-link cards | All 22 gradient |
| **Total unique files needed** | **52** (20 done: About portrait + all 9 Currency Exchange + all 5 Toko Mama + all 3 myBCA + 3 homepage Selected Work cards; 32 outstanding) | |

The 10 cross-link "more work" card images (2 per case-study page, `.more-img`) are not separate exports. Each one represents a project that already has a canonical thumbnail elsewhere (the homepage card, or another case study's hero), so the recommendation throughout this document is to **reuse the same source file**, not produce a new crop per occurrence. This cuts the real production count from roughly 60 image instances down to 50 unique files, of which 5 (the project-card thumbnails) get reused in up to 3 places each.

---

## Homepage (`index.html`)

| Section | Current filename | Purpose | Recommended final filename | Dimensions | Status | Dependencies | Priority |
|---|---|---|---|---|---|---|---|
| About | `assets/images/about-leo-portrait.jpg` | Portrait of Leo, establishes a real person behind the work | `assets/images/about-leo-portrait.jpg` | 712x1067 (source dimensions, unchanged), `object-position: center 35%` | **Implemented and verified** (2026-07-09): extracted from inline base64 to a real file | None | Done |
| Selected Work, Currency Exchange (featured card) | `hp-ce-card.jpg` | Featured project-card thumbnail, first case study a reader sees | `assets/images/hp-ce-card.jpg` | 3:2, 2400x1600 | **Implemented and verified** (2026-07-02) | **Not yet reused** on Toko Mama's/myBCA's/Account Hub's "more work" cross-link cards, those still show CSS gradients, out of scope for this homepage-only pass | **Highest**, featured card, above the fold on most viewports |
| Selected Work, Toko Mama (card) | `hp-tm-card.jpg` | Project-card thumbnail | `assets/images/hp-tm-card.jpg` | 3:2, 2400x1600 | **Implemented and verified** (2026-07-02) | Same not-yet-reused note as above, cross-link cards out of scope for this pass | High |
| Selected Work, myBCA (card) | `hp-mb-card.jpg` | Project-card thumbnail | `assets/images/hp-mb-card.jpg` | 3:2, 2400x1600 | **Implemented and verified** (2026-07-02) | Same not-yet-reused note as above | High |
| Other Explorations, Account Hub (card) | none (CSS gradient, `.exp-img-accounthub`) | Exploration-card thumbnail | `assets/images/cards/account-hub-card.jpg` | 3:2, e.g. 1200x800 | Placeholder | Reused on Aryaduta's cross-link card. Can likely reuse the Account Hub case study's own lead/hero image, recropped to 3:2 | Medium, below the fold, lighter section |
| Other Explorations, Aryaduta (card) | none (CSS gradient, `.exp-img-aryaduta`) | Exploration-card thumbnail | `assets/images/cards/aryaduta-card.jpg` | 3:2, e.g. 1200x800 | Placeholder | Reused on Currency Exchange's and Account Hub's cross-link cards. Can likely reuse Aryaduta's own lead/hero image, recropped to 3:2 | Medium |

`hero-bg` (the dark-green radial/linear gradient behind the H1) was checked and is decorative CSS art, not a content image slot. It is intentionally not in this inventory.

---

## Currency Exchange (`study-case/currency-exchange/index.html`, Rail, flagship, 8 sections + hero)

The deepest case study and the most-read page. Start image production here.

| Section | Current filename | Purpose | Recommended final filename | Dimensions | Status | Dependencies | Priority |
|---|---|---|---|---|---|---|---|
| Hero | `ce-01-hero.jpg` | "Currency Exchange · nobu Go (Final Design)", the first image on the page | `study-case/currency-exchange/assets/ce-01-hero.jpg` | 16:9, 2400x1350 | **Preview** (wired 2026-07-01, pending art-direction review) | None | **Critical**, first image of the flagship page |
| 01 Context | `ce-02-context.jpg` | "Nobu Bank · nobu Go mobile app", establishes the host product | `study-case/currency-exchange/assets/ce-02-context.jpg` | 16:9, 2400x1350 | **Implemented** (wired and verified 2026-07-01) | Content flag: delivered export is a building/signage photo, not an app screen as briefed, confirm intentional | High |
| 03 Landscape | `ce-03-landscape.jpg` | "Competitor review · CIMB, BLU by BCA, myBCA" | `study-case/currency-exchange/assets/ce-03-landscape.jpg` | 16:9, 2400x1350 | **Implemented** (wired and verified 2026-07-01) | None | High |
| 04 Challenge | `ce-04-challenge.jpg` | "Six elements, one screen", an annotated screen | `study-case/currency-exchange/assets/ce-04-challenge.jpg` | 16:9, 2400x1350 | **Implemented** (wired and verified 2026-07-01) | Composition flag: shows two phones, brief specified one, confirm intentional | High |
| 05 Explorations, Exploration 1 | `ce-05-exploration-a.jpg` | "Exploration 1 · Tabs" | `study-case/currency-exchange/assets/ce-05-exploration-a.jpg` | 16:9, 2400x1350 | **Implemented** (wired and verified 2026-07-01) | Composition flag: tilted device with annotation, brief specified flat/unannotated, confirm intentional | Medium |
| 05 Explorations, Exploration 2 | `ce-06-exploration-b.jpg` | "Exploration 2 · Too Clean" | `study-case/currency-exchange/assets/ce-06-exploration-b.jpg` | 16:9, 2400x1350 | **Implemented** (wired and verified 2026-07-01) | Same composition flag as CE-05 | Medium |
| 05 Explorations, Exploration 3 | `ce-07-exploration-c.jpg` | "Exploration 3 · Almost There" | `study-case/currency-exchange/assets/ce-07-exploration-c.jpg` | 16:9, 2400x1350 | **Implemented** (wired and verified 2026-07-01) | Same composition flag as CE-05 | Medium |
| 07 Final Design | `ce-08-final-design.jpg` | "Final Design · Currency Exchange" | `study-case/currency-exchange/assets/ce-08-final-design.jpg` | 16:9, 2400x1350 | **Implemented and verified** (2026-07-02) | **Confirmed intentional**: byte-for-byte identical to `ce-04-challenge.jpg` on purpose, both slots share the same media asset, only the surrounding narrative differs. Previously flagged as a bug; retracted. | High, the payoff image of the narrative |
| 07 Final Design, full flow | `ce-09-full-transaction-flow.mp4` | "The full transaction flow", described as "From the nobu Go home screen, through Face ID, to a completed exchange" | `study-case/currency-exchange/assets/ce-09-full-transaction-flow.mp4` | 16:9, 2400x1350, 59s | **Implemented and verified** (2026-07-02) | **Revised playback treatment**: now wired inside the `.shot-frame`/lightbox system as `autoplay muted loop playsinline` (no visible `controls`), matching the sitewide rule that MP4 sections should autoplay ambiently and still support the lightbox. Confirmed exact 16:9, autoplay/loop/muted all verified, lightbox clone also autoplays correctly. **Performance flag unchanged**: 49MB file, autoplaying on page load now makes this more urgent to compress, not less. | Medium |
| More work (cross-link to Toko Mama) | none (CSS gradient, `.more-img`) | Cross-link thumbnail | reuse `assets/images/cards/toko-mama-card.jpg` | 3:2 | Placeholder | Same file as Toko Mama's homepage card | Low, reused asset |
| More work (cross-link to Aryaduta) | none (CSS gradient, `.more-img`) | Cross-link thumbnail | reuse `assets/images/cards/aryaduta-card.jpg` | 3:2 | Placeholder | Same file as Aryaduta's homepage card | Low, reused asset |

---

## Toko Mama (`study-case/toko-mama/index.html`, Rail, 6 sections + hero)

**Revised 2026-07-01: production plan expanded from 3 assets to 5, now including 2 motion (MP4) assets.** See `docs/blueprints/toko-mama.md` for the full spec, reasoning, and build order. Filenames below now follow the asset-ID convention locked for Currency Exchange and myBCA (`tm-01-hero.jpg` etc.), superseding the earlier `toko-mama-*.jpg` names in this row.

| Section | Current filename | Purpose | Recommended final filename | Dimensions | Status | Dependencies | Priority |
|---|---|---|---|---|---|---|---|
| Hero | `tm-01-hero.jpg` | "Toko Mama POS · Cashier Interface" | `study-case/toko-mama/assets/tm-01-hero.jpg` | 16:9, 2400x1350 | **Implemented and verified** (2026-07-02) | None | High, first image on the page |
| 01 Context | `tm-02-context.jpg` | New: editorial environment photo, a busy Toko Mama store/cashier under high traffic, not a device screen | `study-case/toko-mama/assets/tm-02-context.jpg` | 16:9, 2400x1350 | **Implemented and verified** (2026-07-02) | New `.shot-frame` figure added to `#context`, placed after the body paragraph, before the info-stack. Lightbox confirmed working. | High |
| 02 Friction | `tm-03-friction.mp4` | "Initial Concept (The Problem)", **a motion asset** demonstrating the original problem (tap → snackbar → empty state) | `study-case/toko-mama/assets/tm-03-friction.mp4` | 16:9, 2400x1350 canvas | **Implemented and verified** (2026-07-02) | Filename mismatch resolved on disk. Wired as `autoplay muted loop playsinline` inside `.shot-frame`/lightbox. | High |
| 04 Solution | `tm-04-solution.jpg` | "Final Design (Tab-Based Cart Switching)" | `study-case/toko-mama/assets/tm-04-solution.jpg` | 16:9, 2400x1350 | **Implemented and verified** (2026-07-02) | None, existing HTML slot, unchanged structurally | High, the payoff image |
| 06 Outcome | `tm-05-outcome.mp4` | New: motion asset demonstrating the completed interaction (resume cart, switch carts, continue checkout) | `study-case/toko-mama/assets/tm-05-outcome.mp4` | 16:9, 2400x1350 canvas | **Implemented and verified** (2026-07-02) | New `.shot-frame`/`<video>` added to `#outcome`, placed after the recap list, `autoplay muted loop playsinline`, confirmed exact 16:9, lightbox works. | High |
| More work (cross-link to Currency Exchange) | none (CSS gradient, `.more-img`) | Cross-link thumbnail | reuse `assets/images/cards/currency-exchange-card.jpg` | 3:2 | Placeholder | Same file as Currency Exchange's homepage card | Low, reused asset |
| More work (cross-link to myBCA) | none (CSS gradient, `.more-img`) | Cross-link thumbnail | reuse `assets/images/cards/mybca-card.jpg` | 3:2 | Placeholder | Same file as myBCA's homepage card | Low, reused asset |

---

## myBCA (`study-case/mybca/index.html`, Rail, 5 sections + hero)

**Filenames below now follow the asset-ID convention locked in `docs/blueprints/mybca.md`** (`mb-01-hero.jpg` etc.), superseding the earlier `mybca-*.jpg` names in this row.

| Section | Current filename | Purpose | Recommended final filename | Dimensions | Status | Dependencies | Priority |
|---|---|---|---|---|---|---|---|
| Hero | `mb-01-hero.jpg` | "myBCA · Transfer to BCA Account (the screen with no balance)" | `study-case/mybca/assets/mb-01-hero.jpg` | 16:9, 2400x1350 | **Implemented and verified** (2026-07-02) | None | Medium, first image on the page |
| 01 Gap | `mb-02-gap.jpg` | "The transfer screen, and the insufficient-balance error when the guess is wrong" | `study-case/mybca/assets/mb-02-gap.jpg` | 16:9, 2400x1350 | **Implemented and verified** (2026-07-02) | Delivered as a two-state composite per the blueprint's resolution of this open question | Medium |
| 04 Toggle | `mb-03-toggle.jpg` | "Before, hidden by default, and revealed with one tap" | `study-case/mybca/assets/mb-03-toggle.jpg` | 16:9, 2400x1350 | **Implemented and verified** (2026-07-02) | Before/after composite, two states in one frame | Medium, the payoff image |
| More work (cross-link to Currency Exchange) | none (CSS gradient, `.more-img`) | Cross-link thumbnail | reuse `assets/images/cards/currency-exchange-card.jpg` | 3:2 | Placeholder | Same file as Currency Exchange's homepage card | Low, reused asset |
| More work (cross-link to Toko Mama) | none (CSS gradient, `.more-img`) | Cross-link thumbnail | reuse `assets/images/cards/toko-mama-card.jpg` | 3:2 | Placeholder | Same file as Toko Mama's homepage card | Low, reused asset |

Note: `mybca-toggle-before-after.png` was already named as the worked example in `PROJECT_STRUCTURE.md`'s naming-convention section. This inventory recommends `.jpg` instead since the other case-study shots are photographic screenshots, not the kind of flat graphic `.png` tends to suit better, but either extension is consistent with the lowercase-hyphen rule. Worth confirming the format with Leo (`.jpg` for photographic screen captures, `.png` only if a frame needs transparency or has large flat color areas that compress better lossless).

---

## Account Hub (`visual-lab/account-hub/index.html`, Gallery, lead + 3 phone-row blocks)

| Section | Current filename | Purpose | Recommended final filename | Dimensions | Status | Dependencies | Priority |
|---|---|---|---|---|---|---|---|
| Lead | none (CSS gradient, `.shot-frame.lead`) | "Nobu · the proposed account hub" | `visual-lab/account-hub/assets/account-hub-hero.jpg` | 16:9, e.g. 1600x900 | Placeholder | None | High, first image on the page |
| Before | none (CSS gradient, `.shot-frame.phone`) | "Existing home, with no clear way into the account" | `visual-lab/account-hub/assets/account-hub-before-home.jpg` | 393x852 (export at 2x, ~786x1704, for retina) | Placeholder | None | Medium |
| Before | none (CSS gradient, `.shot-frame.phone`) | "The slide-out drawer, discoverable only if you knew to look" | `visual-lab/account-hub/assets/account-hub-before-drawer.jpg` | 393x852 (2x export) | Placeholder | None | Medium |
| Direction one, Personal | none (CSS gradient, `.shot-frame.phone`) | "Account now sits in the bottom nav, restructured into clear blocks" | `visual-lab/account-hub/assets/account-hub-direction1-bottom-nav.jpg` | 393x852 (2x export) | Placeholder | None | Medium |
| Direction one, Personal | none (CSS gradient, `.shot-frame.phone`) | "The personal direction, leading with identity" | `visual-lab/account-hub/assets/account-hub-direction1-personal.jpg` | 393x852 (2x export) | Placeholder | None | Medium |
| Direction two, Minimal | none (CSS gradient, `.shot-frame.phone`) | "The minimal direction, restrained and clean" | `visual-lab/account-hub/assets/account-hub-direction2-minimal.jpg` | 393x852 (2x export) | Placeholder | None | Medium |
| Direction two, Minimal | none (CSS gradient, `.shot-frame.phone`) | "Same blocks, lighter visual treatment" | `visual-lab/account-hub/assets/account-hub-direction2-variant.jpg` | 393x852 (2x export) | Placeholder | None | Medium |
| More work (cross-link to Currency Exchange) | none (CSS gradient, `.more-img`) | Cross-link thumbnail | reuse `assets/images/cards/currency-exchange-card.jpg` | 3:2 | Placeholder | Same file as Currency Exchange's homepage card | Low, reused asset |
| More work (cross-link to Toko Mama) | none (CSS gradient, `.more-img`) | Cross-link thumbnail | reuse `assets/images/cards/toko-mama-card.jpg` | 3:2 | Placeholder | Same file as Toko Mama's homepage card | Low, reused asset |

---

## Aryaduta (`visual-lab/aryaduta/index.html`, Gallery, lead + 4 blocks, by far the largest asset count)

22 image slots, the single biggest production burden in the portfolio, on the page with the lowest individual hiring weight (a "Pitch Concept," not a shipped or research-backed case study). Recommend producing this page last, and consider whether all 17 phone screens are necessary for the narrative or whether a curated subset would tell the same story with less production cost, a judgment call for Leo, not a decision to make unilaterally here.

| Section | Current filename | Purpose | Recommended final filename | Dimensions | Status | Dependencies | Priority |
|---|---|---|---|---|---|---|---|
| Lead | none (CSS gradient, `.shot-frame.lead`) | "Aryaduta · Guest Experience App" | `visual-lab/aryaduta/assets/aryaduta-hero.jpg` | 16:9, e.g. 1600x900 | Placeholder | None | Medium, first image on the page |
| Guest Experience App | none (`.shot-frame.phone`) | "Home" | `visual-lab/aryaduta/assets/aryaduta-guest-home.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| Guest Experience App | none (`.shot-frame.phone`) | "My Stays" | `visual-lab/aryaduta/assets/aryaduta-guest-my-stays.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| Guest Experience App | none (`.shot-frame.phone`) | "Room Detail" | `visual-lab/aryaduta/assets/aryaduta-guest-room-detail.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| Guest Experience App | none (`.shot-frame.phone`) | "Digital Key" | `visual-lab/aryaduta/assets/aryaduta-guest-digital-key.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| Guest Experience App | none (`.shot-frame.phone`) | "Feedback" | `visual-lab/aryaduta/assets/aryaduta-guest-feedback.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| The guest request flow | none (`.shot-frame.phone`) | "Choose Request" | `visual-lab/aryaduta/assets/aryaduta-request-choose.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| The guest request flow | none (`.shot-frame.phone`) | "Food & Beverage" | `visual-lab/aryaduta/assets/aryaduta-request-food-beverage.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| The guest request flow | none (`.shot-frame.phone`) | "Item Detail" | `visual-lab/aryaduta/assets/aryaduta-request-item-detail.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| The guest request flow | none (`.shot-frame.phone`) | "Order Summary" | `visual-lab/aryaduta/assets/aryaduta-request-order-summary.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| The guest request flow | none (`.shot-frame.phone`) | "Request Sent" | `visual-lab/aryaduta/assets/aryaduta-request-sent.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| The guest request flow | none (`.shot-frame.phone`) | "My Requests" | `visual-lab/aryaduta/assets/aryaduta-request-my-requests.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| The staff task board | none (`.shot-frame.phone`) | "Incoming" | `visual-lab/aryaduta/assets/aryaduta-staff-incoming.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| The staff task board | none (`.shot-frame.phone`) | "Request Detail" | `visual-lab/aryaduta/assets/aryaduta-staff-request-detail.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| The staff task board | none (`.shot-frame.phone`) | "Accepted" | `visual-lab/aryaduta/assets/aryaduta-staff-accepted.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| The staff task board | none (`.shot-frame.phone`) | "In Progress" | `visual-lab/aryaduta/assets/aryaduta-staff-in-progress.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| The staff task board | none (`.shot-frame.phone`) | "Completed" | `visual-lab/aryaduta/assets/aryaduta-staff-completed.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| The staff task board | none (`.shot-frame.phone`) | "Room View" | `visual-lab/aryaduta/assets/aryaduta-staff-room-view.jpg` | 393x852 (2x export) | Placeholder | None | Low |
| Receptionist Command Center | none (`.shot-frame.wide`) | "Reservations" | `visual-lab/aryaduta/assets/aryaduta-reception-reservations.jpg` | 16:9, e.g. 1600x900 | Placeholder | None | Low |
| Receptionist Command Center | none (`.shot-frame.wide`) | "Guest Detail" | `visual-lab/aryaduta/assets/aryaduta-reception-guest-detail.jpg` | 16:9, e.g. 1600x900 | Placeholder | None | Low |
| Receptionist Command Center | none (`.shot-frame.wide`) | "Rate & Feedback" | `visual-lab/aryaduta/assets/aryaduta-reception-rate-feedback.jpg` | 16:9, e.g. 1600x900 | Placeholder | None | Low |
| Receptionist Command Center | none (`.shot-frame.wide`) | "Feedback Detail" | `visual-lab/aryaduta/assets/aryaduta-reception-feedback-detail.jpg` | 16:9, e.g. 1600x900 | Placeholder | None | Low |
| More work (cross-link to Account Hub) | none (CSS gradient, `.more-img`) | Cross-link thumbnail | reuse `assets/images/cards/account-hub-card.jpg` | 3:2 | Placeholder | Same file as Account Hub's homepage exploration card | Low, reused asset |
| More work (cross-link to Currency Exchange) | none (CSS gradient, `.more-img`) | Cross-link thumbnail | reuse `assets/images/cards/currency-exchange-card.jpg` | 3:2 | Placeholder | Same file as Currency Exchange's homepage card | Low, reused asset |

---

## Known gaps not yet represented in any HTML (Missing)

These have no slot in any page yet, unlike everything above which has a working placeholder slot. Listed here for completeness since the goal is a complete asset inventory, not because they block the image-replacement work.

| Asset | Purpose | Recommended final filename | Dimensions | Status | Priority |
|---|---|---|---|---|---|
| Favicon | Browser tab icon | `assets/icons/favicon.ico` (+ optionally `favicon-32.png`, `favicon-180-apple-touch.png`) | 32x32 / 180x180 | Missing | Low, tracked in `TODO.md` as After Publish |
| Open Graph image | Link preview when shared (LinkedIn, Slack, email) | `assets/images/og-image.jpg` | 1200x630 (standard OG ratio) | Missing | Low, tracked in `TODO.md` as After Publish |

---

## Recommended production order

Matches the priority column above, rolled up by page. This is a sequencing recommendation, not a decision; confirm before starting.

1. **Currency Exchange** (9 images): flagship, deepest page, most likely to get a full read.
2. **Homepage cards** (5 images, reused everywhere): unlocks the cross-link thumbnails on every other page for free once produced, plus the homepage is the entry point for every visitor.
3. **myBCA** (3 images): small, high-completion-velocity win once the pattern is proven on Currency Exchange. **Toko Mama** (revised to 5 assets, 2 of them MP4, see `docs/blueprints/toko-mama.md`) is no longer the same quick win it was under the original 3-asset plan; two of its slots also need new HTML markup before they can be wired, so budget accordingly rather than pairing it with myBCA as an equally small task.
4. **Account Hub** (7 images): moderate effort, Gallery template, phone frames.
5. **Aryaduta** (22 images): largest effort, lowest individual hiring weight (Pitch Concept, not shipped or research-backed). Worth a scope conversation before producing all 17 phone screens.
6. **About portrait extraction** (1 image, technically already done visually): low urgency, but should land before a performance pass since it's currently bloating the homepage's HTML payload.
7. **Favicon and OG image**: explicitly After Publish per `TODO.md`, not a blocker.
