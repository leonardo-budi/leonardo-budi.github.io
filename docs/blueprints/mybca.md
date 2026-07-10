# MYBCA — PRODUCTION BLUEPRINT

The complete, page-ordered production checklist for `study-case/mybca/index.html`. Built by reading the entire page top to bottom against `IMAGE_ASSETS.md`, `IMAGE_STYLE_GUIDE.md`, and `FIGMA_PRODUCTION_GUIDE.md`. Work this file from MB-01 to MB-03 in Figma.

Second blueprint of the set, following the structure established in `docs/blueprints/currency-exchange.md` (reading-order checklist, then a resequenced build order). The same structure should repeat for Toko Mama, Account Hub, and Aryaduta once this one is in use.

No HTML modified, no redesign, this only maps what already exists into a build sequence. Blueprint only, no images generated here.

---

## Production status

**Not started.** All 3 assets are still CSS gradient placeholders. This is the smallest of the three Rail pages (Currency Exchange has 9, Toko Mama has 3, myBCA has 3), a fast page to complete once picked up.

---

## Before you start: one structural fact that shapes everything below

The page has **3 image slots and 3 unique production items.** Unlike Currency Exchange, there is no shared-file case here, every slot needs its own export. Two of the page's five rail sections (02 Evidence, 03 Tension) have no image slot at all, they're built entirely from the `.stat-row` survey-stat blocks and `.reflection` quote callouts, both pure CSS/typography components with no image dependency. Section 05 (Outcome) likewise has no image, closing the page on an `.info-stack` and a final `.reflection` quote. The two "More work" cross-link thumbnails at the bottom of the page are not myBCA production items, they reuse Currency Exchange's and Toko Mama's own card thumbnails, produced as part of those pages' own work.

All 3 items below are 16:9 Rail frames (`FIGMA_PRODUCTION_GUIDE.md` section 1), so artboard, export size, and format are identical across every item, only composition, content, and background tint vary. Those constants are stated once here rather than repeated three times:

- **Aspect ratio**: 16:9
- **Figma artboard**: 2400 x 1350px
- **Export size**: 2400 x 1350px (already 2x of the ~1200-1300px max in-page display width)
- **Export format**: WebP (quality ~80-85), JPEG as fallback pending final format confirmation
- **Corner radius**: none, sharp rectangle (Rail template, `IMAGE_STYLE_GUIDE.md` section 1)
- **Naming convention**: asset-ID prefix, matching the pattern locked for Currency Exchange (`ce-01-hero.jpg` etc.), so `mb-01-hero.jpg` through `mb-03-toggle.jpg` (`FIGMA_PRODUCTION_GUIDE.md` section 4)

**One open question flagged for Leo, not resolved here**: `IMAGE_STYLE_GUIDE.md` section 13 flags myBCA's blue-tinted placeholder gradients (`.ts-hero`/`.ts-sec`/`.ts-alt` all in the same blue family) as very likely an accidental inconsistency rather than an intentional per-client brand tint, since no other page has a per-project tint convention and the style guide recommends collapsing all three Rail pages' backdrops to the same neutral dark tone. `FIGMA_PRODUCTION_GUIDE.md` section 8, by contrast, currently locks in the blue gradients as myBCA's literal production backdrop (matching what's live in the CSS today). This blueprint follows `FIGMA_PRODUCTION_GUIDE.md`'s locked numbers below since that's the authoritative production spec, but the discrepancy is worth Leo's explicit confirmation before MB-01 is built, since it's cheaper to settle once than to re-export three backdrops later.

---

## MB-01 — Hero

**HTML section**: `.case-hero` figure, immediately after the case-meta grid, before the rail begins. First image on the page.
**Position**: 1st image encountered, above the fold for most viewports.
**Belongs to**: The page hero, not numbered in the rail (sits before section 01 Gap).
**Type**: Hero.

**Purpose**: Show the screen the whole case study is about, before any narrative starts. Caption: "myBCA · Transfer to BCA Account, the screen with no balance." Pairs with the hook copy: "When you're about to send money, you need to know you have enough. myBCA's transfer screen didn't show your balance."

**UI screens that should appear**: The myBCA transfer-to-BCA-account screen, in its current, real, no-balance state, exactly as the caption names it. This is establishing the problem, not the fix, the fix doesn't appear until MB-03.

**Emphasize**: The transfer amount field and the destination account, the two things a user is filling in while having no balance reference anywhere on screen. The absence of a balance display is the entire point of this image, don't accidentally imply one exists.

**Omit**: OS status bar, home indicator, keyboard, any nav chrome not load-bearing for this screen.

**Composition**: Portrait phone screen centered on the 16:9 canvas, both axes. Screen occupies ~78-85% of canvas height, backdrop fills the rest, split evenly top and bottom. Width follows the phone's real aspect ratio, most of the canvas width stays backdrop on purpose. Identical system to Currency Exchange's CE-01 (`FIGMA_PRODUCTION_GUIDE.md` section 7).

**Safe area**: Keep the phone and all its content within the central 65% of canvas width. Leave a minimum 5% clear backdrop margin on every edge.

**Background treatment**: `linear-gradient(135deg, #04132e 0%, #0a3a6b 45%, #050d1c 100%)`, the locked myBCA `.ts-hero` gradient (`FIGMA_PRODUCTION_GUIDE.md` section 8). **Plus the two decorative radial highlights**: lime at 8% opacity centered ~30%/30%, lime at 4% opacity centered ~75%/70%, same hero-only treatment as every other Rail hero on the site.

**Filename**: `study-case/mybca/assets/mb-01-hero.jpg`.

**Reuses a Figma master component?** Yes, the Rail backdrop component, **hero variant** (with glow), same component family as Currency Exchange's, just myBCA's blue color style instead of green. Build the myBCA-blue hero-variant swatch here first, since it's needed here and nowhere else on this page.

---
↓
---

## MB-02 — Gap (Transfer Screen + Insufficient-Balance Error)

**HTML section**: `#gap` (rail 01).
**Position**: 2nd image, first one inside the rail-numbered narrative.
**Belongs to**: "A small gap, but a real one." The section that establishes the friction: no balance shown, so users guess, and sometimes guess wrong.
**Type**: **Two-state composite** (a deliberate exception to the single-device default, see note below).

**Purpose**: Make the consequence of the missing balance concrete. Caption: "The transfer screen, and the error you hit when the guess is wrong." The body copy explicitly describes two moments: "Guess too high and the app stops you with an insufficient-balance error, after you've already filled everything in."

**UI screens that should appear**: Two states of the same transfer flow: (1) the transfer screen with an amount typed in, and (2) the insufficient-balance error that appears when that guess exceeds the real balance. Both need to be visible in one frame per the caption's own "and" construction, this isn't an either/or choice between the two states.

**Emphasize**: The error state specifically, since it's the moment the copy is building toward ("a small interruption, but one that happens before you've sent a single rupiah"). The first (pre-error) state should read as clearly antecedent to the second, not as two unrelated screens.

**Omit**: OS chrome, keyboard (unless the keyboard is load-bearing for showing the amount was actively being typed, a production judgment call). Don't show a successful transfer completion, that's out of scope for this section.

**Composition**: Two phone screens side by side (or a before/after split within one frame), following the same visual grammar as MB-03's before/after treatment below, so the two composite slots on this page feel like one family rather than two different systems. Scale each phone so both fit within the safe area while each individually stays legible.

**Safe area**: Central 70% of canvas width for the pair, minimum 6% margin from every canvas edge (slightly more generous than a single-phone slot, to keep the pair from feeling cramped).

**Background treatment**: `linear-gradient(135deg, #06182f 0%, #0c3a66 50%, #050f1e 100%)`, the locked myBCA `.ts-sec` gradient. No glow, this is a section shot, not a hero.

**Filename**: `study-case/mybca/assets/mb-02-gap.jpg`.

**Reuses a Figma master component?** Backdrop reuses the section-variant component (myBCA blue). The **two-state composite layout is new**, but should share its underlying structure with MB-03's before/after treatment (two panels, one narrative beat) rather than being built as a one-off, since both are the page's only two multi-state slots.

**Production dependency, flag before starting**: `IMAGE_ASSETS.md` flagged this as possibly needing to be confirmed as a two-state composite rather than a single screen before producing. This blueprint resolves that question: yes, two states, per the caption's own wording ("the transfer screen, **and** the insufficient-balance error").

---
↓
---

## MB-03 — Toggle (Before/After, Balance Hidden and Revealed)

**HTML section**: `#toggle` (rail 04).
**Position**: 3rd and last image on the page.
**Belongs to**: "Giving users control through a toggle." The payoff section, showing the actual fix.
**Type**: **Before/after composite** (confirmed in `IMAGE_STYLE_GUIDE.md` as one of only two annotated/multi-state slots in the entire site, alongside Currency Exchange's Challenge section).

**Purpose**: Show the fix working, not just describe it. Caption: "Existing screen, hidden by default, and revealed with one tap." The copy is explicit about the mechanism: "The balance is hidden by default, masked as IDR followed by dots... One tap reveals the full amount, and one tap hides it again," and explicit that this is not a redesign: "I didn't redesign the screen. The balance sits inside the existing Source Account card."

**UI screens that should appear**: Two states of the same Source Account card: (1) balance masked, "IDR" followed by dots, nothing sensitive visible, and (2) balance revealed, the full amount showing, after the tap. Both states should be the *same* screen otherwise, only the balance field differs, reinforcing the copy's "I didn't redesign the screen" claim. The list beneath the image (`.case-list`) names the same three points, so the image needs to make all three legible: hidden by default, one-tap reveal, placed inside the existing Source Account card (not a new component).

**Emphasize**: The Source Account card specifically, and the visual contrast between masked and revealed states. A small indicator of "this is tappable" (matching the real product's actual affordance, whatever that is) helps sell that this is an interaction, not two unrelated screenshots.

**Omit**: Don't show the full transfer flow around the card, this is a tight, card-level before/after, not a full-screen narrative like MB-02's two-state composite. Don't invent a third state (for example a mid-tap transition), two states is the spec.

**Composition**: Two phone screens (or two card-level crops) side by side, before state on the left, after state on the right, reading left-to-right the same direction as the "one tap reveals" narrative. Same underlying two-panel system as MB-02, so the two composite slots on this page read as one family.

**Safe area**: Central 70% of canvas width for the pair, minimum 6% margin from every canvas edge, same numbers as MB-02.

**Background treatment**: `linear-gradient(135deg, #0a2747 0%, #14528c 50%, #07182b 100%)`, the locked myBCA `.ts-alt` gradient (this slot's CSS class is `.ts-sec.ts-alt`, the page's amber-equivalent variant, myBCA's version is a brighter blue rather than Currency Exchange's amber). No glow.

**Filename**: `study-case/mybca/assets/mb-03-toggle.jpg`.

**Reuses a Figma master component?** Backdrop reuses the alt-variant component (myBCA blue). Shares its two-panel composite structure with MB-02, build that shared component once and reuse it for both rather than building two different before/after systems.

**Production note for whoever implements this into HTML later**: the `.case-list` immediately below this image (three bullet points: hidden by default, one-tap reveal, placed in the existing card) should probably stay full column width, matching the image, rather than being constrained to the narrower `.case-body` reading measure. Currency Exchange went through exactly this back-and-forth (see `SESSION_LOG.md`, 2026-07-01 entries): lists that sit directly beneath a full-width image read better as part of that image's wide "editorial breakpoint" than snapped back into the prose column. Decide this once, consistently, rather than rediscovering it here.

---

## Effort estimate per asset

| Asset | Effort | Why |
|---|---|---|
| MB-01 Hero | **Medium** | Standard single-phone composed slide, but establishes the myBCA-blue hero-variant component from scratch (nothing to inherit from Currency Exchange's green family) |
| MB-02 Gap | **Medium** | Two-state composite, but a simpler narrative pairing (screen → error) than MB-03's tap-interaction pairing |
| MB-03 Toggle | **Medium** | Two-state composite, the page's payoff image, needs the masked/revealed contrast to read clearly at filmstrip-adjacent sizes |

**Total new builds: 3.** No Small or Large outliers, no external sourcing dependency (unlike Currency Exchange's CE-03), no annotation-with-callout-lines work (unlike Currency Exchange's CE-04). This is the most contained page of the three Rail case studies.

## Recommended build order

Reading order already is the efficient order here, there's no CE-01-style reused asset and no external dependency to front-load.

1. **MB-01 (Hero)** — build first. Establishes the myBCA-blue hero-variant backdrop component that nothing else on this page needs again, but that Toko Mama's own blueprint (if it shares any color-family decisions) may reference later.
2. **MB-02 (Gap)** — build second. Establishes the two-panel before/after composite component this page needs twice.
3. **MB-03 (Toggle)** — build third, reusing MB-02's two-panel component directly. Since it's the payoff image, worth a final pass making sure the masked/revealed contrast reads clearly at both full size and filmstrip-adjacent scale before calling the page done.

Before starting MB-01, confirm the flagged backdrop-tint question (myBCA blue vs. collapsing to the same neutral tone as Currency Exchange/Toko Mama) with Leo, since it affects all three assets identically and is cheaper to settle once than to redo later.

---

## Summary

- **Total image slots**: 3 in-page (Hero, Gap, Toggle) + 2 reused cross-link cards (not myBCA production items).
- **Total unique assets to produce**: 3.
- **Suggested production order**: MB-01 → MB-02 → MB-03 (reading order, no resequencing needed).

## Implementation checklist

- [ ] Confirm the backdrop-tint question (myBCA blue vs. neutral) with Leo before building
- [ ] Build the myBCA-blue hero-variant Rail backdrop component (with glow)
- [ ] Build the myBCA-blue section-variant Rail backdrop component (no glow)
- [ ] Build the shared two-panel before/after composite component (used by both MB-02 and MB-03)
- [ ] Produce MB-01 — Hero (`mb-01-hero.jpg`)
- [ ] Produce MB-02 — Gap, two-state composite (`mb-02-gap.jpg`)
- [ ] Produce MB-03 — Toggle, before/after composite (`mb-03-toggle.jpg`)
- [ ] Verify all 3 exports are 2400x1350, correct 16:9
- [ ] Confirm masked/revealed contrast in MB-03 reads clearly at reduced size, not just at full export size
- [ ] Update `IMAGE_ASSETS.md` status column once files are delivered
- [ ] Wire into HTML only after Leo confirms each export (no HTML changes made as part of this blueprint)
- [ ] Decide the `.case-list`-width question for MB-03 (see production note above) before wiring, rather than rediscovering it mid-implementation
