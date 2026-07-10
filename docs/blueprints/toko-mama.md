# TOKO MAMA — PRODUCTION BLUEPRINT

The complete, page-ordered production checklist for `study-case/toko-mama/index.html`. Built by inspecting the entire page top to bottom (a single self-contained file, no separate HTML partials, no includes, matching the site's no-build architecture) against `IMAGE_STYLE_GUIDE.md`, `FIGMA_PRODUCTION_GUIDE.md`, and `IMAGE_ASSETS.md`.

Third blueprint of the set, following the structure established in `docs/blueprints/currency-exchange.md` and `docs/blueprints/mybca.md`. No HTML modified, no redesign, no images generated, blueprint only.

**Revision (2026-07-01): the production plan has expanded from 3 assets to 5, and now includes motion (MP4) as a first-class asset type alongside JPG.** The section below explains what changed and why; everything after it describes the new, current plan. The original 3-asset version of this document is superseded, not preserved inline, git (if this repo used one) or `SESSION_LOG.md` is the place to look for the prior version's exact wording.

---

## Production status

**Implemented and verified (2026-07-02).** All 5 assets are wired into the HTML: TM-01 and TM-04 into their pre-existing slots, TM-02 and TM-05 into newly added markup, TM-03 into its pre-existing slot after a filename mismatch on disk (`tm-02-friction.mp4` vs. the documented `tm-03-friction.mp4`) was resolved. All 5 confirmed loading correctly, holding exact 16:9 at desktop/tablet/mobile, with working lightbox interaction. TM-03 and TM-05 (both MP4) confirmed `autoplay muted loop playsinline`, matching the sitewide video pattern established by Currency Exchange's CE-09.

---

## What changed from the original plan

| | Original plan | Current plan |
|---|---|---|
| Total assets | 3 | 5 |
| Hero | TM-01, unchanged | TM-01, unchanged |
| Context section | No image slot | **New: TM-02**, an editorial environment photograph |
| Friction section | TM-02, a JPG two-moment composite (snackbar + empty aftermath) | **Renumbered to TM-03, now an MP4 motion asset** demonstrating the original problem directly, replacing the composite-JPG workaround entirely |
| Solution section | TM-03, a JPG | **Renumbered to TM-04**, unchanged in substance |
| Outcome section | No image slot | **New: TM-05**, an MP4 motion asset demonstrating the completed interaction |

Two structural consequences worth flagging explicitly, since they affect implementation later (not now, HTML is not being touched in this pass):

1. **TM-02 (Context) and TM-05 (Outcome) do not have HTML slots to wire into yet.** The live page's Context section (`#context`) currently renders only the `.info-stack` (User Profile / Business Need / Design Constraint), no `<figure class="case-shot">`. The Outcome section (`#outcome`) currently renders only a `.case-list` and a closing `.reflection` quote, also no image slot. Both will need a new `.shot-frame` (or a `<video>` element, matching the pattern established for Currency Exchange's CE-09, see TM-03/TM-05 below) added to the markup before these two assets can be wired, whenever HTML work on this page resumes. This blueprint documents the target production spec now, so Figma work isn't blocked waiting for a markup decision, but implementation is blocked on that markup change.
2. **MP4 is now a first-class asset type on this page**, not an exception. `FIGMA_PRODUCTION_GUIDE.md` section 6 previously treated video (via Currency Exchange's CE-09) as a single confirmed exception to an otherwise all-static-image rule. Toko Mama now has two video slots out of five, the largest proportion of any page in the site. `FIGMA_PRODUCTION_GUIDE.md` should be updated to reflect this once this plan is confirmed, see the note at the bottom of this document.

---

## Before you start: constants shared across every asset

**Shared by the 3 static (JPG) assets — TM-01, TM-02, TM-04:**

- **Aspect ratio**: 16:9
- **Figma artboard**: 2400 x 1350px
- **Export size**: 2400 x 1350px (2x of the ~1200-1300px max in-page display width)
- **Export format**: JPG (matching the other two Rail blueprints' recommendation; WebP if confirmed sitewide, `FIGMA_PRODUCTION_GUIDE.md` section 6)
- **Corner radius**: none, sharp rectangle (Rail template, `IMAGE_STYLE_GUIDE.md` section 1)

**Shared by the 2 motion (MP4) assets — TM-03, TM-05:**

- **Aspect ratio**: 16:9 (matching the static frames, so the page keeps one consistent frame shape whether a slot is a photo or a video)
- **Export dimensions**: 2400 x 1350px canvas, same numbers as the static assets, re-encoded to video rather than a still (`FIGMA_PRODUCTION_GUIDE.md` doesn't yet have a locked video-specific size table, this blueprint uses the same 2400x1350 the static Rail frames already use, for consistency, until a dedicated video spec exists)
- **Format**: MP4 (H.264), matching Currency Exchange's CE-09 precedent
- **Playback treatment**: native `<video controls playsinline preload="metadata">`, not the `.shot-frame`/lightbox system, since native controls already provide the play/pause/seek interaction a lightbox would otherwise add. This is the exact pattern CE-09 established and verified working (`SESSION_LOG.md`, 2026-07-01).
- **Performance note**: CE-09 shipped at 49MB and was flagged as too heavy for a portfolio page. Both TM-03 and TM-05 should be produced with a compression pass in mind from the start (trim tightly, moderate bitrate) rather than exported at maximum quality and compressed later, so this doesn't repeat as a post-hoc fix.

**Shared naming convention**: asset-ID prefix, matching the locked pattern (`ce-01-hero.jpg`, `mb-01-hero.jpg`), extended here to include the `.mp4` extension for motion assets: `tm-01-hero.jpg` through `tm-05-outcome.mp4` (`FIGMA_PRODUCTION_GUIDE.md` section 4).

**One open question still flagged for Leo, carried over unchanged**: `IMAGE_STYLE_GUIDE.md` section 13 flags that Toko Mama's placeholder gradients are byte-identical to Currency Exchange's, very likely an accidental copy-paste artifact rather than an intentional shared tint. `FIGMA_PRODUCTION_GUIDE.md` section 8 currently locks in this green backdrop as Toko Mama's literal production spec regardless. Same tension already flagged for myBCA's blue tint in `blueprints/mybca.md`. Still unresolved, still worth Leo settling once across all three Rail pages together.

---

## TM-01 — Hero (Cashier Interface)

**Section**: `.case-hero` figure, immediately after the case-meta grid, before the rail begins. First image on the page.
**Status**: Implemented and verified (2026-07-02). Unchanged from the original plan.
**Type**: Hero image.

**Purpose**: Establish the real product before the narrative starts. Caption: "Toko Mama POS · Cashier Interface." Pairs with the hook copy: "When a cashier puts a transaction on hold, it shouldn't just disappear. Here's how we made it stay visible."

**UI screens that should appear**: The Toko Mama POS cashier interface in its normal, active-transaction state, credible as a real tablet-based checkout tool. Establishes the product and its context, not the Hold Cart problem itself.

**Emphasize**: The interface reading as genuinely built for a tablet POS in a high-traffic retail environment (meta grid: "Platform: Tablet POS," "Constraint: No formal training"), large touch targets, a cart/line-item list, a visible total.

**Omit**: OS chrome, keyboard. Don't show the Hold Cart interaction yet.

**File type**: JPG.
**Aspect ratio**: 16:9.
**Figma artboard**: 2400 x 1350px.
**Export size**: 2400 x 1350px.

**Composition**: Composed Rail slide, single tablet device (landscape, not portrait phone). Screen occupies ~78-85% of canvas height, centered both axes, backdrop fills the rest.

**Safe area**: Central 70% of canvas width, minimum 5% clear backdrop margin on every edge.

**Background treatment**: `linear-gradient(135deg, #051a08 0%, #0a3010 45%, #060f07 100%)`, the locked `.ts-hero` gradient (shared with Currency Exchange, see the open backdrop-tint question above). Plus the two decorative radial highlights (lime 8%/4% opacity), the standard hero-only treatment.

**Filename**: `study-case/toko-mama/assets/tm-01-hero.jpg`.

**Reuse opportunities**: None within this page. Cross-page candidate for the homepage/cross-link Toko Mama card thumbnail (`toko-mama-card.jpg`), alongside TM-04, see TM-04's entry.

**Dependencies**: None.

**Does it appear elsewhere on this page?** No.

**Should it be optimized for future crops?** Yes, same reasoning as before: export with the tablet slightly smaller than the strict minimum within the frame, centered with extra breathing room, in case this becomes the homepage-card source.

**Reuses a Figma master component?** New: a tablet-frame hero-variant Rail backdrop component (with glow), reused by TM-02 and TM-04 below (TM-03 and TM-05 don't use this component, they're video).

**Priority**: High, first image on the page.

---
↓
---

## TM-02 — Context (Editorial Environment Photograph)

**Section**: `#context` (rail 01).
**Status**: Implemented and verified (2026-07-02). New `.shot-frame` figure added after the body paragraph, before the info-stack. Confirmed loading, correct 16:9, lightbox working.
**Type**: Editorial environment photo, not a UI screen.

**Purpose**: Ground the reader in the physical reality of the problem before any interface is shown. Pairs with the section's own copy: "Toko Mama is a convenience store franchise in Indonesia. It's busy, high-traffic, and built around fast checkout... The cashier needs to pause, help someone else, and come back without losing anything." This is the one asset on the page (and, so far, the only environment photograph across any of the three Rail case studies) that isn't a composed device slide.

**Content**: A busy Toko Mama store interior, or a cashier actively working a checkout line under visible time pressure. Real environment, real product context, not a staged or composited UI screen. This is closer in spirit to Currency Exchange's CE-02 (the Nobu Bank building/signage photo already delivered) than to any device-frame slide on this page.

**Emphasize**: A sense of volume and pace, a queue, hands moving, a register mid-transaction, whatever communicates "high-traffic" and "every second counts" without needing the caption to explain it.

**Omit**: Don't stage this as a clean, empty, or posed environment. The whole narrative point of this section is pressure and interruption; a calm, tidy photo would undercut it.

**File type**: JPG.
**Aspect ratio**: 16:9.
**Figma artboard**: 2400 x 1350px.
**Export size**: 2400 x 1350px.

**Composition**: **Not a composed device slide.** No phone/tablet frame, no gradient backdrop tint, this is a straight photographic image, cropped to fill the 16:9 frame directly (`object-fit: cover`, matching how CE-02 was ultimately implemented). Don't force the Rail "screen centered on a dark gradient" system onto this asset, it's a different content type and shouldn't look like a device slide with nothing on it.

**Safe area**: Not applicable in the device-frame sense. Standard photographic composition principles apply instead: keep the main subject (the cashier, the queue, the register) away from the extreme edges so it survives minor responsive recropping.

**Background treatment**: Not applicable, this is a real photograph, not a composed slide with a backdrop gradient.

**Filename**: `study-case/toko-mama/assets/tm-02-context.jpg`.

**Reuse opportunities**: None identified. Not a candidate for the homepage/cross-link card (that card should represent the product, not the environment, per the reasoning already established for TM-01/TM-04).

**Dependencies**: **Needs a new HTML slot before it can be wired** (see "What changed" above). Also needs either a real environment photograph sourced (if Leo has or can get one from the actual client) or a recreated/stock-sourced equivalent, similar in kind to Currency Exchange's CE-03 sourcing dependency, flag this with Leo before starting.

**Does it appear elsewhere on this page?** No.

**Should it be optimized for future crops?** No, this is a scene-specific editorial photo, not a UI asset likely to be cropped elsewhere.

**Reuses a Figma master component?** No, this doesn't use the tablet-frame component at all, it's a plain photographic crop.

**Priority**: High.

---
↓
---

## TM-03 — Friction (Motion: The Original Problem)

**Section**: `#friction` (rail 02).
**Status**: Implemented and verified (2026-07-02). Filename mismatch on disk (`tm-02-friction.mp4` vs. the documented `tm-03-friction.mp4`) resolved, then wired as `autoplay muted loop playsinline` inside the pre-existing `.shot-frame.ts-sec` slot. Renumbered from the original TM-02; content type changed from a static JPG two-moment composite to a motion asset, replacing that composite workaround outright.

**Purpose**: Show the failure mode described in the copy by demonstrating it, not compositing it. Caption context: "When the cashier taps 'Hold Cart,' a snackbar confirms the action for 3 seconds. Then the cart disappears entirely." The `.case-list` beneath names three specific symptoms: the cart disappears, the interface resets to empty, there's no visible indicator of where it went. A real recording of this sequence demonstrates all three directly, which is why this superseded the original two-moment JPG composite plan, a video doesn't need to fake a moment-in-time composite when it can just show the moment.

**What the recording should show**: A cashier tapping "Hold Cart," the 3-second confirmation snackbar appearing and disappearing, and the interface resetting to its empty state, in that order, in real time or close to it.

**Emphasize**: The disappearance itself, the cut from "cart visible" to "cart gone," should read as abrupt and undercommunicated, matching the copy's framing of this as a problem, not a feature.

**Omit**: Don't show the Recall Draft button in a way that makes it look easy to find (same guidance as the original plan). Don't pad the recording with unrelated interactions before or after the core sequence.

**File type**: MP4 (H.264).
**Aspect ratio**: 16:9.
**Export dimensions**: 2400 x 1350px canvas.
**Playback treatment**: Native `<video controls playsinline preload="metadata">`, no lightbox.

**Background/framing**: Screen-recording style, the tablet interface filling the frame directly (matching how CE-09 was ultimately produced), not a composed slide with a gradient backdrop, video content doesn't benefit from the same "device on dark background" treatment static hero/section shots use.

**Filename**: `study-case/toko-mama/assets/tm-03-friction.mp4`.

**Reuse opportunities**: None.

**Dependencies**: **Needs a new `<video>` element in place of the current `.shot-frame` button** before it can be wired (a markup change, not made as part of this blueprint). No external sourcing dependency, this is Toko Mama's own product in its own broken state, fully controllable in a screen recording.

**Does it appear elsewhere on this page?** No.

**Should it be optimized for future crops?** Not applicable to video in the same way as a static image, but keep the recording trimmed tightly to just the relevant sequence (tap → snackbar → empty state) rather than a longer, loosely-bounded clip, both for file size and for editorial pacing.

**Reuses a Figma master component?** No, video assets don't use the Rail backdrop component system the same way static slides do.

**Priority**: High.

---
↓
---

## TM-04 — Solution (Final Design, Tab-Based Cart Switching)

**Section**: `#solution` (rail 04).
**Status**: Implemented and verified (2026-07-02). Renumbered from the original TM-03. Content and spec unchanged.
**Type**: Final UI showcase, hero / payoff.

**Purpose**: Show the resolved design. Caption: "Final Design (Tab-Based Cart Switching)." The copy: "When a cart is held, it becomes a tab at the top of the screen... White tab means active cart, grey tab means held cart. Cashiers can switch between carts with a single click." The three `.reason-card` items beneath it are the takeaways this image needs to make visually obvious.

**UI screens that should appear**: The cashier interface with at least two cart tabs visible at the top of the screen, one active (white) and one held (grey). Ideally three tabs, matching the "maximum of three active hold sessions" constraint named later in the My Role section.

**Emphasize**: The tab row, specifically the white-vs-grey state distinction.

**Omit**: OS chrome, keyboard. Don't show more than three tabs.

**File type**: JPG.
**Aspect ratio**: 16:9.
**Figma artboard**: 2400 x 1350px.
**Export size**: 2400 x 1350px.

**Composition**: Composed Rail slide, single tablet device, same system as TM-01.

**Safe area**: Central 70% of canvas width, minimum 5% clear margin on every edge.

**Background treatment**: `linear-gradient(135deg, #1a1208 0%, #3a2410 50%, #0f0a06 100%)`, the locked `.ts-sec.ts-alt` gradient. No glow.

**Filename**: `study-case/toko-mama/assets/tm-04-solution.jpg`.

**Reuse opportunities**: Cross-page candidate for the homepage/cross-link Toko Mama card thumbnail, alongside TM-01. Pick one of the two, not both, and not a third separate shoot.

**Dependencies**: None, existing HTML slot already accommodates this content type unchanged.

**Does it appear elsewhere on this page?** No.

**Should it be optimized for future crops?** Yes, same reasoning as TM-01: keep the tab row and device inside the safe area's conservative end so a 3:2 crop has room to breathe.

**Reuses a Figma master component?** Yes, the tablet-frame alt-variant backdrop, built at TM-01/TM-02.

**Priority**: High, the payoff image of the narrative.

---
↓
---

## TM-05 — Outcome (Motion: The Completed Interaction)

**Section**: `#outcome` (rail 06).
**Status**: Implemented and verified (2026-07-02). New `.shot-frame`/`<video>` slot added after the recap list, `autoplay muted loop playsinline`. Confirmed loading, correct 16:9, lightbox working.
**Type**: Motion asset, closing demonstration.

**Purpose**: Close the case study by proving the fix works end to end, the same role Currency Exchange's CE-09 plays for its own page. Pairs with the section's copy: "By making carts visible, we reduced reliance on memory and minimized hesitation during peak traffic... cashiers can see all active sessions at a glance, switch between carts instantly, continue transactions without searching."

**What the recording should show**: The completed interaction end to end: resuming a held cart, switching between multiple active carts via the tab row, and continuing checkout to completion. Per the user's own framing: "resume cart, switch carts, continue checkout, etc."

**Emphasize**: Fluency and speed, tab switches should look instant and confident, contrasting directly with TM-03's abrupt, confusing disappearance. If TM-03 and TM-05 are watched back to back, the improvement should be obvious without narration.

**Omit**: Don't pad with unrelated POS functionality (payment processing, receipt printing, etc.) unless directly part of demonstrating the hold/switch/continue flow.

**File type**: MP4 (H.264).
**Aspect ratio**: 16:9.
**Export dimensions**: 2400 x 1350px canvas.
**Playback treatment**: Native `<video controls playsinline preload="metadata">`, no lightbox, same as TM-03.

**Background/framing**: Screen-recording style, same treatment as TM-03.

**Filename**: `study-case/toko-mama/assets/tm-05-outcome.mp4`.

**Reuse opportunities**: None.

**Dependencies**: **Needs a new `<video>` element added to the Outcome section**, which currently has no image/media slot at all (a markup change, not made as part of this blueprint). No external sourcing dependency.

**Does it appear elsewhere on this page?** No.

**Should it be optimized for future crops?** Not applicable. Keep the recording trimmed to the resume → switch → continue sequence specifically, matching the copy's own list of what it should demonstrate, rather than a broader unscoped walkthrough.

**Reuses a Figma master component?** No.

**Priority**: High.

---

## Effort estimate per asset

| Asset | Effort | Why |
|---|---|---|
| TM-01 Hero | **Medium** | Establishes the tablet-frame component from scratch, otherwise a standard single-device composed slide |
| TM-02 Context | **Medium** | New content type (real photography, not a device slide); needs either real sourcing or a credible recreation, plus a new HTML slot |
| TM-03 Friction | **Large** | Motion asset requiring a real recorded sequence (tap → snackbar → empty state), plus a new `<video>` element replacing the existing static slot |
| TM-04 Solution | **Medium** | Single clean screen, needs at least two (ideally three) distinct tab states composited convincingly, unchanged from the original plan |
| TM-05 Outcome | **Large** | Motion asset requiring a full resume/switch/continue sequence, plus a brand-new HTML slot in a section that has never had one |

**Total new builds: 5.** Two Large motion assets (new to this page), three Medium static assets. Meaningfully more scope than the original 3-asset plan, driven almost entirely by the two new video slots and the one new photography-sourcing dependency.

## Recommended build order

1. **TM-01 (Hero)** — build first, establishes the tablet-frame component TM-02 and TM-04 both need.
2. **TM-04 (Solution)** — build second, a single clean state, fast to finish while the tablet-frame component is fresh, and resolves the two-vs-three-tab question that TM-05's demonstration should stay consistent with.
3. **TM-03 (Friction, motion)** — build third. Record this before TM-05 so the "before" state exists as a concrete reference for how much sharper TM-05's "after" should feel by contrast.
4. **TM-05 (Outcome, motion)** — build fourth, directly informed by TM-03's pacing and framing so the two motion assets read as a matched pair.
5. **TM-02 (Context)** — build last, or in parallel with the above if the photography sourcing can happen independently. This is the one asset with a real external dependency (sourcing or recreating a credible store/cashier environment shot), start that sourcing early even if the final photo composition happens last, the same pattern Currency Exchange's CE-03 followed for its own external dependency.

Before starting TM-01, confirm the flagged backdrop-tint question with Leo (unchanged from the previous version of this blueprint). Before starting TM-02, confirm with Leo whether a real Toko Mama store photo is obtainable or whether this needs to be a recreated/stock equivalent, the same kind of sourcing conversation Currency Exchange's CE-03 needed.

---

## Summary

- **Total image/media slots**: 5 in-page (Hero, Context, Friction, Solution, Outcome) + 2 reused cross-link cards (not Toko Mama production items). **Recalculated from the original 3.**
- **Total unique assets to produce**: 5 (3 JPG, 2 MP4).
- **Suggested production order**: TM-01 → TM-04 → TM-03 → TM-05 → TM-02.
- **New HTML dependency**: TM-02 and TM-03 and TM-05 all require markup changes before they can be wired (TM-02 and TM-05 are entirely new slots; TM-03 is a content-type change from `<button class="shot-frame">` to `<video>`). None of this is done as part of this blueprint. Only TM-01 and TM-04 can be wired into the page's current markup unchanged.

## Implementation checklist

- [ ] Confirm the backdrop-tint question (Toko Mama green vs. neutral) with Leo before building TM-01/TM-04
- [ ] Confirm the TM-02 photography sourcing approach (real store photo vs. recreated/stock) with Leo before building
- [ ] Decide whether the homepage/cross-link Toko Mama card thumbnail should be cropped from TM-01 or TM-04, or shot separately
- [ ] Build the tablet-frame hero-variant Rail backdrop component (with glow)
- [ ] Build the tablet-frame alt-variant Rail backdrop component (no glow)
- [ ] Produce TM-01 — Hero (`tm-01-hero.jpg`)
- [ ] Produce TM-04 — Solution, resolve two-vs-three-tab question (`tm-04-solution.jpg`)
- [ ] Record TM-03 — Friction, tap → snackbar → empty state sequence (`tm-03-friction.mp4`)
- [ ] Record TM-05 — Outcome, resume → switch → continue sequence (`tm-05-outcome.mp4`)
- [ ] Source or produce TM-02 — Context, editorial environment photo (`tm-02-context.jpg`)
- [ ] Verify all 3 static exports are 2400x1350, correct 16:9
- [ ] Verify both video exports hold 16:9 and are trimmed tightly (learn from Currency Exchange CE-09's 49MB file-size flag, compress from the start rather than after the fact)
- [ ] If TM-01 or TM-04 is chosen as the card-thumbnail source, verify the 3:2 crop still reads clearly
- [ ] Add the new HTML slots this plan requires (new `.shot-frame` or `<video>` for TM-02 and TM-05, convert TM-03's existing `.shot-frame` to `<video>`) — a separate task, not part of this blueprint, HTML not modified here
- [ ] Update `IMAGE_ASSETS.md` status column once files are delivered
- [ ] Wire into HTML only after Leo confirms each export and the markup changes above are made
