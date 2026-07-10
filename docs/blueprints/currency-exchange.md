# CURRENCY EXCHANGE — PRODUCTION BLUEPRINT

The complete, page-ordered production checklist for `study-case/currency-exchange/index.html`. Built by reading the entire page top to bottom against `IMAGE_ASSETS.md`, `IMAGE_STYLE_GUIDE.md`, and `FIGMA_PRODUCTION_GUIDE.md`. Work this file from CE-01 to CE-09 in Figma; the "Recommended build order" section at the bottom resequences for efficiency where it beats reading order.

This is the first of what should become one blueprint per page. The same structure (reading-order checklist, then a resequenced build order) should be reused for Toko Mama, myBCA, Account Hub, and Aryaduta once Currency Exchange is done, each as its own file under `docs/blueprints/`.

No HTML modified, no redesign, this only maps what already exists into a build sequence.

---

## Production status (2026-07-02)

All 9 assets are produced and wired into the HTML.

- **CE-08 confirmed as an intentional reuse of CE-04's asset (2026-07-02), not a bug.** Both slots share the same media on purpose, only the surrounding narrative differs between the Exploration and Final Design sections. The 2026-07-01 finding that flagged this as a "wrong-file duplicate" is retracted.

Remaining non-blocking flags, each noted in its own entry: CE-01 pending art-direction review, CE-02's building photo vs. app screen, CE-04's terminology mismatches, CE-05/06/07's tilted/annotated treatment, CE-09's file size. None of these block considering the page's asset wiring complete.

---

## Before you start: one structural fact that shapes everything below

The page has **9 image slots and 9 unique production items.** Section 08 (Reflection) has no image slot at all, the page simply ends its visual content at the full transaction flow. The two "More work" cross-link thumbnails at the bottom of the page are not Currency Exchange production items, they reuse Toko Mama's and Aryaduta's own card thumbnails, produced as part of those pages' own work.

All 9 items below are 16:9 Rail frames (`FIGMA_PRODUCTION_GUIDE.md` section 1), so artboard, export size, and format are identical across every item except CE-09 (see its own entry), only composition, content, and inset vary. Those constants are stated once here rather than repeated nine times:

- **Aspect ratio**: 16:9
- **Figma artboard**: 2400 x 1350px
- **Export size**: 2400 x 1350px (already 2x of the ~1200-1300px max in-page display width)
- **Export format**: WebP (quality ~80-85), JPEG as fallback pending final format confirmation. **Exception: CE-09** is intentionally format-agnostic, most likely an animated GIF or other lightweight looping format rather than a static image, see its own entry.
- **Corner radius**: none, sharp rectangle (Rail template, `IMAGE_STYLE_GUIDE.md` section 1)

---

## CE-01 — Hero

**HTML section**: `.case-hero` figure, immediately after the case-meta grid, before the rail begins. First image on the page.
**Position**: 1st image encountered, above the fold for most viewports.
**Belongs to**: The page hero, not numbered in the rail (sits before section 01 Context).
**Type**: Hero.

**Status: Implemented, pending art-direction review (not marked complete).** Wired into the HTML and verified technically sound (correct file, correct 2400x1350 resolution, loads without error, holds 16:9 at desktop/tablet/mobile, lightbox works). Not marked complete because the delivered export has open art-direction findings from the earlier QA pass (photographic outdoor background instead of the locked gradient backdrop, visible device chrome and tilt, directional shadow, off-center composition, OS status bar in crop, CTA not visible, a copy typo). See the joint art-direction review still pending with Leo before this asset is finalized.

**Purpose**: Prove in one glance that this shipped and solved the stated problem, before the reader has read any narrative. Pairs with the hook copy: "Real money, live rates, split-second decisions... making all of that feel simple, without hiding what users needed to know."

**UI screens that should appear**: The finished exchange screen: both currency panels (buy/sell) visible and editable simultaneously, currency + account + balance grouped per side, the live rate with a swap control centered between the two panels, the primary CTA visible at rest.

**Emphasize**: The rate + swap control first, then the two panels as a balanced pair, then the CTA as the closing beat.

**Omit**: OS status bar, home indicator, keyboard, any tab/nav bar not load-bearing for this screen.

**Composition**: Portrait phone screen centered on the 16:9 canvas, both axes. Screen occupies ~78-85% of canvas height (roughly 1050-1150px at 1350px canvas height), backdrop fills the rest, split evenly top and bottom. Width follows the phone's real aspect ratio, most of the canvas width stays backdrop on purpose.

**Safe area**: Keep the phone and all its content within the central 65% of canvas width. Leave a minimum 5% clear backdrop margin on every edge, no content (including the decorative glow) should touch the canvas border.

**Screenshot inset**: Not applicable, this is a Rail composed slide, not a matted Gallery frame. See "Composition" above.

**Background treatment**: `linear-gradient(135deg, #051a08 0%, #0a3010 45%, #060f07 100%)`, the locked `.ts-hero` gradient. **Plus the two decorative radial highlights**: lime at 8% opacity centered ~30%/30%, lime at 4% opacity centered ~75%/70%. This is the one frame in the page allowed this extra polish (`IMAGE_STYLE_GUIDE.md` section 13). CE-08 uses the same backdrop treatment since it shows the same Final Design screen.

**Filename**: `study-case/currency-exchange/assets/ce-01-hero.jpg`.

**Reuses a Figma master component?** Yes, the Rail backdrop component, **hero variant** (with glow). Build this variant first since it's needed here and nowhere else, every other Currency Exchange asset uses the plain section variant.

---
↓
---

## CE-02 — Context

**HTML section**: `#context` (rail 01).
**Position**: 2nd image, first one inside the rail-numbered narrative.
**Belongs to**: "Meet Nobu Bank, and the gap." The section establishes who Nobu is before the project starts.
**Type**: Supporting image (establishing shot).

**Status: Implemented and verified (2026-07-01).** Wired, loads correctly, holds 16:9 at desktop/tablet/mobile, lightbox works. **Content flag**: the delivered export is a photograph of a Nobu Bank building exterior/signage, not a screen of the nobu Go app as the brief specified ("a representative screen of the existing nobu Go app, the home/dashboard screen is the natural choice... not the currency exchange flow"). Technically sound, but worth confirming with Leo whether this is an intentional creative deviation before calling the asset final.

**Purpose**: Ground the reader in the host product before the project's problem is introduced. Caption: "Nobu Bank · nobu Go mobile app." This is about the bank's existing app, not the new currency feature, it's context, not a preview.

**UI screens that should appear**: A representative screen of the existing nobu Go app (the home/dashboard screen is the natural choice), showing it as a real, in-production banking app. Not the currency exchange flow, this section is explicitly about the gap that existed before the project.

**Emphasize**: That this is a real, credible, already-functioning banking app (matches the copy's "120,000+ users" scale claim). Clean, trustworthy, unremarkable in a good way, it shouldn't try to be exciting.

**Omit**: Anything related to currency exchange (that's the gap being described, it shouldn't appear yet). OS chrome, keyboard.

**Composition**: Same single-phone-centered system as CE-01, no glow. Screen at ~78-85% of canvas height, centered both axes.

**Safe area**: Central 65% of canvas width, 5% minimum clear backdrop margin on every edge.

**Screenshot inset**: Not applicable (Rail).

**Background treatment**: `linear-gradient(135deg, #0d1f05 0%, #1a3a08 50%, #0a100a 100%)`, the locked `.ts-sec` gradient (shared with Toko Mama). No glow, flat.

**Filename**: `study-case/currency-exchange/assets/ce-02-context.jpg`.

**Reuses a Figma master component?** Yes, Rail backdrop component, **section variant** (no glow). This is the simplest asset on the page, a good candidate to validate the section-variant component before using it five more times.

---
↓
---

## CE-03 — Landscape (Competitor Review)

**HTML section**: `#landscape` (rail 03).
**Position**: 3rd image.
**Belongs to**: "What competitors were doing." The section names three specific apps with specific critiques.
**Type**: **Comparison** (a deliberate exception to the single-device default, three real apps are explicitly named and critiqued side by side).

**Status: Implemented and verified (2026-07-01).** Wired, loads correctly, holds 16:9 at desktop/tablet/mobile, lightbox works. Triptych of CIMB/BLU by BCA/myBCA renders as specified, with per-app name labels beneath each panel as the brief recommended.

**Purpose**: Make the competitive gap legible at a glance. Caption: "Competitor review · CIMB · BLU by BCA · myBCA." The body copy and the case-list beneath it are specific enough that this should function almost as evidence, not just mood: "nobody put the full picture together."

**UI screens that should appear**: Three real competitor screens, one per named app, each showing exactly the state the case-list describes:
- **CIMB**: a transfer screen with no rate shown, no account balance, one side of the transaction at a time.
- **BLU by BCA**: a dual-field screen (closest structurally) but with no balance visible on the main screen.
- **myBCA**: the confirmation screen showing its 59-second rate countdown.

**Emphasize**: The specific absence or presence each app's screen demonstrates, this image's whole job is letting the reader visually confirm the case-list claims next to it. A small identifying label under each panel (app name only, e.g. "CIMB") is recommended even though it's a deviation from this page's general "no in-image labels" default, three unlabeled bank screens are not self-identifiable at a glance, and the copy explicitly names each one. Keep any label minimal: Inter, small caps, neutral gray, matching the annotation typography rule in `IMAGE_STYLE_GUIDE.md` section 10, not a new visual device.

**Omit**: Anything from these apps beyond the specific screen named. No need to show full flows, just the one relevant state per app.

**Composition**: A **triptych**, three phone screens of equal size arranged side by side, evenly spaced, centered as a group on the 16:9 canvas. This is a new layout, not the standard single-phone Rail composition, see "Component" note below.

**Safe area**: Each of the three panels equal width, a consistent ~4% canvas-width gutter between them. The group as a whole centered with a minimum 8% margin from every canvas edge, the wider safe margin (versus the standard 5%) accounts for the optional name labels needing room beneath each panel without crowding the canvas edge.

**Screenshot inset**: Not applicable (Rail), but unlike CE-01/CE-02, each individual panel here is smaller, scale each phone so all three plus their gutters fit within the safe area while each phone individually still occupies roughly 70-78% of its own allotted column height.

**Background treatment**: `linear-gradient(135deg, #0d1f05 0%, #1a3a08 50%, #0a100a 100%)`, the same `.ts-sec` gradient as CE-02. No glow.

**Filename**: `study-case/currency-exchange/assets/ce-03-landscape.jpg`.

**Reuses a Figma master component?** Partially. The backdrop reuses the standard section-variant component. The **triptych layout itself is a new component**, not yet in `FIGMA_PRODUCTION_GUIDE.md`. Build it once here; if a future page needs a similar multi-app or multi-state comparison, promote it into the shared guide rather than rebuilding it from scratch, but don't add it speculatively until a second real use case shows up.

**Production dependency, flag before starting**: this is the only asset on the page that needs **real source material from outside Figma**, actual screenshots or accurate recreations of CIMB's, BLU by BCA's, and myBCA's relevant screens. Confirm whether you already have these captured from the original competitive research, or whether they need to be sourced fresh before this asset can be built. This is worth starting early even if the final composition happens later in the build order (see "Recommended build order" below).

---
↓
---

## CE-04 — Challenge (Six Elements, One Screen)

**HTML section**: `#challenge` (rail 04).
**Position**: 4th image.
**Belongs to**: "One screen. A lot to solve." The case-list beneath it names exactly six things.
**Type**: **Annotated diagram** (one of only two annotated slots on this page).

**Status: Implemented and verified (2026-07-01).** Wired, loads correctly, holds 16:9 at desktop/tablet/mobile, lightbox works. **Content flag**: the delivered export shows two phone screens side by side with annotation lines, where the brief specified a single annotated screen ("Single phone, but scaled slightly smaller... to leave room for annotation labels"). Worth confirming with Leo whether the two-screen treatment is an intentional composition choice before calling the asset final. **Terminology flag (2026-07-01)**: three of the baked-in annotation labels don't match the terminology established elsewhere in this case study: "Source of funds" should read "Source of fund" (singular, used 6+ times site-wide), "Transaction purposes" should read "Transaction purpose" (singular, matches this section's own list), and "Exchange rate information" doesn't match "live rate," the term used everywhere else including this section's own list. These are baked into the image pixels and can't be corrected via HTML/CSS, needs a Figma re-export.

**Purpose**: Make the difficulty concrete. Caption: "Six elements, one screen." The copy's whole point is that six distinct requirements had to coexist on one screen, the image needs to show all six and mark them.

**UI screens that should appear**: The final exchange screen (the same screen as CE-01/CE-08, or a close variant of it) with all six elements visible and annotated: (1) two active fields, buy and sell, (2) the destination account, (3) the source of fund, (4) transaction purpose and additional information, (5) a compliance disclaimer, (6) the live rate with swap control.

**Emphasize**: All six elements need roughly equal annotation weight, this is a "look how much had to fit" image, not a hierarchy image. The annotation marks themselves (numbers 1-6, thin connector lines) are what's emphasized, more than any single UI element over another.

**Omit**: Nothing from the six-element list should be cropped out, by definition every one of them needs to be visible and labeled. OS chrome, keyboard.

**Composition**: Single phone, but scaled slightly smaller than CE-01/CE-02 to leave room for annotation labels and connector lines extending outward from the screen, recommend the phone at ~65-72% of canvas height (versus the standard 78-85%) specifically to make room for the six callouts.

**Safe area**: Central 55-60% of canvas width for the phone itself, with the outer band (up to 8-10% margin from each edge) reserved for annotation labels and their connector lines. This is the one asset on the page where the safe-area margin needs to be treated as active label space, not just empty backdrop.

**Screenshot inset**: Not applicable (Rail).

**Background treatment**: `linear-gradient(135deg, #0d1f05 0%, #1a3a08 50%, #0a100a 100%)`, the same `.ts-sec` gradient. No glow, the annotation marks are the focal device here, not a backdrop highlight.

**Annotation style** (per `IMAGE_STYLE_GUIDE.md` section 10): Inter typeface, thin hairline connector lines (not thick arrows), neutral white/gray palette, **never the lime accent**. Number each callout 1-6, matching the case-list order beneath the image so a reader can map label-to-list directly.

**Filename**: `study-case/currency-exchange/assets/ce-04-challenge.jpg`.

**Reuses a Figma master component?** Yes for the backdrop (section variant) and the phone screen content (can likely reuse CE-01's screen as the base, since the final design already shows these six elements, just add the annotation layer on top). Build the **annotation/callout component** (numbered marker + hairline + label) here, it's also needed for myBCA's toggle before/after slot later, so build it as a reusable component now rather than a one-off.

---
↓
---

## CE-05 — Exploration 1 · Tabs

**HTML section**: within `#explorations` (rail 05), first of three exploration sub-blocks.
**Position**: 5th image.
**Belongs to**: "Logical on paper. Broken in practice." First of three sequential failed explorations.
**Type**: Exploration.

**Status: Implemented and verified (2026-07-01).** Wired, loads correctly, holds 16:9 at desktop/tablet/mobile, lightbox works. **Composition flag**: the delivered export shows the phone tilted with annotation callout lines. The brief specified flat, front-on, no annotation for this slot (annotation was reserved for CE-04 only, per `IMAGE_STYLE_GUIDE.md` section 11's "flat, front-on perspective only" rule). Worth confirming with Leo whether this tilted, annotated treatment is an intentional style choice for all three Explorations before calling the asset final.

**Purpose**: Show the first design attempt and let its specific flaws be visible, not just described. Image caption (below, as `.img-caption`): "One side at a time, a buried rate, and a currency selector that read as 'equivalent' rather than a real swap."

**UI screens that should appear**: A tabbed interface, one currency side (buy or sell) showing at a time. Critically, per the copy, **no source-of-fund field anywhere on screen** (that's explicitly named as the flaw). The live rate present but visually buried, in plain text rather than a prominent readout. A currency selector control that reads more like a label ("equivalent to") than an actionable swap button.

**Emphasize**: The three specific trust problems the copy names: the missing source of fund, the buried rate, the passive-reading currency selector. A reader should be able to spot all three without needing the caption to explain them.

**Omit**: Anything that would make this look more resolved than it was, this is explicitly an early, flawed iteration. No source-of-fund field (its absence is the point), no swap control polish.

**Composition**: Standard single-phone Rail composition, same system as CE-01/CE-02, ~78-85% canvas height, centered.

**Safe area**: Central 65% of canvas width, 5% minimum clear margin on every edge.

**Screenshot inset**: Not applicable (Rail).

**Background treatment**: `.ts-sec` gradient, same as CE-02/CE-03/CE-04. No glow, this is a process image, not a hero moment.

**Filename**: `study-case/currency-exchange/assets/ce-05-exploration-a.jpg`.

**Reuses a Figma master component?** Yes, Rail backdrop component, section variant. No new component needed.

---
↓
---

## CE-06 — Exploration 2 · Too Clean

**HTML section**: within `#explorations`, second sub-block.
**Position**: 6th image.
**Belongs to**: "Clean enough to look good. Not clear enough to work."
**Type**: Exploration.

**Status: Implemented and verified (2026-07-01).** Wired, loads correctly, holds 16:9 at desktop/tablet/mobile, lightbox works. Same composition flag as CE-05: tilted device with annotation lines rather than the brief's flat, unannotated treatment. See CE-05's note; likely the same intentional style choice applied consistently across all three Explorations, worth a single confirmation covering all three rather than three separate ones.

**Purpose**: Show the correction (source of fund now present) and its new problem (clarity sacrificed for minimalism). Caption: "Source of fund came forward, but the fields didn't look interactive and the rate hid behind a sheet."

**UI screens that should appear**: Source of fund now visible on the main screen (the fix from Exploration 1). But the input fields should look like static display text, with no visible affordance (no border, no chevron, nothing signaling they're tappable). The rate should not be visible on the main screen at all, at most a bottom-sheet handle hint suggesting more detail is one tap away.

**Emphasize**: The specific new failure: fields that look inert rather than interactive, and a rate that's now hidden rather than just buried. This should read as visually quieter and more minimal than Exploration 1, that's the point, the minimalism itself is the flaw being illustrated.

**Omit**: Don't show the bottom sheet open (the rate is hidden, the point is that it's not visible on the main screen). Don't add any affordance hints that would undercut "the fields didn't look interactive."

**Composition**: Standard single-phone Rail composition, identical system to CE-05.

**Safe area**: Central 65% of canvas width, 5% minimum clear margin on every edge.

**Screenshot inset**: Not applicable (Rail).

**Background treatment**: `.ts-sec` gradient, no glow.

**Filename**: `study-case/currency-exchange/assets/ce-06-exploration-b.jpg`.

**Reuses a Figma master component?** Yes, Rail backdrop component, section variant. No new component needed.

---
↓
---

## CE-07 — Exploration 3 · Almost There

**HTML section**: within `#explorations`, third and final sub-block.
**Position**: 7th image.
**Belongs to**: "The closest one. But two things broke."
**Type**: Exploration.

**Status: Implemented and verified (2026-07-01).** Wired, loads correctly, holds 16:9 at desktop/tablet/mobile, lightbox works. Same composition flag as CE-05/CE-06: tilted device with annotation lines rather than flat/unannotated. See CE-05's note.

**Purpose**: Show the most-resolved failed attempt, close enough to the final design that its two remaining flaws stand out clearly. Caption: "Better structure, but the two account cards were indistinguishable and the tabs still hadn't earned their place."

**UI screens that should appear**: Source of fund and destination account now in the same card (the structural fix from this round). But, per the copy, the two account cards (source and destination) should look **visually identical** to each other, same styling, same hierarchy, no clear differentiator. Tabs should still be present (not yet removed, that doesn't happen until the final design).

**Emphasize**: The visual sameness of the two account cards, a reader should be able to look at this and genuinely struggle to tell which card is the source and which is the destination, that confusion is the entire point of this image. The lingering tab UI as a secondary, still-present flaw.

**Omit**: Don't differentiate the two account cards in a way the copy doesn't support, that would undercut the lesson. Don't remove the tabs (that's the final design's fix, not this one's).

**Composition**: Standard single-phone Rail composition, same system as CE-05/CE-06. As the closest exploration to the final design, this one should feel the most visually similar to CE-01 of the three explorations, reinforcing the "almost there" framing.

**Safe area**: Central 65% of canvas width, 5% minimum clear margin on every edge.

**Screenshot inset**: Not applicable (Rail).

**Background treatment**: `.ts-sec` gradient, no glow.

**Filename**: `study-case/currency-exchange/assets/ce-07-exploration-c.jpg`.

**Reuses a Figma master component?** Yes, Rail backdrop component, section variant. No new component needed.

---
↓
---

## CE-08 — Final Design

**HTML section**: `#final` (rail 07), first figure in the section.
**Position**: 8th image encountered while reading.
**Belongs to**: "Everything the user needs. Nothing they don't." The narrative payoff after three explorations and the principle section.
**Type**: Hero / payoff.

**Status: Implemented and verified (2026-07-02).** Wired into the HTML, technically sound (correct 2400x1350 resolution, loads without error, holds 16:9 at desktop/tablet/mobile, lightbox works, hover affordance and cursor work correctly). **Confirmed intentional (2026-07-02)**: `ce-08-final-design.jpg` is byte-for-byte identical to `ce-04-challenge.jpg` on purpose, both slots deliberately share the same media asset. Only the surrounding narrative changes between the Exploration/Challenge section and the Final Design section. A 2026-07-01 finding flagged this as a wrong-file bug on the assumption CE-08 should pair with CE-01 instead; that finding is retracted, the CE-04 pairing is correct.

**Purpose**: The closing design statement of the narrative. Caption: "Final Design · Currency Exchange." Reuses CE-04's annotated screen as the earned reveal at the end of the narrative, the callouts that explained the six required elements during the Challenge section now serve as the visual proof that the final design accommodates all of them.

**UI screens that should appear**: Same screen content as CE-04 (the annotated six-element diagram), reused rather than re-exported.

**Composition**: Rail composed slide, `.ts-sec.ts-alt` slot. Same annotated two-phone composition as CE-04. Note: the CSS placeholder for this slot uses the amber `.ts-alt` gradient; the real image's own baked-in backdrop takes over once wired.

**Background treatment**: Same as CE-04, since this is the same file.

**Filename**: `study-case/currency-exchange/assets/ce-08-final-design.jpg`.

**Reuses a Figma master component?** Yes, Rail backdrop component, hero variant. The screen content can likely be duplicated directly from CE-01's frame; the new work is the export itself.

---
↓
---

## CE-09 — The Full Transaction Flow

**HTML section**: `#final` (rail 07), second figure, immediately after the final-design recap list.
**Position**: 9th and last image on the page.
**Belongs to**: Closes out the Final Design section. Caption (as `.img-caption`, below the image): "From the nobu Go home screen, through Face ID, to a completed exchange."
**Type**: Sequence / flow (the one genuinely multi-step image on this page).

**Purpose**: Prove the feature works end to end as a real, shippable flow, not just a single polished screen. This is the closing visual statement of the case study before Reflection (which has no image of its own).

**Status: Implemented and verified (2026-07-01).** The format decision resolved to a real MP4 video rather than a static image or GIF. Delivered as `ce-09-full-transaction-flow.mp4`, confirmed 2400x1350 (exact 16:9, matches every other Rail frame's canvas), 59-second duration. Wired as a native `<video controls playsinline preload="metadata">` element (not a `.shot-frame`, since native playback controls already provide the interaction a lightbox would otherwise add). Verified: play/pause both work, renders at exact 16:9 at desktop/tablet/mobile with no cropping (`object-fit: cover` is safe since the source aspect ratio matches exactly), `preload="metadata"` avoids downloading the full file until the user presses play. **Performance flag**: the file is 49MB, unusually heavy for a portfolio page; worth a compression pass (H.264 at a lower bitrate, or a shorter/trimmed cut) before this counts as production-ready, since it will meaningfully slow the page on a first visit if the user does press play.

**Original format-decision note (superseded 2026-07-01):** the copy describes a multi-step sequence (home screen → Face ID → completed exchange). This was previously flagged as intentionally undecided between a static composited image and an animated GIF; the video format above resolves that decision.

**UI screens that should appear**, as a left-to-right sequence within one frame: (1) the nobu Go home screen (entry point), (2) the Face ID / biometric confirmation moment, (3) the final exchange screen (the CE-01 screen, or its completed/confirmed state), (4) optionally a "completed" success state if the copy's "completed exchange" implies a distinct confirmation screen beyond the final design screen itself. 3 panels is the minimum to read as a flow, 4 is acceptable if a distinct success state exists and adds clarity rather than redundancy.

**Emphasize**: The sense of progression, left to right, panel to panel. Each panel should be recognizable as a distinct step, not a near-duplicate of its neighbor.

**Omit**: Don't pad the sequence with intermediate steps the copy doesn't mention. Three named beats (home, Face ID, completed exchange) is the spec, don't invent a fourth and fifth step just to fill the frame.

**Composition**: Multiple phone screens arranged left to right within the single 16:9 frame, **not** a single device in hand or a literal device-in-motion treatment (`IMAGE_STYLE_GUIDE.md` section 12). Same flat, no-shadow, front-on treatment as every other asset on this page, just multiple panels instead of one.

**Safe area**: Each panel equal width with a consistent gutter (recommend ~3-4% of canvas width between panels, tighter than CE-03's triptych gutter since these panels are meant to read as a continuous sequence, not separately-labeled comparison items). Group centered with a minimum 6% margin from canvas edges.

**Screenshot inset**: Not applicable (Rail).

**Background treatment**: `.ts-sec` gradient (same green family as CE-02 through CE-07), no glow. A subtle directional cue between panels (a thin connecting line or a small forward arrow in neutral gray, not lime) is optional and should stay minimal if used, this isn't an annotated diagram like CE-04, it's a sequence, the panel order itself should carry most of the storytelling.

**Filename**: `study-case/currency-exchange/assets/ce-09-full-transaction-flow.mp4`.

**Reuses a Figma master component?** Backdrop reuses the section-variant component. The **multi-panel sequence layout is a new component**, related to but not identical to CE-03's triptych (CE-03 compares three different apps side by side with labels, CE-09 sequences one app's flow without labels). Build it as its own component; don't force it to share CE-03's triptych component just because both are "multiple phones in one frame," they serve different reading patterns.

---

## Effort estimate per asset

| Asset | Effort | Why |
|---|---|---|
| CE-01 Hero | **Large** | Highest-stakes single asset on the page, appears twice, defines the visual language (phone styling, type treatment, backdrop) every other asset on this page inherits from |
| CE-02 Context | **Small** | One screen, no annotation, no composite, the existing nobu Go app, simplest asset on the page |
| CE-03 Landscape | **Large** | Three-panel triptych, a new layout component, plus a real external dependency (sourcing or recreating three competitor apps' screens) |
| CE-04 Challenge | **Medium** | One screen (likely reusing CE-01's), but needs a new annotation/callout component built from scratch |
| CE-05 Exploration 1 | **Medium** | Requires designing a believable early-stage screen, not just exporting something that already exists, but no annotation or composite work |
| CE-06 Exploration 2 | **Medium** | Same as CE-05 |
| CE-07 Exploration 3 | **Medium** | Same as CE-05, slightly faster since it's closest to the final design and can lean on CE-01's component for reference |
| CE-08 Final Design | **None** | Confirmed 2026-07-02: reuses CE-04's file exactly, no separate export |
| CE-09 Full Flow | **Large** | Multi-panel composite, 3-4 distinct screen states, a new sequence-layout component |

**Total new builds: 9**. Two Large-but-independent assets (CE-01, CE-09), one Large-with-external-dependency asset (CE-03), four Medium, two Small (CE-02, CE-08).

## Recommended build order (not reading order)

Reading order is right for the visitor, it isn't the fastest path through Figma. CE-01 is the foundation every other asset either reuses or is built in reference to, and the three Explorations are easiest derived backward from the finished design while it's fresh in the file.

1. **CE-01 (Hero)** — build first. It establishes the phone-screen component, the type treatment inside the screen, and the backdrop component that the next seven assets all reuse or reference. CE-08 can be exported from the same Figma frame with minimal extra work once CE-01 is done.
2. **CE-04 (Challenge)** — build second, while CE-01's screen is still open. The annotation/callout component built here is also needed later for myBCA's toggle slot, worth getting right early rather than rushing it at the end of this page.
3. **CE-09 (Full Flow)** — build third. It directly extends CE-01 into a sequence, doing it while CE-01's screen and component states are fresh avoids rebuilding the same screen from memory later.
4. **CE-07 → CE-06 → CE-05 (Explorations, in reverse order)** — build the explorations backward from the final design. Exploration 3 is closest to CE-01 and fastest to derive; stripping features back further for Exploration 2, then Exploration 1, is easier than building forward from nothing each time.
5. **CE-02 (Context)** — build anytime, it's fully independent and the fastest single item on the page, a good filler task between the larger builds above, or a quick win to do first if you'd rather warm up on something simple before tackling CE-01.
6. **CE-03 (Landscape)** — build last, or in parallel with everything else if the competitor screenshots can be sourced early. This is the one asset blocked on external material (real CIMB/BLU/myBCA screens), start sourcing that material on day one even if the actual Figma composition happens last.

If you only have time for a partial session, CE-01 alone is the highest-leverage single asset to finish; it gives every subsequent asset its visual reference point, and CE-08 can follow immediately after as a near-free second export from the same frame.
