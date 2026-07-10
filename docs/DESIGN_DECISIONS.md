# DESIGN_DECISIONS

Every important decision we made on purpose, with the reasoning. Do not reopen these without a strong, evidence-based reason. They represent the final agreed direction.

## The locked design system

Fixed and not to be changed:

- **Colors**: `--bg #0A0A0A`, `--bg-card #111111`, `--bg-card-hover #171717`, `--text #F0EFE9`, `--text-muted #8C8C84`, `--accent #C8F135` (lime), `--border #1C1C1C`. Layout: `--maxw 1440px`.
- **Accent discipline**: lime is used sparingly, one highlighted word, the active rail item, a hover state, a small label. Never as a fill or a second brand color.
- **Fonts, one job each**: Fraunces (serif) for headings and display; Inter (sans) for body and UI; Shrikhand for the "Leo." logo only, with a lime period, 40px tablet and up, 36px on mobile.
- **Type scale** (base 16, floor 10): `--fs-2xs 10` through `--fs-4xl 46`. Section titles use `clamp(38px, 4.4vw, 62px)`. Substantive reading text (body, info points, bullets) at `--fs-lg` (18); secondary card text at `--fs-base` (16); captions at `--fs-sm` (14); labels and tags at `--fs-xs`/`--fs-2xs`.
- **Image ratios**: 16:9 for case-study internal frames and hero; 3:2 for project, exploration, and "more work" cards; 4:3 for the About portrait; 393x852 for phone frames.
- **Tokens are duplicated per file.** A token change must be applied to every file. This is an accepted tradeoff of a no-build static site.

## Two templates

- **Rail** (Currency Exchange, Toko Mama, myBCA): deep case studies, sticky left section nav with scroll-spy, collapsing to inline section tags on mobile. Use when the work supports a genuine multi-section narrative.
- **Gallery** (Account Hub, Aryaduta): lighter, image-led, no rail. Use when the work is a refinement or pitch that does not support a full narrative arc. Choosing Gallery for thinner work is honest framing, not a downgrade; forcing thin content onto the Rail looks weaker, not stronger.

Section count follows the source material, not the template. myBCA has five sections, not the eight Currency Exchange uses, because the real material only supports five without fabrication.

## Final eyebrow strategy

Each case-study eyebrow leads with the project's **distinct dimension** in a `[dimension] · [client/product]` shape. This was a deliberate repositioning to counter a "feels too narrow" perception, achieved purely by emphasis at the top of each page, with no change to the underlying work.

| Page | Eyebrow | Dimension surfaced |
|---|---|---|
| Currency Exchange | Constraints & trade-offs · Nobu Bank | Decision-making under real constraints |
| Toko Mama | Workflow under pressure · Toko Mama | Operational design for frontline users |
| myBCA | Validating an assumption · myBCA | Evidence-informed design |
| Account Hub | Improving discoverability · Nobu Bank | Findability and placement |
| Aryaduta | Designing across touchpoints · Aryaduta | Multi-surface, connected service |

### Why each project carries a different dimension

The dimensions are real, not assigned. We pressure-tested each against the body copy before changing anything. Currency Exchange already names timelines, dependencies, a compliance disclaimer, and three failed explorations. myBCA already runs a survey and lets evidence drive the pivot. Toko Mama is already about peak-traffic workflow. Account Hub is already about a buried entry point. Aryaduta is the only project spanning guest, staff, and reception surfaces. Leading each eyebrow with its strongest existing dimension makes the portfolio read as broader without inventing anything.

### Why "quiet" repositioning

We chose subtle editorial framing over explicit labeling. The eyebrow orients the reader to what a project is fundamentally about, without announcing "this project demonstrates X." Explicit labeling reads as telling the reader how to interpret the work, which is less humble and less senior.

### Why eyebrow grammar is intentionally mixed

The eyebrows mix noun phrases ("Constraints & trade-offs," "Workflow under pressure") and gerund phrases ("Validating an assumption," "Improving discoverability," "Designing across touchpoints"). This was kept on purpose. Eyebrows are seen one per page, never side by side, so per-project accuracy and natural phrasing outrank grammatical symmetry. (Contrast with rail labels, below, which are seen together and therefore must be parallel.)

### Why specific wordings were chosen

- **Account Hub = "Improving discoverability," not "Information Architecture."** The work is genuinely about a buried entry point moved into the bottom nav: discoverability and placement. Calling it IA would imply taxonomy, navigation modeling, or card-sorting the case study does not show. We deliberately chose the more modest, accurate framing. "Improving" also signals a refinement rather than a ground-up redesign, preserving honest scope. We rejected "Navigation Refinement" because "navigation" names the mechanism (bottom nav) rather than the problem (hard to find); discoverability keeps the reader on the problem, which is the more senior framing.
- **Aryaduta = "Designing across touchpoints," not "Connected service design."** Chosen because it is descriptive and grounded in what the project shows (guest app, staff app, receptionist console), whereas "service design" starts to imply a discipline or specialization we did not want to claim. Repositioning Aryaduta also genuinely broadens the portfolio: it is the only multi-surface project, so it adds range without invention.
- **myBCA = "Validating an assumption," not "Research & validation" or "small."** Leo asked to drop "small" because the humility is already carried by the visible methodology and sample size inside the study. "Validating an assumption" describes the activity honestly (he suspected a problem and checked before designing) without implying the rigor that "Research" would, given the sample of eleven. "Evidence-based design" was rejected as a self-applied methodology label.

## Rail labels: bare nouns, parallel

myBCA's rail labels are bare nouns (Gap, Evidence, Tension, Toggle, Outcome), matching the bare-noun style of Currency Exchange and Toko Mama. An earlier version used "The Gap / The Tension / etc."; that was changed because the rail is a persistent, on-screen structural signature seen across all three Rail case studies in one sitting, so it must be grammatically consistent. The mobile section-tag mirrors were aligned to match. In-page section headlines were left as written, because those are content, not navigation.

## Project naming conventions

Each project has **one canonical name used on every card and cross-link**:

- Currency Exchange
- Improving Hold Cart in a High-Traffic POS
- Privacy & Transparency in Money Transfers (myBCA)
- Account Hub Refinement
- Hospitality Service Ecosystem

Earlier the same project appeared under different names across pages (for example Aryaduta as both "Hospitality App & Staff Tools" and "Hospitality Service Ecosystem"). That was fixed because inconsistent self-naming quietly contradicts the portfolio's core claim of caring about details.

### Why hero titles differ from homepage/card names

This is intentional and is **not** an inconsistency. A **card** is a short label a reader skims, so it uses the canonical short name (for example "Currency Exchange"). A **hero H1** is allowed to be a fuller, contextual headline (for example "Currency Exchange, built into nobu Go," or myBCA's "Balancing privacy and transparency in money transfers"). The card-versus-hero distinction is a deliberate convention: short for scanning, fuller for the page itself. The "built into nobu Go" hero was kept long on purpose because it tells the reader at a glance the work shipped into a real product, a credibility signal that belongs in the hero and nowhere else.

## Homepage card taxonomy

Homepage cards use **domain and platform tags** (for example Fintech, Mobile, Tablet, Retail POS, Micro-UX, Independent), which serve a different purpose from eyebrows. Tags give a recruiter a quick domain/platform read; eyebrows orient to a project's dimension. We deliberately kept these two systems separate; turning tags into dimension cues would lose useful domain information. We changed Toko Mama's homepage tag from "UX Case Study" (a format label, and an orphaned term) to "Retail POS" so all homepage cards share a domain/platform taxonomy.

## Aryaduta type label

Aryaduta is labeled a **"Pitch Concept"** consistently (its meta status, its homepage card type, and now its cross-link card in Currency Exchange). One surface previously called it a "Case study"; corrected, because "Pitch Concept" is the honest label.

## BCA scale context

One sentence was added to the opening of myBCA's first section: "myBCA is the mobile banking app of BCA, one of Indonesia's largest banks." This is contextual credibility, not marketing. European readers do not know BCA; one clause converts an unknown app into a real, widely-used product. It was added at the section opening so the hero hook keeps its punch, and phrased modestly ("one of," not "the largest").

## Layout philosophy

Left-aligned editorial grid, generous structural whitespace, restraint everywhere. The centered Contact section is the single intentional exception to the left alignment. One caption per image, each adding information. Interactions: reveal-on-scroll (respecting `prefers-reduced-motion`), card hover (background shift, lime left-border, lime title, corner arrow fills and rotates), every image is a button that opens an accessible lightbox dialog, rail scroll-spy on case studies, mobile hamburger nav. Breakpoints: mobile `max-width: 768px`, tablet `769px to 1024px`, desktop `min-width: 769px`.

## What we intentionally decided NOT to change

- **The repetition** of "120K+ users" and "built design systems from scratch" on the homepage. Trimming it was negligible gain; the phrases reflect genuinely important parts of Leo's experience, and human writing beats over-optimized writing.
- **The mixed eyebrow grammar** (see above).
- **Browser tab title format** varies slightly per page (some include the client, some do not). Negligible hiring impact; left as is.
- **Meta-label variation** across pages (Project/Timeline on myBCA versus Client/Platform elsewhere). This is honest, myBCA says "Project" because it is independent work, not a client brief.
- **The custom cursor.** Noted as a stylistic risk some reviewers love and some find gimmicky, but left in as Leo's choice.
- **The About paragraph's "stay close to engineering" line.** It is concrete and valued by European product teams; it now reads as a supporting detail rather than a competing headline.
- **The systems-thinking gap.** Deliberately not papered over with copy. It is a real evidence gap to be addressed by a future project (see `FUTURE_IDEAS.md`), not by editing this portfolio.
