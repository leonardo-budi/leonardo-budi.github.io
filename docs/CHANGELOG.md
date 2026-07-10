# CHANGELOG

Major milestones and the decisions made at each, oldest to newest. This is a narrative history, not a commit log.

## Phase 0: Foundation (prior to this effort)

- Established the static, no-build architecture: one self-contained HTML file per page, inline styles and scripts, tokens duplicated per file, relative links, dark editorial aesthetic.
- Locked the design system: colors, the lime accent discipline, the three-font system (Fraunces / Inter / Shrikhand), the type scale, and the image ratios.
- Built the homepage and the first complete pages: Currency Exchange (Rail, the flagship, eight-section arc), Toko Mama (Rail), and Aryaduta (Gallery).
- Defined the two templates (Rail and Gallery) and the core interactions (reveal-on-scroll, card hover, accessible lightbox, rail scroll-spy, mobile nav).

## Phase 1: Building the two remaining pages

- **myBCA built** on the Rail template. Decided on five sections, not the flagship's eight, because the real source material only supports five without fabrication. Reported the survey as raw counts ("8 of 11," "7 of 11") rather than percentages, to avoid implying false rigor on a sample of eleven. Used verbatim participant quotes, one per side of the privacy-versus-transparency tension. Built with correctly-ratioed placeholder frames mapped to deck slides, tinted blue for BCA.
- **Account Hub built** on the Gallery template, generated from the Aryaduta reference so the CSS and JS stayed byte-identical. Decided Gallery over Rail because the work is a refinement (one buried-nav problem, one fix, two visual directions) and does not support a full narrative. Tinted placeholders Nobu green. Framed honestly as discoverability and placement, not information architecture.

## Phase 2: Critical review

- Conducted a full hiring-manager review of the portfolio as one product. Diagnosed the central finding: the strongest claim (systems thinking, backed by testimonials about the OVO design system) has no supporting case study. Separated this into two concerns: thematic narrowness (a storytelling problem, fixable by repositioning) and an evidence gap (a credibility problem, not fixable by copy).
- Agreed to keep two goals independent: lock and publish the current portfolio now; audit the systems work as a separate future project. No mixing.

## Phase 3: The locking pass

Worked through issues with strict approval gates, smallest-effective-change, and truthful-over-persuasive throughout.

- **Critical fixes**: unified project naming to one canonical form each (resolving, for example, Aryaduta appearing as both "Hospitality App & Staff Tools" and "Hospitality Service Ecosystem"); corrected the homepage myBCA card from "a toggle that solved it" to "a toggle as the answer" to match the case study's honest, unmeasured outcome; aligned myBCA's rail labels (and their mobile mirrors) to the bare-noun style of the other Rail studies.
- **Repositioning (editorial, not narrative)**: changed all five case-study eyebrows to lead with each project's genuine distinct dimension, after pressure-testing that each dimension was already supported by the body. Chose quiet framing over explicit labeling, and modest wordings throughout ("Improving discoverability" not "Information Architecture"; "Designing across touchpoints" not "Connected service design"; "Validating an assumption" not "Research & validation").
- **Taxonomy and honesty**: corrected Aryaduta's type label to "Pitch Concept"; changed Toko Mama's homepage tag from the orphaned "UX Case Study" to the domain tag "Retail POS."
- **Credibility**: added one modest sentence of BCA scale context to myBCA.
- **Deployment-critical fix**: renamed `myBCA.html` to lowercase `mybca.html` to match its links and prevent a case-sensitivity 404 on GitHub Pages.
- **Deliberate non-changes**: kept the homepage repetition, the mixed eyebrow grammar, the per-page meta-label and tab-title variation, and the custom cursor, each for a reasoned, recorded purpose (see `DESIGN_DECISIONS.md`).
- **Final QA**: verified naming, navigation, footer, contact, links (case-sensitive), tokens, fonts, responsive breakpoints, heading hierarchy, the em-dash rule, and grammar across all six pages. All passed.

## Phase 4: Repository restructuring and link integrity baseline

- Confirmed the canonical project structure as nested, not flat: `study-case/<project>/index.html` for Rail case studies, `visual-lab/<project>/index.html` for Gallery pieces, homepage staying at the repo root for GitHub Pages compatibility.
- Rewrote every internal link and the CV link across all six pages to correct, depth-aware relative paths for the nested structure. No copy or markup structure changed, only `href` values.
- Removed a leftover duplicate file (`visual-lab/account-hub/account-hub.html`) with stale, non-canonical eyebrow copy; kept the canonical `index.html` in that folder.
- Renamed the CV to its canonical filename, `LeonardoBudi_CV2026_EU.pdf`, and relocated it to `CV/`.
- Updated `PROJECT_STRUCTURE.md` and `PROJECT_RECAP.md` to describe the actual nested structure and the relative-link convention.
- Verified all internal links resolve case-sensitively, no duplicate files remain, and the structure serves correctly under simulated GitHub Pages conditions (every page and the CV returned 200, including directory-style paths auto-resolving to `index.html`).
- Established `SESSION_LOG.md` as a new living document for session-by-session detail, distinct from this file's milestone-level narrative. See `SESSION_LOG.md` for the full record of this session.

## Phase 5: Production completion

- All six pages fully implemented: every image, video, and hover/lightbox interaction wired across Currency Exchange, Toko Mama, myBCA, Account Hub, Aryaduta, and the Homepage. The `.shot-frame` component is now byte-identical across all six files, including Aryaduta, which had never been through the standardization pass and carried a real latent bug (lightbox JS firing on navigation-only cards) until this phase.
- Every cross-link "More Work" card and both Homepage Explorations cards wired with real thumbnails; zero placeholder gradients remain anywhere in the site.
- One flagged, unresolved production deviation: the Account Hub and Aryaduta homepage cards were delivered at 16:9 rather than the locked 3:2 Portfolio Card ratio; implemented as delivered, not silently corrected.

## Phase 6: Hiring review and editorial refinement

- Conducted a second, independent hiring-manager review (the first was Phase 2). Reached the same central finding independently: the strongest claimed strength (systems thinking, evidenced only by testimonials about OVO's design system) has no supporting case study. Also newly identified: the portfolio's own "simplicity is about clarity, not reduction" thesis had been restated near-identically four times across the Homepage and Currency Exchange, and the three Currency Exchange Explorations sections all closed with the same sentence template.
- **Fixed what copy editing can fix**: de-duplicated the repeated thesis across four locations, keeping one as the introduction (Homepage) and one as the earned realization (Currency Exchange Reflection), rewriting the other two to do distinct narrative jobs. Gave each of the three Explorations sections a different closing function (unresolved trade-off, open question, stated realization) instead of a repeated template. Resolved a pronoun inconsistency in Currency Exchange (a "we" with no textual antecedent, next to an explicit "I owned the design direction" claim), correcting only the two occurrences that were genuinely inconsistent and leaving three others that describe genuine shared project conditions.
- **Fixed the testimonials' narrative disconnection, not their content**: reordered the three homepage testimonial cards so the one not referencing OVO leads, and added a bridge sentence to the section intro. Explicitly declined to edit any testimonial's wording, since altering what a real recommender said to fit the narrative better would be a truthfulness violation, not an improvement.
- **Did not fix, and documented as intentionally not fixed**: the underlying systems-thinking evidence gap (as opposed to its narrative symptom), the absence of quantified outcomes in any case study, and Toko Mama's smaller, honestly-scoped contribution relative to Currency Exchange. None of these are solvable by editorial work alone; inventing metrics or a case study that doesn't exist would violate the project's own "truthful over impressive" rule.

## Current state

Every page is fully implemented and has been through at least one editorial review pass; the Homepage and Currency Exchange have been through two. The only remaining hard gate is the actual GitHub Pages deploy, everything else outstanding is either small polish or a deliberately deferred, larger decision (the systems audit). See `TODO.md` for the current task list and `SESSION_LOG.md` for the session-by-session log.
