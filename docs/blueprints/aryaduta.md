# ARYADUTA — PRODUCTION BLUEPRINT

The complete, page-ordered production checklist for `visual-lab/aryaduta/index.html`. Built by reading the entire page top to bottom against `IMAGE_ASSETS.md`, `IMAGE_STYLE_GUIDE.md`, and `FIGMA_PRODUCTION_GUIDE.md`. Work this file from AR-01 to AR-22 in Figma.

Fifth blueprint of the set, following the structure established in `docs/blueprints/currency-exchange.md`, `mybca.md`, `toko-mama.md`, and `homepage.md`. This is the last page without a blueprint; once this document exists, every page in the portfolio has one.

No HTML modified, no redesign, no images generated. Blueprint only.

---

## Production status

**Not started.** All 22 in-page slots are still CSS gradient placeholders, confirmed via direct inspection of `visual-lab/aryaduta/assets/` (empty) and the live HTML (every `.shot-frame` on the page is an empty button with no `<img>` child). By a wide margin, this is the largest asset count of any page in the portfolio: Currency Exchange has 9, Toko Mama has 5, myBCA has 3, Account Hub has 7, Aryaduta has 22.

**Scope confirmed (2026-07-03).** `IMAGE_ASSETS.md` had flagged since 2026-06-30 that this page carries the largest production cost for the lowest individual hiring weight (a self-initiated pitch concept, `Status: Pitch Concept`), and recommended a scope conversation before committing to all 17 phone screens. That conversation happened: Leo confirmed **all 22 assets proceed as planned**, full 5-block structure, no trimming. The scope-conversation flag is resolved; the rest of this document reflects the full build.

**Ratio system revised (2026-07-03, same day).** Every phone-screen spec below (AR-02 through AR-18) has been updated from the old 393:852 / 786x1704 spec to the newly standardized **Portrait Device Showcase ratio, 9:16, 1350x2400** (`FIGMA_PRODUCTION_GUIDE.md` section 1). The old spec was derived from the HTML's own current placeholder CSS; the new system inverts that, every asset is built to one of five approved production ratios, and the HTML is updated to match once real assets exist. This is a genuine ratio change (393:852 ≈ 0.4613, 9:16 = 0.5625), not a relabeling. Lead and wide slots (AR-01, AR-19–22) were already 16:9, 2400x1350, matching the new **Landscape Showcase** ratio exactly, so nothing changes for those 5 assets beyond the name of the category they belong to.

---

## Before you start: structural facts that shape everything below

**22 image slots, 22 unique production items.** No shared-file case like Currency Exchange's CE-01/CE-08 exists on this page, and no cross-link "more work" card counts against this total (those reuse other pages' own thumbnails, or remain blocked, see the Cross-link section at the end).

**The page is organized into 5 blocks**, each a `.gallery-block` section:

| Block | HTML anchor | Slot type | Count |
|---|---|---|---|
| Lead (page top, before the intro paragraph) | `.lead-wrap` | `.shot-frame.lead` | 1 |
| Guest Experience App | 1st `.gallery-block` | `.shot-frame.phone` (in `.phone-row`) | 5 |
| The Guest Request Flow | 2nd `.gallery-block` | `.shot-frame.phone` (in `.phone-row`) | 6 |
| The Staff Task Board | 3rd `.gallery-block` | `.shot-frame.phone` (in `.phone-row`) | 6 |
| Receptionist Command Center | 4th `.gallery-block` | `.shot-frame.wide` (in `.wide-grid`) | 4 |

1 + 5 + 6 + 6 + 4 = **22**, confirmed by direct count against the live HTML. The closing "Why two directions"-equivalent block (here, none exists as a distinct section; the page moves straight from Receptionist Command Center into More Work) has no image slot, consistent with the other Gallery page.

**Unlike the Rail pages, there is no backdrop-tint decision to make here.** Currency Exchange, Toko Mama, and myBCA's placeholder gradients are literally baked into their final production exports (the gradient *is* the shipped backdrop). Gallery frames work differently: per `FIGMA_PRODUCTION_GUIDE.md` section 8 and `IMAGE_STYLE_GUIDE.md` section 4, the final export's mat is a **flat `--bg-card` (`#111111`) fill, no gradient**, identical across every Gallery frame on both Account Hub and Aryaduta. The amber-tinted gradients currently visible on this page (`.shot-frame.phone/.wide/.lead` backgrounds, `#1c1208`/`#2e1f0c` family) are placeholder-only art with no bearing on the real export, they exist purely so an empty button isn't a dead black rectangle before production. No open question to flag or resolve here, unlike the Rail pages' green/blue tint discrepancy.

**Constants for every slot** (stated once rather than repeated 22 times):

- **Approved production ratios**: every asset on this page uses one of the two ratios that apply to Gallery pages, per `FIGMA_PRODUCTION_GUIDE.md` section 1: **Portrait Device Showcase** (9:16, 1350x2400) for every phone screen, and **Landscape Showcase** (16:9, 2400x1350) for the lead image and the Receptionist Command Center's wide screens. No custom or page-derived export size is used anywhere on this page.
- **Corner radius**: baked into CSS, not the export (phone 20px, wide 12px, lead 4px). Per `FIGMA_PRODUCTION_GUIDE.md` section 8, don't round corners inside the file itself.
- **Mat fill**: flat `--bg-card` (`#111111`), matted per `IMAGE_STYLE_GUIDE.md` section 4 (phone: ~4-6% inset margin; lead/wide: ~8-12% inset margin), built directly into the exported canvas.
- **Export format**: WebP (quality ~80-85) per `IMAGE_STYLE_GUIDE.md` section 15, JPEG as fallback pending final format confirmation, same as every other page.
- **Screenshots stay in the product's real, proposed UI palette.** Do not re-tint toward the site's lime-on-black system (`IMAGE_STYLE_GUIDE.md` section 6, "truthful over impressive").
- **No device chrome, no shadow, flat-on perspective**, same rule as every other page in the site.
- **Naming convention**: asset-ID prefix, matching the pattern locked for Currency Exchange/Toko Mama/myBCA (`FIGMA_PRODUCTION_GUIDE.md` section 4). This **supersedes** the older `aryaduta-guest-home.jpg`-style filenames still listed in `IMAGE_ASSETS.md` today, those predate the asset-ID convention (locked 2026-07-01, after `IMAGE_ASSETS.md`'s Aryaduta section was last written) and should be updated to match once this blueprint is adopted.

---

## AR-01 — Lead

**HTML section**: `.lead-wrap` figure, the first media on the page, before the intro paragraph.
**Position**: 1st image, above the fold for most viewports.
**Type**: Gallery lead.

**Purpose**: Establish the whole concept in one image before any narrative starts. `data-caption`: "Aryaduta · Guest Experience App." Sets up the intro paragraph's framing: "A pitch concept spanning three roles in one service loop."

**UI screens that should appear**: The Guest Experience App's most representative screen (likely its Home screen, since that's the natural establishing shot for an app the reader hasn't seen yet), shown large and matted, not a montage of all three roles. The three-role structure is explained by the copy immediately below, not by this image, this image's job is just to make the guest app itself feel real and considered before the filmstrips start.

**Emphasize**: Whatever visual identity choice best signals "hospitality, guest-facing, premium hotel," since this is the reader's very first impression of the whole case study.

**Omit**: OS chrome, keyboard, any of the staff or receptionist interfaces, those get their own sections below.

**Composition**: Single phone screen (or a phone screen with light surrounding editorial context, e.g. an in-hand or on-a-nightstand framing, if that reads better matted at 16:9 than a bare screen floating in empty mat, a production judgment call) centered within the lead mat, ~8-12% inset per the Gallery lead rule.

**Filename**: `visual-lab/aryaduta/assets/ar-01-lead.jpg`.
**Aspect ratio**: 16:9 (Landscape Showcase). **Figma artboard / export size**: 2400 x 1350px.
**Reuse**: None in-page. Flagged in `IMAGE_ASSETS.md` as the likely source for Aryaduta's homepage Explorations card and its own cross-link thumbnails (see Cross-link section below), recropped to 3:2, once produced.

---

## Guest Experience App (AR-02 through AR-06)

**HTML section**: 1st `.gallery-block`, `.phone-row` of 5 screens.
**Belongs to**: "Led end to end with a junior designer, from mapping the service flow to finalizing the screens. Check-in, a digital room key, and post-stay feedback in one place."
**Type**: Gallery phone, all 5.

| ID | Screen (caption) | Filename | Notes |
|---|---|---|---|
| AR-02 | Home | `ar-02-guest-home.jpg` | Establishing screen for the guest app; if AR-01 already uses this screen, AR-02 should show a distinct crop/state so the filmstrip doesn't repeat the lead image verbatim |
| AR-03 | My Stays | `ar-03-guest-my-stays.jpg` | Booking/reservation list view |
| AR-04 | Room Detail | `ar-04-guest-room-detail.jpg` | Single-stay detail, likely the screen that surfaces the digital key entry point |
| AR-05 | Digital Key | `ar-05-guest-digital-key.jpg` | The digital room key itself, a strong visual anchor for this section, worth extra polish since "digital room key" is explicitly named in the section's own description copy |
| AR-06 | Feedback | `ar-06-guest-feedback.jpg` | Post-stay feedback capture, closes the loop this section's copy describes |

**Composition**: Single phone screen per frame, matted at ~4-6% inset, centered on both axes, per the Gallery phone rule. No two-state composites in this block, each of the 5 is a single screen.

**Aspect ratio**: 9:16 (Portrait Device Showcase) for all 5. **Figma artboard / export size**: 1350 x 2400px.

---

## The Guest Request Flow (AR-07 through AR-12)

**HTML section**: 2nd `.gallery-block`, `.phone-row` of 6 screens.
**Belongs to**: "A seamless interface for in-room dining and amenity requests, from menu to confirmation in a few taps."
**Type**: Gallery phone, all 6.

| ID | Screen (caption) | Filename | Notes |
|---|---|---|---|
| AR-07 | Choose Request | `ar-07-request-choose.jpg` | Entry point into the flow, likely a category picker (food, housekeeping, etc.) |
| AR-08 | Food & Beverage | `ar-08-request-food-beverage.jpg` | Menu browsing state |
| AR-09 | Item Detail | `ar-09-request-item-detail.jpg` | Single menu item, distinct from AR-14's staff-facing "Request Detail," name deliberately disambiguated in this blueprint's filenames to avoid confusion between the two |
| AR-10 | Order Summary | `ar-10-request-order-summary.jpg` | Pre-confirmation review |
| AR-11 | Request Sent | `ar-11-request-sent.jpg` | Confirmation state, the "few taps" payoff the section copy promises |
| AR-12 | My Requests | `ar-12-request-my-requests.jpg` | Status-tracking list, the guest-side view of what the Staff Task Board (next block) shows from the other side |

**Composition**: Single screen per frame, same phone-frame rules as the previous block. This is the longest single flow on the page (6 sequential screens); worth a light continuity pass across all 6 (consistent nav chrome, consistent typography scale) since they're meant to read as one uninterrupted task, more than any other block on this page.

**Aspect ratio**: 9:16 (Portrait Device Showcase) for all 6. **Figma artboard / export size**: 1350 x 2400px.

---

## The Staff Task Board (AR-13 through AR-18)

**HTML section**: 3rd `.gallery-block`, `.phone-row` of 6 screens.
**Belongs to**: "Real-time task management, so housekeeping and the kitchen see a request the moment it lands and can mark it done."
**Type**: Gallery phone, all 6.

| ID | Screen (caption) | Filename | Notes |
|---|---|---|---|
| AR-13 | Incoming | `ar-13-staff-incoming.jpg` | New-request queue, the staff-side counterpart to AR-11's "Request Sent" |
| AR-14 | Request Detail | `ar-14-staff-request-detail.jpg` | **Deliberately renamed from a bare "Request Detail" to disambiguate from AR-09's guest-facing "Item Detail."** Same caption text as the HTML (`data-caption="Request Detail"`), only the filename is disambiguated |
| AR-15 | Accepted | `ar-15-staff-accepted.jpg` | Status transition, first of a 3-stage lifecycle (Accepted → In Progress → Completed) |
| AR-16 | In Progress | `ar-16-staff-in-progress.jpg` | Second lifecycle stage |
| AR-17 | Completed | `ar-17-staff-completed.jpg` | Third lifecycle stage, the staff-side counterpart to a guest eventually seeing their request fulfilled |
| AR-18 | Room View | `ar-18-staff-room-view.jpg` | Likely a room/guest-context view a staff member checks alongside a task, distinct from the task list itself |

**Composition**: Single screen per frame, same rules as the prior two blocks. The 3-stage status lifecycle (AR-15/16/17) is this block's own internal continuity thread, worth the same visual-consistency pass as the Request Flow block, since a reader scanning left to right should read them as one status progressing, not three unrelated screens.

**Aspect ratio**: 9:16 (Portrait Device Showcase) for all 6. **Figma artboard / export size**: 1350 x 2400px.

---

## Receptionist Command Center (AR-19 through AR-22)

**HTML section**: 4th `.gallery-block`, `.wide-grid` of 4 screens (the only block on this page, and the only place in the entire site outside Currency Exchange, using the `.shot-frame.wide` frame type).
**Belongs to**: "Bookings, room status, and guest feedback in one view, so front-desk staff stop switching between systems mid-conversation with a guest."
**Type**: Gallery wide, all 4.

| ID | Screen (caption) | Filename | Notes |
|---|---|---|---|
| AR-19 | Reservations | `ar-19-reception-reservations.jpg` | Booking/room-status overview, the "one view" the section copy promises |
| AR-20 | Guest Detail | `ar-20-reception-guest-detail.jpg` | Single-guest record, front-desk's counterpart to AR-04's guest-side "Room Detail" |
| AR-21 | Rate & Feedback | `ar-21-reception-rate-feedback.jpg` | Aggregate or per-guest feedback view, receptionist-side counterpart to AR-06's guest-side "Feedback" |
| AR-22 | Feedback Detail | `ar-22-reception-feedback-detail.jpg` | Single feedback record detail |

**Composition**: This is a desktop/tablet interface, not a phone screen, this section's own copy ("stop switching between systems mid-conversation with a guest") implies a front-desk workstation context, matted at the Gallery lead/wide ~8-12% inset rather than the tighter phone inset. Since these render in a 2-column `.wide-grid` (not a horizontal filmstrip), each screen gets more on-screen real estate than any phone-row image on the page, worth a slightly higher information density and finer detail than the phone screens, since readers will actually be able to make out more of the interface at this display size.

**Aspect ratio**: 16:9 (Landscape Showcase) for all 4. **Figma artboard / export size**: 2400 x 1350px, the same Landscape Showcase spec used for any Rail hero/section or the Gallery lead image, per `FIGMA_PRODUCTION_GUIDE.md` section 1.

---

## Cross-link "More Work" cards (not counted in the 22)

Aryaduta's own page has 2 cross-link cards at the bottom (→ Account Hub, → Currency Exchange). Per the established sitewide pattern, these should reuse other pages' *own* card thumbnails, not be produced as part of this blueprint:

- **→ Currency Exchange**: `hp-ce-card.jpg` already exists (`assets/images/hp-ce-card.jpg`) and is already reused on every other page's cross-link card. This one is a pure implementation task, no production needed, whenever Aryaduta's own implementation happens.
- **→ Account Hub**: blocked, Account Hub has no card asset yet either (see `docs/blueprints/` — Account Hub has no blueprint of its own; its lead image, once produced, is the documented source for its homepage Explorations card and this cross-link card alike, per `IMAGE_ASSETS.md`).

Separately, two *other* pages' cross-link cards currently point at Aryaduta and are blocked waiting on this page's own production: Currency Exchange's "→ Aryaduta" more-work card, and the Homepage's "Other Explorations → Aryaduta" card (HP-06). Both are documented as reusing Aryaduta's own lead/hero image (AR-01), recropped to 3:2, once AR-01 exists. No new dedicated card shoot needed for Aryaduta, same reuse-not-new-export principle established for every other page's homepage/cross-link cards.

---

## Effort estimate

| Block | Count | Effort | Why |
|---|---|---|---|
| AR-01 Lead | 1 | Medium | First impression of the whole case study, establishes the visual bar for everything after it |
| Guest Experience App (AR-02–06) | 5 | Small each | Single screens, no composites, but the first block built sets the continuity/chrome standard the other phone blocks should match |
| Guest Request Flow (AR-07–12) | 6 | Small each, plus a continuity pass | Longest single flow on the page, worth extra care that all 6 read as one sequence |
| Staff Task Board (AR-13–18) | 6 | Small each, plus a continuity pass | Same continuity consideration as the Request Flow, particularly the 3-stage status lifecycle |
| Receptionist Command Center (AR-19–22) | 4 | Medium each | Desktop/tablet interfaces need more invented UI detail than a phone screen, and are the only `.wide` frames outside Currency Exchange |

**Total new builds: 22**, by a wide margin the largest single-page production effort in the portfolio (compare: Currency Exchange 9, Toko Mama 5, myBCA 3, Account Hub 7). Confirmed as committed work, full scope.

## Recommended production order

1. **AR-01 (Lead)** first. It sets the visual bar and, per `FIGMA_PRODUCTION_GUIDE.md`'s Gallery-mat convention, should establish the reusable mat components (phone-inset variant, lead/wide-inset variant) that every other slot on this page needs.
2. **Guest Experience App (AR-02–06)** next. Smallest, most self-contained block; establishes the guest-app visual identity that the Request Flow block continues directly.
3. **The Guest Request Flow (AR-07–12)**. Directly extends the Guest Experience App's visual language; sequencing it right after keeps that continuity easiest to hold.
4. **The Staff Task Board (AR-13–18)**. A different persona (staff, not guest), reasonable to batch as its own pass once the guest-side work is settled.
5. **Receptionist Command Center (AR-19–22)** last. The only desktop/tablet block, the only `.wide` frame type on this page, and the highest per-asset effort; benefits from being built once every phone-frame convention on the page is already locked, so the wide frames can echo the same visual system rather than setting their own.

Scope is confirmed at 22 (see Production status above), so AR-01 can start without any further scoping decision.

---

## Summary

- **Total media slots on the page**: 22 in-page (1 lead + 17 phone + 4 wide) + 2 cross-link cards (not Aryaduta production items, see Cross-link section).
- **Total unique assets to produce**: 22.
- **Total reused assets**: 0 inbound (nothing on this page reuses another page's asset); 1 outbound (AR-01 is the documented future source for 3 other pages' cross-link/Explorations cards once produced: Aryaduta's own homepage Explorations card, Currency Exchange's "→ Aryaduta" more-work card, and Account Hub's "→ Aryaduta" more-work card, none of which exist as slots on this page itself).
- **Recommended production order**: AR-01 → Guest Experience App → Guest Request Flow → Staff Task Board → Receptionist Command Center.

## Implementation checklist

- [ ] Build the Gallery phone-inset mat component (~4-6% margin, `--bg-card` fill), if not already reused from Account Hub's own production
- [ ] Build the Gallery lead/wide-inset mat component (~8-12% margin, `--bg-card` fill), if not already reused from Account Hub's own production
- [ ] Produce AR-01 — Lead (`ar-01-lead.jpg`)
- [ ] Produce AR-02 through AR-06 — Guest Experience App (5 phone screens)
- [ ] Produce AR-07 through AR-12 — The Guest Request Flow (6 phone screens)
- [ ] Produce AR-13 through AR-18 — The Staff Task Board (6 phone screens)
- [ ] Produce AR-19 through AR-22 — Receptionist Command Center (4 wide screens)
- [ ] Verify all 17 phone exports are 1350x2400 (9:16, Portrait Device Showcase), all 5 lead/wide exports are 2400x1350 (16:9, Landscape Showcase)
- [ ] Confirm continuity (chrome, type scale) reads consistently within the Guest Request Flow's 6-screen sequence and the Staff Task Board's 3-stage status lifecycle
- [ ] Update `IMAGE_ASSETS.md`'s Aryaduta filenames from the old `aryaduta-<description>.jpg` convention to the asset-ID prefix convention used here (`ar-01-lead.jpg` etc.), and update its Lead/wide export-size note from the placeholder "e.g. 1600x900" to the locked 2400x1350
- [ ] Update `MASTER_ASSET_TRACKER.md` with a new Aryaduta section once any assets are delivered
- [ ] Wire into HTML only after Leo confirms each export (no HTML changes made as part of this blueprint)
- [ ] Once AR-01 exists, revisit the 3 blocked cross-link/Explorations cards that depend on it (Aryaduta's own homepage card, Currency Exchange's "→ Aryaduta" card, Account Hub's "→ Aryaduta" card)
