# PROJECT HANDOFF

Written 2026-07-08, after full asset implementation across all six pages and a complete hiring-review-driven editorial pass on the Homepage and Currency Exchange. This document exists so a brand-new Claude conversation can pick up this project with zero prior context and continue seamlessly. It supersedes all earlier handoffs; their content is folded in below where still accurate, and their now-stale claims (mainly: images still placeholder, copy still "locked" and untouched) have been removed, not just appended to.

**Read this first, in this order, if you're new here:**
1. This document (orientation, architecture, current copy state, what's done, what's next)
2. `docs/README.md` (the project's own reading order for everything else)
3. `docs/TODO.md` (current backlog, all of it small/deliberately-deferred, not launch-blocking)
4. `docs/SESSION_LOG.md` (the full, dated history — read the most recent entries first)

---

## 1. What this project is

A static, no-build HTML portfolio for Leonardo Budi Kurniawan (Leo), a Senior Product Designer, targeting European product-led companies. Six pages, two visual templates, a locked dark editorial design system (near-black background, lime accent, Fraunces serif headings, Inter body text).

**The copy is no longer "locked" in the sense earlier documentation meant.** Every page's copy was originally locked and treated as final, but the Homepage and Currency Exchange have since been through a real hiring-manager review and a full editorial pass in response to it (see section 5). Toko Mama, myBCA, Account Hub, and Aryaduta have not been through this same review pass and their copy is unchanged from the original lock. Don't assume the whole site's copy is either "fully locked" or "fully open" — check section 5 and `SESSION_LOG.md` for exactly what's changed.

Two overriding rules, stated at the start of this engagement and never superseded:
- **Truthful over impressive.** Never invent evidence; surface what already exists. Report problems and open questions rather than papering over them. This rule has been tested directly: no metrics were fabricated for any case study, and no testimonial's wording was altered to fit the narrative better, even when doing so would have made the portfolio read more impressively.
- **No em dashes, anywhere**, in any copy or documentation prose.

---

## 2. Architecture

**This is a deliberately no-build, dependency-free static site.** Confirmed explicitly in `docs/PROJECT_STRUCTURE.md`:

> Every page is a single self-contained `.html` file. Inside each file, in order: `<head>` with meta, Google Fonts link, and a full inline `<style>` block; then `<body>` with the page markup; then a single inline `<script>` block at the end. There are no external CSS or JS files. This is deliberate... Design tokens and the shared component CSS are duplicated in every file. There is no shared stylesheet. A token or shared-component change must therefore be made in all six files, and verified to stay identical.

**This is the single most important architectural fact for continuing this project.** When a shared component (like `.shot-frame`) needs a change, it means editing the same CSS/JS block, byte-identically, into every file that uses it. There is no way to "fix it in one place." Always diff the block across files after editing to confirm they match.

### Folder structure

```
/
  index.html                                    (homepage, repo root — required by GitHub Pages)
  study-case/currency-exchange/index.html        (Rail template, fully implemented, two editorial passes)
  study-case/toko-mama/index.html                (Rail template, fully implemented, one editorial pass)
  study-case/mybca/index.html                    (Rail template, fully implemented, one editorial pass)
  visual-lab/account-hub/index.html              (Gallery template, fully implemented)
  visual-lab/aryaduta/index.html                 (Gallery template, fully implemented)
  CV/LeonardoBudi_CV2026_EU.pdf
  assets/images/                                 (site-wide reused assets: homepage cards, about portrait once extracted)
  study-case/<project>/assets/                   (per-project production assets, all populated)
  visual-lab/<project>/assets/                   (per-project production assets, all populated)
  docs/                                           (all project documentation)
```

Relative link depth: from `study-case/<project>/index.html` or `visual-lab/<project>/index.html`, the repo root is `../../`.

### Two page templates

- **Rail** (Currency Exchange, Toko Mama, myBCA): a sticky left-side progress rail, composed "deck slide" images (16:9, sharp corners, no device chrome, backdrop gradient baked into the export). Fully built out, fully implemented, all three pages complete.
- **Gallery** (Account Hub, Aryaduta): phone filmstrips and matted screen captures (`.shot-frame.phone`, `.shot-frame.wide`, `.shot-frame.lead`), rounded corners. Gallery's mat is a fixed flat `--bg-card` fill baked into the export, not a gradient backdrop like Rail. Both pages fully implemented.

### Design tokens (CSS custom properties, identical across all files)

```css
--bg: #0A0A0A;
--bg-card: #111111;
--bg-card-hover: #171717;
--text: #F0EFE9;
--text-muted: #8C8C84;
--accent: #C8F135;       /* lime, used sparingly, never as an image fill */
--border: #1C1C1C;
--maxw: 1440px;
```

Fonts: Fraunces (serif, headings), Inter (sans, body/UI), Shrikhand (the "Leo." logo only, with a lime-colored period).

---

## 3. The canonical reusable component: `.shot-frame`

Applied identically (copy-pasted byte-for-byte) into all six HTML files: `index.html`, both Rail case-study files not yet named, `study-case/toko-mama/index.html`, `study-case/mybca/index.html`, `visual-lab/account-hub/index.html`, and `visual-lab/aryaduta/index.html`. Confirmed via diff that the core block is byte-identical across all six as of the full-implementation pass.

**What it does, visually.** On hover or keyboard focus: the image/video scales to 1.02 and a dark overlay fades to 18% opacity, both immediately over 200ms. A centered pill-shaped text hint fades in and slides up, staggered: 120ms delay + 90ms fade-in when appearing, an immediate 150ms fade with no delay when disappearing. Hint text reads "Click to Preview" for images, "Preview Video" for videos. Cursor is `zoom-in`.

**Three non-obvious things you need to know before touching this again:**

1. **`.shot-frame` is applied to two structurally different things, and the JS must tell them apart.** On case-study pages, `.shot-frame` is a `<button>` that opens a lightbox modal on click. On the homepage's cards and every case-study page's "more work" cross-link cards, `.shot-frame` is applied to a `<div>` nested inside an `<a href>` — clicking should just navigate. The JS does `if (f.tagName === 'BUTTON') { f.addEventListener('click', function(){ open(f); }); }` to keep these separate. **This exact bug (lightbox JS firing on navigation-only cards) was found and fixed independently on both Account Hub and Aryaduta** during their respective standardization passes; if a new page or component is ever added, check this first.
2. **`margin: 0` in the base rule will collapse intentional spacing.** Combine with compound-class overrides (`.pip.shot-frame { margin-bottom: 28px; }`, etc.) wherever `.shot-frame` sits alongside a class that needs its own margin.
3. **`position: relative` on `.shot-frame > img, video` is load-bearing.** Without it, placeholder `::before` gradients paint above real photos in stacking order. If a real image ever "disappears" behind a gradient after a CSS change, check this first.

### Video pattern

Every MP4 (`ce-09-full-transaction-flow.mp4`, `tm-03-friction.mp4`, `tm-05-outcome.mp4`) uses `autoplay muted loop playsinline preload="metadata"`, no native `controls`, wrapped inside a `.shot-frame` button so clicking still opens the lightbox.

---

## 4. Implementation status (complete)

**Every page is fully implemented. There are no placeholder images anywhere in the site.**

| Page | Status |
|---|---|
| Currency Exchange | 9/9 assets implemented. Two editorial passes completed (see section 5). |
| Toko Mama | 5/5 assets implemented. Not yet through the hiring-review-driven editorial pass. |
| myBCA | 3/3 assets implemented. Not yet through the hiring-review-driven editorial pass. |
| Account Hub | 7/7 assets implemented, `.shot-frame` standardized. |
| Aryaduta | 22/22 assets implemented, `.shot-frame` standardized (was the last page to receive this, see `SESSION_LOG.md` 2026-07-06). |
| Homepage | All visible media slots implemented (About portrait extracted to a real file 2026-07-09, `assets/images/about-leo-portrait.jpg`). Copy through a full editorial pass (see section 5). |
| Cross-link "More Work" cards | All 8 possible cards wired. No placeholders remain. |

Cross-check `docs/MASTER_ASSET_TRACKER.md` for the asset-by-asset ledger if you need file-level detail; it's accurate as of the full-implementation pass and hasn't needed updating since, because nothing image-related has changed since.

**One flagged, unresolved production deviation**: `hp-ah-card.jpg` and `hp-ar-card.jpg` (the Account Hub and Aryaduta homepage cards) were delivered at 16:9 (2400x1350), not the locked 3:2 (2400x1600) Portfolio Card spec the other three homepage cards use. `hp-ah-card.jpg` is byte-identical to Account Hub's own lead image. Implemented exactly as delivered, not silently corrected.

---

## 5. Current copy state, and what changed

This is the part most likely to be out of date if you're picking this project up later. Read `SESSION_LOG.md`'s 2026-07-08 entry for the full detail; this is a summary.

### The hiring review

Leo requested a skeptical, high-standards hiring-manager review of the whole portfolio (not the first one, see `CHANGELOG.md` Phase 2 for an earlier round). It reached two Critical findings:

1. **A core thesis, restated too many times.** "Simplicity is about clarity, not reduction" (in various phrasings) appeared near-identically four times: the Homepage hero, the Currency Exchange hook, its Reflection, and its closing lesson line. Read consecutively, this felt like padding, not a point of view.
2. **The testimonials feel disconnected.** All three homepage testimonials praise OVO design-system work. Nothing else on the site, no case study, no About-section line, references it. The quotes read as floating, unconnected proof.

Both were resolved through explicitly-scoped editorial passes (Leo asked for each section by name, one at a time, not a blanket rewrite). **Neither fix involved inventing content or editing what a testimonial actually says** — see below for exactly what changed.

### Homepage — current state

- **Hero**: sub-line is *"I simplify complex products without simplifying the decisions people need to make."* This is the philosophy's one canonical statement at the site level; don't add a second one elsewhere without checking this section first.
- **About**: three paragraphs, no longer mentions design systems, OVO, or the 120K+ user figure (that figure now lives only in the hero's proof chips). Kept deliberately narrow to the candidate's own stated positioning.
- **"How I Work"** (formerly "Strengths" / "What you actually get"): label is "How I work," heading is "The principles behind my work.", three cards: Thoughtful Decisions, Intentional Craft, Pragmatic Under Constraints. None of the three cards mention design systems or OVO. Card titles are `var(--fs-xl)` (22px, the next step up on the existing type scale, was previously a manually-set 20px not on the scale at all).
- **Selected Work**: label "Selected Work," heading "Complex problems. Clear decisions.", with an intro paragraph below it. The "Featured" badge that used to sit beside the heading was removed, not replaced.
- **Other Explorations**: intro paragraph now reads more generically ("across different industries, teams, and stages of product development") than an earlier, sharper version ("Some shipped, some didn't... just lighter on documentation"). This is a known, minor regression in copy quality, not something anyone has asked to fix yet, flagged here in case it comes up.
- **Testimonials**: **structure changed, content did not.** The three testimonial quotes, names, roles, and relationship labels are byte-identical to the originals. What changed: (a) card order, Aldi Buntaran's quote (no OVO mention) now leads, followed by the two OVO-referencing quotes; (b) the section intro was moved from a right-aligned side-column position into a body-copy paragraph directly below the heading (matching the label→heading→intro pattern used in Selected Work and Other Explorations), and now reads *"Recommendations from people who collaborated with me across different teams, roles, and projects."* — deliberately avoids the words "design systems" per Leo's explicit follow-up request, since the portfolio doesn't have a dedicated Design Systems case study and using that phrase created an expectation the site doesn't fulfill.
- **Testimonials heading single-line fix**: "What people say" was wrapping to two lines because the shared `.t-light`/`.t-bold` spans are `display: block` (the mechanism behind every two-line heading site-wide). Fixed with a scoped override (`.testimonials-header .sec-title .t-light, .t-bold { display: inline; }`), not a change to the shared rule, so no other heading was affected.

### Currency Exchange — current state

- **Hero hook**: *"Real money, live rates, and a screen that had to hold everything at once. Every field affected another, and fixing one often meant breaking a different one."* Went through two rounds: first rewritten away from restating the homepage thesis, then a second pass (at Leo's request) to make the second sentence describe the actual design problem rather than the article's own structure.
- **Context and My Role**: rewritten earlier in this project's editorial history to add explicit business rationale (revenue retention, not just convenience) and a clearer, appropriately-scoped ownership statement ("I owned the design direction..."). Unchanged since.
- **Landscape competitor bullets**: rewritten with analytical, present-tense framing ("Reduces cognitive load by...", "Keeps both currencies visible...", "Builds confidence with..."). Presentation-only change also applied: each competitor's name and description now sit on separate lines (name on its own line, description indented beneath it, wrapped lines aligned), scoped to this list only via a `.case-list-stacked` modifier class, other bullet lists on the page are unaffected.
- **Challenge intro, Explorations 1-3, Final Design, Reflection**: all rewritten with new copy earlier in this project's editorial history (see `SESSION_LOG.md` for the exact before/after text of each).
- **Explorations 1-3, closing sentences**: each now ends with a distinct narrative function instead of a repeated template. Exploration 1 closes on an unresolved trade-off ("Focus and understanding, it turned out, weren't the same problem..."), Exploration 2 on an open question ("...what it would take to make those pieces feel like one decision instead of several"), Exploration 3 on a stated realization ("Tabs were never the feature. They were the thing standing in the way of it."). Everything before each new closing sentence is untouched.
- **Pronoun consistency**: reviewed every "I"/"we"/"our" against the "I owned the design direction" claim. Two occurrences were changed to "I" for consistency (Exploration 1's opening, Final Design's closing line). Three "we" occurrences were deliberately kept: Key Constraints and "If I went back, one" (both describe shared project resources, not a personal decision), and "If I went back, two" (the rate-lock scope cut, a genuine cross-functional timeline/technical trade-off). **Don't "fix" these remaining three "we" instances**, they were reviewed and kept on purpose.
- **Reflection, closing lesson line**: now reads *"The lesson: every constraint left something out. The real work was deciding which gaps were acceptable to leave for later, and which ones weren't."* — deliberately a trade-offs synthesis of the "if I went back" list, not a restatement of the Reflection's own opening thesis.

### Toko Mama and myBCA

Both fully implemented, both have real copy from an earlier editorial pass in this project's history (see `SESSION_LOG.md` for the exact text of each section), but **neither has been through the hiring-review-driven pass described above**. If a similar review is ever requested for these two pages, expect to find the same categories of issue (repeated phrasing, pronoun questions, section endings) since they weren't checked for these specific patterns. Each also had one single-line heading fix applied (Toko Mama: "Making saved carts visible.", myBCA: "A small gap, but a real one.") — both were hard-coded `<br/>` tags removed, not CSS/typography changes.

### Account Hub and Aryaduta

Copy unchanged since original production. Neither has been through any editorial review pass. Both are honestly labeled as a "Proposal"/"UX Refinement" and a "Pitch Concept" respectively, appropriately lighter in scope than the three Rail case studies, and this was confirmed appropriate during the hiring review (not treated as a gap needing inflation).

---

## 6. What was deliberately left unchanged, and why

- **No metrics were invented for any case study.** Currency Exchange, Toko Mama, and myBCA all explicitly state they have no quantified outcome to report. This is the honest state of the work, not a gap to be papered over.
- **No testimonial's wording was changed.** The testimonials' disconnection from the rest of the site was a narrative-structure problem (fixed via reordering and a bridge sentence), not a content problem. Editing what a real person said to make the story fit better would have been a truthfulness violation.
- **Toko Mama's smaller scope of ownership was kept as an honest account**, not inflated to match Currency Exchange's full-ownership narrative.
- **The systems-thinking/OVO evidence gap itself remains open.** Fixing the testimonials' narrative connection did not, and could not, close the underlying gap (a real Design Systems case study doesn't exist in this portfolio). This is `TODO.md`'s single largest deferred item, predates the 2026-07-08 review, and is intentionally kept separate from routine editorial work.
- **Three "we" pronoun instances in Currency Exchange were kept**, not converted to "I," because they genuinely describe shared project conditions or cross-functional trade-offs rather than personal design decisions.

---

## 7. Remaining work

1. **Deploy to GitHub Pages.** The only remaining hard gate. Everything else is polish or deliberately deferred.
2. **CE-09 video compression** (49MB, now autoplays on load).
3. ~~About portrait extraction from inline base64 to a real file~~, done 2026-07-09.
4. ~~Favicon~~, done 2026-07-09 (`assets/favicon/`, built from the actual "Leo." wordmark's font outlines). **OG image** still outstanding, explicitly deferred to After Publish.
5. **The systems audit** (see section 6), the one large deferred decision, separate from routine maintenance.
6. Smaller open items: the Homepage card ratio deviation (HP-05/HP-06), Aryaduta's meta grid still at 3 columns, the Rail backdrop-tint question (CE/TM green vs. myBCA blue), and the softer "Other Explorations" intro copy noted in section 5.

See `docs/TODO.md` for the full, current, prioritized list.

---

## 8. Documentation index

| Document | Purpose |
|---|---|
| `docs/README.md` | The project's own recommended reading order |
| `docs/WORKING_RULES.md`, `DESIGN_DECISIONS.md`, `COPYWRITING_GUIDELINES.md` | Foundational rules; still worth reading, though "copy is locked" language predates this session's editorial passes |
| `docs/PROJECT_STRUCTURE.md` | File/naming/deployment conventions, including the no-build architecture |
| `docs/TODO.md` | Current, up-to-date task list as of this handoff |
| `docs/CHANGELOG.md` | Narrative history of major milestones, now includes Phase 5 (production completion) and Phase 6 (hiring review and editorial refinement) |
| `docs/SESSION_LOG.md` | Long, granular, dated log of every session's work. The authoritative history for exact before/after text of any copy change. |
| `docs/IMAGE_ASSETS.md`, `IMAGE_STYLE_GUIDE.md`, `FIGMA_PRODUCTION_GUIDE.md` | Production system documentation, all still accurate, unaffected by this session's copy-only work |
| `docs/blueprints/*.md` | Per-page production blueprints, all six pages now implemented against them |
| `docs/MASTER_ASSET_TRACKER.md` | Cross-page asset ledger, accurate as of full implementation, unaffected by copy changes |
| `docs/SESSION_HANDOFF.md` | This document |

---

## 9. A note on the local preview/testing environment

Worth knowing if you continue using the same browser-preview tooling: it has shown intermittent flakiness across every session, screenshots occasionally render solid black on the first capture after a DOM mutation or scroll (a repeat capture or server restart sometimes fixes it, sometimes doesn't), and at least once a real coordinate-based click failed to visibly register while a synthetic `dispatchEvent` immediately confirmed the underlying JS logic worked correctly. None of this reflects real bugs in the site. When the screenshot tool looks wrong, cross-check via the accessibility snapshot, direct DOM text reads, or `getBoundingClientRect`/`scrollWidth` comparisons before concluding there's a real regression. That said, real regressions have been caught this way more than once, so don't wave away a discrepancy without independently confirming it either way.
