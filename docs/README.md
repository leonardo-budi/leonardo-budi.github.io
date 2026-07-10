# Project documentation

Long-term documentation for Leo's portfolio. If you are a new session picking this up, read in this order.

1. **SESSION_HANDOFF.md**: the current source of truth for architecture, implementation status, and exactly what copy has changed and why. Start here if you're a new session, it supersedes the older `PROJECT_RECAP.md` framing below wherever the two disagree.
2. **WORKING_RULES.md**: how to work on it. The non-negotiables.
3. **DESIGN_DECISIONS.md**: every intentional decision and its reasoning. Do not reopen these.
4. **COPYWRITING_GUIDELINES.md**: the writing voice, with examples.
5. **PROJECT_STRUCTURE.md**: files, naming, and deployment (including the case-sensitivity rule).
6. **TODO.md**: what's left. All six pages are fully implemented; nothing here gates launch except the actual deploy. Recommended order: deploy, known/accepted gaps, small polish, technical QA, future improvements, deferred systems audit.
7. **DEFINITION_OF_DONE.md**: the checklist for "finished."
8. **CHANGELOG.md**: how the project got here.
9. **SESSION_LOG.md**: dated, session-by-session log of work and verification, more granular than `CHANGELOG.md`. Living document, updated at the end of every significant session.
10. **IMAGE_ASSETS.md**: complete inventory of every visual asset across all six pages: current status, recommended filename and dimensions, dependencies, and production priority. The checklist for replacing placeholders with real exports.
11. **IMAGE_STYLE_GUIDE.md**: the production design system for portfolio imagery, derived from the existing CSS (framing, mockup style, shadows, ratios, color treatment, export format). The single source of truth for *why* every image in `IMAGE_ASSETS.md` should look the way it does.
12. **FIGMA_PRODUCTION_GUIDE.md**: the Figma-side production system, artboard sizes, export resolutions, naming, folder structure, reusable components. The single source of truth for the concrete *numbers* behind every creative brief, so individual briefs only document what's asset-specific.
13. **blueprints/**: one complete, page-ordered production checklist per page (asset IDs, composition, effort, build order): `blueprints/currency-exchange.md`, `blueprints/mybca.md`, `blueprints/toko-mama.md`, `blueprints/homepage.md`, `blueprints/aryaduta.md`, `blueprints/account-hub.md`. The working checklist for producing a page's images in Figma start to finish. Every page now has one.
14. **FUTURE_IDEAS.md**: postponed ideas that must not touch the current locked portfolio.

## The one-paragraph summary

A static, no-build HTML portfolio for a Senior Product Designer targeting European product-led companies. Six pages, two templates (Rail and Gallery), a locked dark editorial design system, and a deliberately honest, modest voice. **All six pages are fully implemented** (every image, video, and interaction wired). The Homepage and Currency Exchange have also been through a hiring-manager review and a full editorial pass in response to it; Toko Mama, myBCA, Account Hub, and Aryaduta have not, and their copy is unchanged since original lock. The only remaining hard gate before publishing is the GitHub Pages deploy itself. The single biggest future opportunity, a design-systems case study, is a separate audit project, not edits to these pages, see `TODO.md`.

## Two rules that override everything

- Truthful over impressive. Never invent evidence; surface what already exists.
- No em dashes, anywhere.
