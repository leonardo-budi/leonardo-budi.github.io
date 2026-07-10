# DEFINITION_OF_DONE

What "finished" means for this project, as a checklist. A line is done only when it is true and verified, not merely attempted.

## Status legend

- [x] done and verified
- [ ] not yet done

## Copywriting

- [x] Voice locked and consistent across all six pages (see `COPYWRITING_GUIDELINES.md`)
- [x] All claims truthful and evidence-based; no unmeasured outcomes asserted
- [x] No em dashes anywhere
- [x] One canonical name per project, used on every card and cross-link
- [x] Eyebrows reposition each project to its real dimension (quiet, modest framing)
- [x] BCA scale context added

## HTML

- [x] All six pages content-complete and structurally valid (balanced tags, one H1 each)
- [x] Naming, navigation, footer, and contact consistent across pages
- [x] Internal links resolve case-sensitively (lowercase filenames)
- [x] Design tokens and font imports identical across all files
- [x] Two-template system (Rail, Gallery) applied correctly per page
- [x] Accessible lightbox (dialog role, focus management, Escape), images as buttons, decorative SVGs `aria-hidden`, reduced-motion respected

## Images

- [x] All gradient placeholders replaced with real exports (confirmed across all six pages, zero placeholders remain)
- [x] Locked ratios respected: 16:9 (Landscape Showcase), 3:2 (Portfolio Card), 9:16 (Portrait Device Showcase, standardized 2026-07-03, supersedes the earlier 393x852 spec), 4:3 (About portrait only)
- [x] Meaningful `alt` text on every real image
- [x] `/assets` created and populated with consistent lowercase-hyphen filenames
- [ ] One flagged, unresolved deviation: `hp-ah-card.jpg`/`hp-ar-card.jpg` delivered at 16:9 rather than the locked 3:2 Portfolio Card ratio (see `MASTER_ASSET_TRACKER.md`, `TODO.md`)

## Responsive QA

- [x] Mobile, tablet, and desktop breakpoints present in all files
- [x] Real-device-equivalent pass done with real images in place (rail collapse, phone-row filmstrips, image scaling, no overflow), repeated after the later editorial pass on Homepage/Currency Exchange

## Accessibility

- [x] Keyboard-operable lightbox and navigation in current markup
- [x] Semantic landmarks and heading order
- [ ] WCAG AA contrast re-checked against real images and any overlays/captions
- [ ] Full keyboard and screen-reader pass on the deployed site

## Performance (Lighthouse)

- [ ] Images compressed and correctly sized
- [ ] `width`/`height` set to prevent layout shift; below-the-fold images lazy-loaded
- [ ] Lighthouse run and addressed (performance, accessibility, best practices, SEO)

## Deployment (GitHub Pages)

- [ ] Repo public, Pages enabled
- [ ] Lowercase-filename / case-sensitivity rule confirmed on the live site
- [ ] Every internal link verified on the live URL
- [ ] CV download verified on the live URL
- [x] Favicon (all sizes, SVG + PNG, linked in all six files, 2026-07-09)
- [ ] Open Graph tags and image (may be post-launch; see `TODO.md`)

## Cross-browser

- [ ] Chrome, Safari, Firefox verified
- [ ] Custom cursor degrades gracefully (already off on coarse pointers)

## Definition of "publishable"

The site is publishable when every box above through Deployment is checked. **Images, copy, and HTML are all done; deployment itself is the one remaining gate** for a first publish. Performance, Open Graph/favicon, and custom domain can follow shortly after launch without blocking it (see `TODO.md`). The systems-thinking/OVO evidence gap and the absence of quantified case-study outcomes are known, accepted, and documented as intentional, not items on this checklist (see `SESSION_HANDOFF.md` section 6).
