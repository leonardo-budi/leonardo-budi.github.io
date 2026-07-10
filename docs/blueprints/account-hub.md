# ACCOUNT HUB — PRODUCTION BLUEPRINT

The complete, page-ordered production checklist for `visual-lab/account-hub/index.html`. Built by reading the entire page top to bottom against `IMAGE_ASSETS.md`, `IMAGE_STYLE_GUIDE.md`, and `FIGMA_PRODUCTION_GUIDE.md`. Work this file from AH-01 to AH-07 in Figma.

Sixth and last blueprint of the set, following the structure established in `docs/blueprints/currency-exchange.md`, `mybca.md`, `toko-mama.md`, `homepage.md`, and `aryaduta.md`. Once this document exists, every page in the portfolio has a blueprint.

No HTML modified, no redesign, no images generated. Blueprint only.

---

## Production status

**Not started.** All 7 in-page slots are still CSS gradient placeholders, confirmed via direct inspection of `visual-lab/account-hub/assets/` (empty) and the live HTML (every `.shot-frame` on the page is an empty button with no `<img>` child). This page's `.shot-frame` interaction system and layout were refined and standardized in a prior session (meta grid brought to the sitewide 4-column standard, `.shot-frame` made byte-identical to the canonical component, both More Work cross-link cards wired), but that work was interaction/layout only. **Nothing in this blueprint has been produced yet.**

**Ratio system revised (2026-07-03, same day this blueprint was first written).** Every phone-screen spec below (AH-02 through AH-07) has been updated from the original 393:852 / 786x1704 spec to the newly standardized **Portrait Device Showcase ratio, 9:16, 1350x2400** (`FIGMA_PRODUCTION_GUIDE.md` section 1). The old spec was derived directly from this page's own placeholder CSS; the new system inverts that relationship, every asset is built to one of five approved production ratios first, and the HTML's `aspect-ratio` is updated to match once real assets exist, not the reverse. This is a genuine ratio change (393:852 ≈ 0.4613, 9:16 = 0.5625), not a relabeling. AH-01 (Lead) was already 16:9, 2400x1350, matching the new **Landscape Showcase** ratio exactly, so nothing changes there beyond the name of the category it belongs to.

---

## Before you start: structural facts that shape everything below

**7 image slots, 7 unique production items.** No shared-file case, no composite/multi-state slots, no external sourcing dependency. This is the smallest Gallery-template page (compare: Aryaduta has 22).

**The page is organized into 4 blocks:**

| Block | HTML anchor | Slot type | Count |
|---|---|---|---|
| Lead (page top, before the intro paragraph) | `.lead-wrap` | `.shot-frame.lead` | 1 |
| Before | 1st `.gallery-block` | `.shot-frame.phone` (in `.phone-row`) | 2 |
| Direction One · Personal | 2nd `.gallery-block` | `.shot-frame.phone` (in `.phone-row`) | 2 |
| Direction Two · Minimal | 3rd `.gallery-block` | `.shot-frame.phone` (in `.phone-row`) | 2 |

1 + 2 + 2 + 2 = **7**, confirmed by direct count against the live HTML. The closing "Why two directions" block has no image slot, built entirely from `.gallery-head` copy, same pattern as Aryaduta's own closing-note-equivalent sections.

**No backdrop-tint decision needed**, same as every Gallery page: the final export's mat is a flat `--bg-card` (`#111111`) fill, not a gradient, per the already-locked spec (`FIGMA_PRODUCTION_GUIDE.md` section 8, `IMAGE_STYLE_GUIDE.md` section 4). The green-tinted placeholder gradients currently on the page have no bearing on production.

**Constants for every slot** (stated once rather than repeated 7 times):

- **Approved production ratios**: every asset on this page uses one of the two ratios that apply to Gallery pages, per `FIGMA_PRODUCTION_GUIDE.md` section 1: **Portrait Device Showcase** (9:16, 1350x2400) for every phone screen, and **Landscape Showcase** (16:9, 2400x1350) for the lead image. No custom or page-derived export size is used anywhere on this page.
- **Corner radius**: baked into CSS, not the export (phone 20px, lead 4px). Don't round corners inside the exported file itself.
- **Mat fill**: flat `--bg-card` (`#111111`), matted per `IMAGE_STYLE_GUIDE.md` section 4 (phone: ~4-6% inset margin; lead: ~8-12% inset margin), built directly into the exported canvas.
- **Export format**: WebP (quality ~80-85) per `IMAGE_STYLE_GUIDE.md` section 15, JPEG as fallback pending final format confirmation, same as every other page.
- **Screenshots stay in Nobu's real, proposed UI palette.** Do not re-tint toward the site's lime-on-black system.
- **No device chrome, no shadow, flat-on perspective.**
- **Naming convention**: asset-ID prefix, matching the pattern locked for Currency Exchange/Toko Mama/myBCA/Aryaduta (`ah-01-lead.jpg` through `ah-07-direction-two-variant.jpg`), superseding any older ad hoc filename ever informally discussed for this page.

---

## AH-01 — Lead

**Section**: `.lead-wrap` figure, the first media on the page, before the intro paragraph.
**Purpose**: Establish the fix before any narrative starts. `data-caption`: "Nobu · the proposed account hub." Sets up the hero hook: "This was a proposal to move them into the bottom navigation... and to give the page a clearer shape."
**Filename**: `visual-lab/account-hub/assets/ah-01-lead.jpg`.
**Image or video**: Image.
**Aspect ratio**: 16:9 (Landscape Showcase).
**Export size**: 2400 x 1350px.
**Figma artboard size**: 2400 x 1350px.
**Export format**: WebP (JPEG fallback).
**Production priority**: **Highest.** First image on the page, and the documented future source for the Homepage Explorations card (HP-05) and every currently-blocked cross-link card pointing at Account Hub (see the Homepage-card section below). Producing this one asset unblocks work on three other pages.

**Safe area**: Gallery lead inset, ~8-12% margin on all sides, screen centered on both axes within the mat.

**Composition notes**: The proposed account hub itself, the "after" state this whole case study is building toward, most likely the new Account landing screen once it's been moved into the bottom nav and restructured into clear blocks. This is an establishing shot, not a comparison, the actual before/after contrast is what the next three blocks are for. Since the two directions (Personal, Minimal) haven't been chosen between yet within the case study's own narrative, this lead image should read as a fair, direction-agnostic representation of "the account hub, fixed," not visually pre-committing to either direction. If that's not achievable in one frame, use whichever direction reads more neutral as the establishing shot (the Personal direction, since it's presented first in the page's own reading order, is the more defensible default).

**Reuse opportunities**: Source for the Homepage's "Other Explorations" Account Hub card (HP-05, needs a dedicated 3:2 re-export, not a crop, see the Homepage-card section below). Also the documented source for Aryaduta's own "→ Account Hub" more-work cross-link card, which is currently blocked for the same reason (`docs/blueprints/aryaduta.md`, Cross-link section).

---

## Before (AH-02, AH-03)

**Section**: 1st `.gallery-block`, `.phone-row` of 2 screens.
**Belongs to**: "Account settings opened from a slide-out drawer, the kind you only find if you already know it's there. Useful things sat one hidden gesture away, grouped together without much order."
**Type**: Gallery phone, both.

| ID | Screen (caption) | Filename | Notes |
|---|---|---|---|
| AH-02 | Existing home | `ah-02-before-home.jpg` | The current home screen, deliberately showing **no visible entry point** into account settings, matching the caption's own point ("no clear way into the account"). Don't accidentally include an obvious account affordance here, the whole point of this image is the absence. |
| AH-03 | The slide-out drawer | `ah-03-before-drawer.jpg` | The drawer open, overlaid on the home screen, showing the existing account-adjacent items "grouped together without much order" per the section copy. A single static frame with the drawer already open is sufficient; see the MP4 note below for a borderline alternative. |

**Composition notes**: Single screen per frame, matted at ~4-6% inset, centered on both axes, per the Gallery phone rule. **AH-03 is this page's one borderline MP4 candidate**, flagged explicitly rather than defaulted past: a slide-out drawer is inherently a motion-based UI pattern, and the site's established MP4 rule (`FIGMA_PRODUCTION_GUIDE.md` section 6) is "any asset demonstrating a flow or interaction." However, unlike Toko Mama's Friction/Outcome sections, this page's copy never explicitly narrates the *motion itself* as the point, it describes the drawer's *discoverability problem* ("discoverable only if you knew to look"), which a single static frame of the open drawer already communicates. **Default recommendation: JPG, single state.** See the "MP4 vs. JPG" section below for the full reasoning and how to override this if Leo wants to show the actual slide-in gesture.

**Aspect ratio**: 9:16 (Portrait Device Showcase) for both. **Figma artboard / export size**: 1350 x 2400px.

---

## Direction One · Personal (AH-04, AH-05)

**Section**: 2nd `.gallery-block`, `.phone-row` of 2 screens.
**Belongs to**: "The entry point moves into the bottom navigation, where your thumb already rests, and the page is rebuilt as clear blocks: Account, Security, and the rest. This direction leans personal, leading with the member's name, photo, and tier so the page feels like theirs."
**Type**: Gallery phone, both.

| ID | Screen (caption) | Filename | Notes |
|---|---|---|---|
| AH-04 | Account in the bottom nav | `ah-04-direction-one-nav.jpg` | Shows the new bottom-nav entry point itself (an Account tab now present where it wasn't before), plus the restructured page underneath, organized into clear blocks (Account, Security, and the rest, per the copy). This is the structural fix, independent of visual tone. |
| AH-05 | Personal direction | `ah-05-direction-one-personal.jpg` | The same restructured page, but in its "personal" visual treatment: leads with the member's name, photo, and tier at the top of the page, per the copy's own description. This is the tonal choice, distinct from AH-04's structural one. |

**Composition notes**: AH-04 and AH-05 should likely be understood as two views of the *same underlying screen*, one emphasizing the new nav entry point, one emphasizing the personal visual identity at the top of the page, rather than two unrelated screens. Worth building from one shared base component so the two stay visually consistent with each other (same nav bar, same block structure) while differing only in what each frame chooses to foreground.

**Aspect ratio**: 9:16 (Portrait Device Showcase) for both. **Figma artboard / export size**: 1350 x 2400px.

---

## Direction Two · Minimal (AH-06, AH-07)

**Section**: 3rd `.gallery-block`, `.phone-row` of 2 screens.
**Belongs to**: "The same structure and the same bottom-nav entry, in a quieter style. Less expressive, more restrained, for a version that stays out of the way and lets the actions lead."
**Type**: Gallery phone, both.

| ID | Screen (caption) | Filename | Notes |
|---|---|---|---|
| AH-06 | Minimal direction | `ah-06-direction-two-minimal.jpg` | The same bottom-nav entry and same block structure as Direction One, but restrained: no personal-identity lead, quieter typography/color treatment, "lets the actions lead" per the copy. |
| AH-07 | Minimal variant | `ah-07-direction-two-variant.jpg` | "Same blocks, lighter visual treatment," per the caption. A second state of the minimal direction, likely a secondary settings block, a scrolled state, or a different section of the same restructured page shown in the same quiet visual language as AH-06. |

**Composition notes**: This block is explicitly the **same underlying structure as Direction One**, only the visual tone changes ("The same fix, stripped back"). AH-06/AH-07 should reuse the exact same page structure and block arrangement built for AH-04/AH-05, differing only in typography weight, color intensity, and how much personal/identity content is foregrounded. Building Direction One first and deriving Direction Two from it directly (rather than designing both from scratch independently) is the most efficient path and the one most likely to make the two directions read as a fair, consistent comparison rather than two different apps.

**Aspect ratio**: 9:16 (Portrait Device Showcase) for both. **Figma artboard / export size**: 1350 x 2400px.

---

## Which assets should become MP4, which should remain JPG

**All 7 assets are recommended as JPG (WebP export, JPEG fallback).** No slot on this page has copy that explicitly narrates a demonstrated interaction or multi-step flow the way Toko Mama's Friction (`tm-03-friction.mp4`) and Outcome (`tm-05-outcome.mp4`) sections do. The page's own narrative is a structural and tonal comparison (before vs. after, personal vs. minimal), which single static frames communicate cleanly.

**One borderline case, flagged rather than silently decided**: AH-03 (the slide-out drawer). A drawer is inherently a motion-based UI element, and the sitewide MP4 rule (`FIGMA_PRODUCTION_GUIDE.md` section 6) technically qualifies "any asset demonstrating a flow or interaction." If Leo wants to actually show the drawer sliding open, rather than a single static frame of it already open, this would become `ah-03-before-drawer.mp4`, following the established MP4 pattern (`autoplay muted loop playsinline`, wrapped in `.shot-frame`). **If chosen, export it at the Portrait Device Showcase ratio (9:16, 1350x2400), not the Motion category's 16:9 default** (`FIGMA_PRODUCTION_GUIDE.md` section 1a): AH-03's subject is a single portrait phone screen, and forcing that recording into a 16:9 canvas would mean padding a portrait screen inside a landscape mat, breaking Gallery's "flat mat, real screen aspect" philosophy. This is the one documented exception to Motion's default ratio, and AH-03 is its first live candidate. **Default recommendation remains JPG** since the section's copy is about the drawer's poor discoverability, not its motion, and a static frame already makes that point. This is a judgment call for Leo to confirm before AH-03 is built, not a decision this blueprint makes unilaterally.

---

## Which assets can reuse existing components

No asset on this page reuses another page's *file* (no shared-file case like Currency Exchange's CE-04/CE-08). But several assets should share the same underlying Figma *components* rather than being built independently from scratch:

- **AH-04 and AH-05** should share one base screen structure (same nav bar, same block layout), differing only in which content each frame foregrounds (nav entry point vs. personal identity).
- **AH-06 and AH-07** should be derived directly from AH-04/AH-05's structure, restyled to the minimal tone, rather than designed independently. This is the same "shared structure, different skin" relationship already established between myBCA's MB-02/MB-03 composite pairs.
- **The Gallery phone-inset and lead-inset mat components** (already built once for Account Hub's earlier interaction work, or for Aryaduta if that's produced first) should be reused here rather than rebuilt, per `IMAGE_STYLE_GUIDE.md` section 11's "one continuous system" rule across both Gallery pages.

---

## Which Homepage card will eventually be needed (3:2)

**HP-05, the Homepage's "Other Explorations → Account Hub" card**, currently blocked (`docs/blueprints/homepage.md`, `MASTER_ASSET_TRACKER.md`). Per the same pattern already used for Currency Exchange/Toko Mama/myBCA's own homepage cards (`hp-ce-card.jpg`, `hp-tm-card.jpg`, `hp-mb-card.jpg`): once AH-01 is produced, export a **dedicated 3:2 canvas directly from AH-01's Figma composition** (2400 x 1600px), not a pixel-crop of the flattened 16:9 JPG, since cropping a 1350px-tall image up to a 1600px-tall canvas would force an upscale. Recommended filename: `hp-ah-card.jpg`, stored at `assets/images/` (repo root), matching the flat, project-prefixed convention already established for the other three homepage cards.

This single new export also unblocks two other currently-placeholder cross-link cards that are documented as reusing Account Hub's own lead image (not this dedicated homepage-card export, a separate file): Aryaduta's own "→ Account Hub" more-work card (see `docs/blueprints/aryaduta.md`), which should reuse `hp-ah-card.jpg` directly once it exists, the same way every other cross-link card on the site reuses a homepage card rather than sourcing its own crop.

**No other Rail page currently links to Account Hub.** Confirmed by direct inspection: none of Currency Exchange's, Toko Mama's, or myBCA's "more work" sections reference Account Hub at all (their cross-link cards point only at each other, plus Currency Exchange's still-blocked "→ Aryaduta" card). So `hp-ah-card.jpg` has exactly two consumers once produced: the Homepage's own HP-05 slot, and Aryaduta's "→ Account Hub" card.

---

## Effort estimate

| Block | Count | Effort | Why |
|---|---|---|---|
| AH-01 Lead | 1 | Medium | First impression of the case study, and the single highest-leverage asset on this page since it unblocks two other pages |
| Before (AH-02, AH-03) | 2 | Small each | Simple, single-state screens; AH-03 needs a scope decision (JPG vs. MP4) before it's finalized, but the JPG version itself is simple |
| Direction One (AH-04, AH-05) | 2 | Medium each | Establishes the shared base structure that Direction Two derives from, worth extra care here since it isn't just for these two screens |
| Direction Two (AH-06, AH-07) | 2 | Small each | Derived directly from Direction One's structure, restyled, not designed from scratch |

**Total new builds: 7.** The smallest Gallery-template page (compare: Aryaduta's 22), a fast page to complete once picked up.

## Recommended production order

1. **AH-01 (Lead)** first. Highest priority, unblocks the Homepage card and Aryaduta's cross-link card the moment it's done, and sets the visual bar for the account hub's "after" state that the rest of the page builds toward.
2. **Direction One (AH-04, AH-05)** next, not Before. Building the primary recommended direction's shared base structure early means Direction Two (which explicitly derives from it) and the Before block (which needs to visually contrast against *something* already-built) both have a stable reference to work against.
3. **Direction Two (AH-06, AH-07)**, derived directly from Direction One's structure.
4. **Before (AH-02, AH-03)** last. Reading order puts this block first on the page, but production-wise it benefits from being built last, once the "after" state (Directions One and Two) exists, so the contrast the section is making ("no clear way in" vs. "clear blocks, thumb-reachable") can be judged against a finished reference rather than guessed at in isolation.

Before starting AH-03, confirm the JPG-vs-MP4 scope question above with Leo (see "MP4 vs. JPG" section), since it's the one open production decision on this page.

---

## Summary

- **Total media slots on the page**: 7 in-page (1 lead + 6 phone) + 2 already-implemented cross-link cards (not Account Hub production items, both wired in a prior session, reusing `hp-ce-card.jpg`/`hp-tm-card.jpg`).
- **Total unique assets to produce**: 7 (all recommended as JPG; AH-03 is one open MP4-vs-JPG judgment call for Leo).
- **Total reused assets**: 0 inbound. 1 outbound once produced: AH-01 is the documented future source for `hp-ah-card.jpg` (a dedicated 3:2 re-export, new file, not a crop), which in turn is the source for HP-05 and Aryaduta's "→ Account Hub" card.
- **Recommended production order**: AH-01 → Direction One → Direction Two → Before.

## Implementation checklist

- [ ] Confirm the AH-03 JPG-vs-MP4 scope question with Leo before finalizing that asset
- [ ] Build/reuse the Gallery phone-inset mat component (~4-6% margin, `--bg-card` fill)
- [ ] Build/reuse the Gallery lead-inset mat component (~8-12% margin, `--bg-card` fill)
- [ ] Produce AH-01 — Lead (`ah-01-lead.jpg`)
- [ ] Produce AH-04, AH-05 — Direction One · Personal, establishing the shared base screen structure
- [ ] Produce AH-06, AH-07 — Direction Two · Minimal, derived from Direction One's structure
- [ ] Produce AH-02, AH-03 — Before (JPG or MP4 per the confirmed scope decision)
- [ ] Verify all 6 phone exports are 1350x2400 (9:16, Portrait Device Showcase), the lead export is 2400x1350 (16:9, Landscape Showcase)
- [ ] Once AH-01 is delivered, produce `hp-ah-card.jpg` (2400x1600, 3:2) as a dedicated re-export, not a crop
- [ ] Update `IMAGE_ASSETS.md` and `MASTER_ASSET_TRACKER.md` once assets are delivered
- [ ] Wire into HTML only after Leo confirms each export (no HTML changes made as part of this blueprint); the `.shot-frame` interaction system on this page is already standardized and ready to receive real `<img>`/`<video>` tags without further CSS/JS changes
- [ ] Once `hp-ah-card.jpg` exists, revisit the two blocked cards that depend on it: the Homepage's HP-05 slot and Aryaduta's "→ Account Hub" more-work card
