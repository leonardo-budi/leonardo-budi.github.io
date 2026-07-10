# PROJECT_RECAP

Background and positioning context. For current implementation status and exactly what copy has changed, read `SESSION_HANDOFF.md` first, it's the current source of truth; this file covers the "why" behind the project that doesn't change session to session.

## What this is

A personal design portfolio for **Leonardo Budi Kurniawan (Leo)**, a Senior Product Designer with roughly 12 years of experience in fintech and consumer apps, based in Norrkoping, Sweden.

It is a **static website**: plain HTML, CSS, and a small amount of vanilla JavaScript. No framework, no build step, no dependencies. Each page is one self-contained `.html` file with an inline `<style>` block and an inline `<script>` block. Design tokens are duplicated in the `:root` of every file. Pages link to each other with relative paths. The aesthetic is dark and editorial.

Contact used across the site: `hello.leonardobudi@gmail.com`, `linkedin.com/in/leonardobudi`, and a CV file linked from every page.

## Why this portfolio exists

Leo is job-hunting for Senior Product Designer roles. The portfolio's job is to get him **read as senior within about ten seconds** and earn an interview invitation. The site itself is a craft sample, so build quality and editorial restraint are part of the argument, not decoration.

The guiding strategy is **depth over breadth**: a few complete, honest narratives that show judgment, trade-offs, and even dead ends, rather than a wall of thumbnails. Recruiters reward demonstrated thinking, not volume.

## Target audience

Recruiters, hiring managers, and design leads at **European, product-led companies**. Primary geography: Sweden (Stockholm, Gothenburg), wider Europe, and fully remote European roles. The information hierarchy and copy are tuned to how those readers skim and what they value.

Two facts about this audience shape the whole portfolio:
1. They will **not recognize the client names** (Nobu Bank, BCA, OVO, Aryaduta, Toko Mama are Indonesian). Scale context has to be supplied where it matters.
2. Leo needs **work-permit sponsorship**, which the contact section states plainly and honestly upfront.

## Overall positioning

A senior fintech designer who makes complex money flows feel simple without hiding what matters, who works close to engineering, and who is honest about outcomes. Tone anchors as of the most recent editorial pass: "Complex problems. Clear decisions.", "The principles behind my work.", "I care about the details no one sees." (the earlier "Works I'm proud of" / "What you actually get" headings have since been rewritten, see `SESSION_HANDOFF.md` section 5 for the current copy).

A known positioning ceiling, diagnosed and deliberately deferred (see `FUTURE_IDEAS.md` and `TODO.md`): Leo's strongest claim is **systems thinking / design systems**, corroborated by two of three testimonials about the OVO design system, but **no current case study shows systems work**. The portfolio currently reads as a clear Senior, not yet Staff. This was flagged in an early review and independently reconfirmed by a second, later hiring-manager review; closing the gap for real (a real Design Systems case study) remains a separate future project, not something editorial work can fix. What editorial work *could* fix, the testimonials reading as disconnected from the rest of the site, was addressed on 2026-07-08, see `SESSION_HANDOFF.md`.

## Current project status

**Every page is fully implemented**: all images, video, and interaction wired across all six pages, no placeholders remain. The Homepage and Currency Exchange have also been through a hiring-manager review and a full editorial pass in response to it. Toko Mama, myBCA, Account Hub, and Aryaduta are implemented but haven't been through that same review pass; their copy is unchanged since the original lock described below. See `SESSION_HANDOFF.md` for exact current state and `TODO.md` for what's left (the only remaining hard gate is the GitHub Pages deploy itself).

## Folder structure

Nested by project type, which becomes the GitHub Pages repo root. `index.html` (the homepage) stays at the repo root so GitHub Pages can serve it at `/`; every case study lives one level deeper under `study-case/` or `visual-lab/`, each in its own named folder. See `PROJECT_STRUCTURE.md` for detail.

```
/ (repo root)
  index.html
  study-case/
    currency-exchange/index.html
    toko-mama/index.html
    mybca/index.html
  visual-lab/
    account-hub/index.html
    aryaduta/index.html
  CV/LeonardoBudi_CV2026_EU.pdf
  /assets        (real production images and video, fully populated)
  /docs          (this documentation)
```

## All HTML pages

| Page | File | Template | Role |
|---|---|---|---|
| Homepage | `index.html` | Homepage (unique) | Entry point, routes to all work |
| Currency Exchange | `study-case/currency-exchange/index.html` | Rail | Flagship case study (deepest) |
| Toko Mama | `study-case/toko-mama/index.html` | Rail | Operational case study |
| myBCA | `study-case/mybca/index.html` | Rail | Research/validation micro-study |
| Account Hub | `visual-lab/account-hub/index.html` | Gallery | Discoverability refinement |
| Aryaduta | `visual-lab/aryaduta/index.html` | Gallery | Multi-touchpoint pitch concept |

Two templates exist. **Rail**: deep case studies with a sticky left section nav and scroll-spy, collapsing to inline section tags on mobile. **Gallery**: lighter, image-led, no rail. See `DESIGN_DECISIONS.md`.

Folder convention is **all lowercase**. The myBCA folder is `mybca` (lowercase), not `myBCA`. This matters on case-sensitive servers; see `PROJECT_STRUCTURE.md`.

## Current navigation structure

- **Homepage (`index.html`)**: section-based. Hero, Selected Work (the three deep case studies), Other Explorations (the two lighter Gallery pieces), About, How I Work (formerly labeled "Strengths"), Testimonials, Contact.
- **Case studies**: a top nav with "Back to Home" (to `index.html`) and the "Leo." logo (also to `index.html`). Rail pages additionally have a sticky left rail with scroll-spy that links to in-page sections. Each page ends with a "More work" block cross-linking to two other case studies, then a centered Contact block.
- **Cross-linking map**: homepage links to all five case studies. Currency Exchange links to Toko Mama + Aryaduta. Toko Mama links to Currency Exchange + myBCA. myBCA links to Currency Exchange + Toko Mama. Account Hub links to Currency Exchange + Toko Mama. Aryaduta links to Account Hub + Currency Exchange.

## What has been completed

- All six pages built, content-complete, and **fully implemented with real production images, video, and interaction** (no placeholders remain anywhere in the site).
- Two new pages authored early in this effort: myBCA (Rail, five sections) and Account Hub (Gallery).
- Critical consistency fixes: canonical project naming everywhere; homepage overclaim removed; myBCA rail labels aligned.
- Editorial repositioning: all five case-study eyebrows lead with each project's distinct dimension.
- A second hiring-manager review, later in the project, followed by a full editorial pass on the Homepage and Currency Exchange specifically (thesis de-duplication, testimonial reordering and re-bridging, Explorations rhythm, pronoun consistency). See `SESSION_HANDOFF.md` section 5 for exactly what changed.
- Filename casing corrected to lowercase `mybca.html`.
- Full cross-page QA passed (naming, nav, footer, contact, links, tokens, fonts, responsive breakpoints, em-dash rule, heading hierarchy), repeated after the later editorial pass.

## What remains

The only hard gate: deploy to GitHub Pages and verify every link and the CV download live. Everything else is small polish, honest open questions already documented as intentional, or the larger deferred systems audit. See `TODO.md` for the current, prioritized list and `SESSION_HANDOFF.md` for full context.

Explicitly **not** remaining: inventing metrics that don't exist, editing a testimonial's actual wording, or adding new templates, fonts, or accent colors. The portfolio direction is settled; targeted editorial refinement (as opposed to a narrative rewrite) is an accepted, ongoing activity, not something to avoid.
