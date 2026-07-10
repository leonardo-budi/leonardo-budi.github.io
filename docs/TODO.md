# TODO

Tasks remaining on this project, in recommended order. This file is a living document: update it at the end of every significant work session to reflect what was completed and what should happen next. See `SESSION_LOG.md` for the full session-by-session record.

**Current state (2026-07-08): every page is fully implemented (all images, video, and interaction wired) and has been through a hiring-manager review and a full editorial pass on the Homepage and Currency Exchange.** Nothing below is a launch blocker in the sense earlier versions of this file meant; the site could be deployed as-is. What remains is a mix of small polish items, honest open questions, and one larger deferred decision.

## 1. Deploy (the only remaining hard gate)

- **Deploy to GitHub Pages**: make the repo public, enable Pages, push, then verify every internal link and the CV download on the live URL. Repository structure, link integrity, and case-sensitivity have all been verified locally as deploy-ready; the actual deploy hasn't happened yet.

## 2. Known, accepted gaps (not blocking, already documented as intentional)

These are open questions or honest limitations that were surfaced and deliberately left as-is, not oversights. Don't rediscover or re-litigate these without new information.

- **No case study has a quantified outcome.** Flagged directly in the hiring review. Currency Exchange, Toko Mama, and myBCA all explicitly state they have no metrics to report (no baseline existed, or the concept was never shipped). This is truthful, not a gap to paper over with an invented number. Only resolvable if real analytics/usage data ever becomes available for one of these features.
- **The systems-thinking / OVO evidence gap.** The homepage testimonials all praise design-systems work at OVO; no case study anywhere in the portfolio demonstrates that work. The hiring review's Critical finding about the testimonials feeling "disconnected" was fixed (reordered the cards, added a bridge sentence — see `SESSION_LOG.md`, 2026-07-08), but that only fixed the *narrative connection*, not the underlying *evidence gap*. Actually closing this would mean producing a real Design Systems case study, a separate, larger effort. See the "Deferred systems audit" section below, this item predates the 2026-07-08 review and remains the right home for it.
- **Toko Mama's smaller scope, left as an honest account.** Unlike Currency Exchange (full ownership, three explorations, final delivery), Toko Mama's "My Role" section describes reviewing and refining an existing proposal, a lighter-touch contribution. This was reviewed during the hiring pass and deliberately kept as-is, since it's an accurate account of what happened, not something to inflate.
- **Homepage cards HP-05/HP-06 ratio deviation.** `hp-ah-card.jpg` and `hp-ar-card.jpg` are both delivered at 16:9 (2400x1350), not the locked 3:2 (2400x1600) Portfolio Card spec the other three homepage cards use. `hp-ah-card.jpg` is byte-identical to Account Hub's own lead image, not a dedicated re-export. Implemented exactly as delivered; flagged in `MASTER_ASSET_TRACKER.md`, not corrected without Leo's input.
- **Aryaduta's meta grid is still 3 columns**, not the sitewide 4-column standard Account Hub already received in its own layout-polish pass. Left as-is since asset-implementation sessions were explicitly scoped to assets and interaction, not layout.
- **The Rail backdrop-tint question.** Currency Exchange and Toko Mama's placeholder gradients are byte-identical (green family) while myBCA has its own distinct blue family, likely an accidental copy-paste artifact from early production. Never resolved one way or the other by Leo. Doesn't apply to either Gallery page.
- **CE-01's pending art-direction review** (photographic background, device tilt/chrome, off-center composition), flagged in an early session, never formally closed out. Not currently blocking anything.

## 3. Small polish items (low effort, do whenever convenient)

- **CE-09 compression pass.** The full-transaction-flow video is 49MB and now autoplays on page load, more pressing than when it was click-to-play. Needs a compression/trim pass.
- ~~**About portrait extraction.**~~ Done 2026-07-09: extracted to `assets/images/about-leo-portrait.jpg`, `<img>` src updated, no `data:image` payloads remain in `index.html` (188KB to 51KB). See `SESSION_LOG.md`.
- ~~**Favicon** (HP-07).~~ Done 2026-07-09: built from the exact "Leo." wordmark (Shrikhand glyph outlines extracted directly from the font, not redrawn), same design tokens (`#0A0A0A` bg, `#F0EFE9` text, `#C8F135` accent dot). Delivered as `assets/favicon/favicon.svg` (vector), `favicon-16x16.png`, `favicon-32x32.png`, `favicon-48x48.png`, `apple-touch-icon.png` (180x180, opaque per Apple HIG), and `favicon-mono.svg` (single-color, transparent, wired as `rel="mask-icon"`). Linked in all six HTML files. See `SESSION_LOG.md`.
- **Open Graph image** (HP-08). Genuinely new, homepage-original asset. Explicitly deferred to "After Publish," not a launch blocker.
- **If Leo ever gets the original, unedited LinkedIn recommendation text**, there may be sentences already in the source that could replace the current testimonial excerpts without needing any OVO/design-system framing at all, a stronger fix than the bridge-sentence approach used on 2026-07-08. Not actionable without that source text.

## 4. Technical QA (do before or shortly after deploy)

- **Accessibility check**: WCAG AA contrast on image overlays/captions, full keyboard path including the lightbox dialog (focus trap, Escape, focus return), heading order, and landmarks.
- **Cross-browser test**: Chrome, Safari, Firefox at minimum; confirm the custom cursor degrades gracefully (already disabled on coarse pointers).
- **Performance pass**: compress/size all exports (see CE-09 above especially), add `width`/`height` to prevent layout shift, lazy-load below-the-fold images, run Lighthouse.

## 5. Future improvements (not gating anything)

- Reconsider whether the custom cursor still earns its place now that real content is in (see `DESIGN_DECISIONS.md`).
- Future writing pieces in Leo's voice, well after launch (see `FUTURE_IDEAS.md`).
- **Custom domain**, if desired.

## 6. Deferred: the systems audit (long-term, separate effort, the one big open decision)

Intentionally separate from maintaining this portfolio. Do not let this affect the current, locked pages.

- **Systems audit** of OVO, DDT, and Nobu work to determine whether a Design Systems case study is supportable by real evidence. This is the single highest-leverage future addition, because it's the one gap that copy editing alone cannot close (confirmed independently by both the original Phase 2 review and the 2026-07-08 hiring review).
- If, and only if, that work lands, reconcile it back into the homepage About/"How I Work" copy and reconsider whether the testimonials need a fuller connection than the current bridge sentence provides.

## Out of scope (do not do)

- Inventing metrics or outcomes that weren't actually measured.
- Editing a testimonial's substance to make it fit the narrative better (reordering cards and adjusting the intro is fine; changing what a quote says is not).
- Adding new templates, fonts, or accent colors.
- Introducing a build step or framework.
- "Optimizing" human writing for negligible gain, or repeating an editorial pass on a section that already went through one without a specific new reason.
- Flattening the repository structure back to a single directory.
