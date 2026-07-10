# IMAGE_STYLE_GUIDE

The single source of truth for every image produced for this portfolio. Built by reading the actual CSS that will hold each image (border, radius, shadow, hover behavior, aspect ratio) across all six pages, not by inventing a new visual language. Every rule below is either evidence from the existing markup or flagged explicitly as a recommendation that needs confirmation. This document does not redesign anything; it specifies how to fill the slots that `IMAGE_ASSETS.md` already inventoried.

Read this alongside `DESIGN_DECISIONS.md` (the locked design system) and `IMAGE_ASSETS.md` (the per-image checklist). This document is the bridge between them: it says *how* each entry in `IMAGE_ASSETS.md` should look.

---

## 1. Overall visual style

The site's existing visual language is dark, editorial, restrained, and typographic. Every image dropped into it has to read as a quiet supporting actor, not as decoration competing with the text. Three facts from the codebase set the ceiling for image treatment:

- **No box-shadow is ever applied to an image itself.** The only `box-shadow` in the entire site is an ambient hover shadow on the homepage project-card container (`0 20px 60px rgba(0,0,0,.4)`), which is a UI hover affordance, not a property of the image content. Images must therefore be flat, edge-to-edge rectangular crops with no baked-in drop shadow, glow, or vignette of their own.
- **No border-radius on Rail case-study images** (`.shot-frame.ts-hero`, `.shot-frame.ts-sec`: `border: none`, no radius, sharp rectangular corners). **Gallery pages do round their frames** (`.shot-frame.phone`: 20px, `.shot-frame.wide`: 12px, `.shot-frame.lead`: 4px). This is a real, evidence-based difference between the two templates, not an oversight, see section 11.
- **The static border treatment is a 1px hairline** (`var(--border)`, `#1C1C1C`). Nothing else frames an image at rest.
- **Hover/focus interaction (standardized 2026-07-02, unified sitewide 2026-07-03 across Currency Exchange, Toko Mama, myBCA, the homepage's Featured and Other Explorations cards, and every "more work" cross-link card, inherited automatically by future pages)**: one literal `.shot-frame` component reused byte-identically everywhere, not a lookalike per-context system. On hover or keyboard focus: the image or video scales to 1.02 and a dark overlay fades in to 18% opacity, both immediately over 200ms, never fully obscuring the media. A centered pill-shaped text hint ("Click to Preview" for images, "Preview Video" for videos) follows on a staggered, asymmetric timing: a 120ms delay plus 90ms fade-and-slide-up when appearing (210ms total), but an immediate 150ms fade with no delay when disappearing, so hiding feels instant while revealing feels deliberate. Cursor is `zoom-in`. Inside the lightbox, the overlay, hint, and scale are all suppressed, the enlarged view stays a clean static preview. On non-button contexts (homepage cards, cross-link cards, all `<a>`-wrapped navigation rather than lightbox triggers), the shared JS only binds the lightbox-open behavior to actual `<button>` elements, so the identical CSS interaction applies everywhere while click behavior correctly differs by context. This replaced an earlier lime-hairline hover tint (case-study pages) and an icon-only variant (an intermediate homepage-only build), neither of which remain anywhere in the codebase.

Net effect: images should look like they belong inside a minimal editorial frame, not inside a marketing mockup. No drop shadows, no 3D device tilts, no glossy reflections, no floating-device-on-gradient-orb compositions common in SaaS marketing sites. The lime accent (`#C8F135`) is not used anywhere in the hover interaction; it must never be painted into the image content itself (this matches the locked "accent discipline" rule in `DESIGN_DECISIONS.md`: lime is sparing, never a fill).

## 2. Framing and composition rules

- **Rail frames stay edge-to-edge** (`object-fit: cover`, no internal padding). These are composed slides already (section 3); the "breathing room" lives inside the composition itself, between the screen and the slide's own dark backdrop, not as separate frame padding.
- **Gallery frames are matted, not edge-to-edge.** This is a deliberate decision (superseding an earlier draft of this section), see section 4 for the full reasoning and exact values. The screen sits inset within its frame on a consistent dark mat, with the inset amount calibrated by frame type: light for phone screens (legibility-sensitive, small display size), more generous for lead/wide frames (lower information density, more room to breathe).
- Composition is the content's job, not the frame's. A screenshot should be captured/composed so its own internal whitespace and hierarchy reads correctly when cropped to the locked ratio (16:9 for Rail frames and Gallery `wide`/`lead`, 393:852 for Gallery `phone`, 3:2 for homepage/cross-link cards, 4:3 for the About portrait). Don't rely on cropping in production to "fix" a composition shot at the wrong ratio. For Gallery frames, compose to the ratio of the *visible screen area* (the frame ratio minus the mat inset), not the full outer frame, since the mat eats into the usable area.
- For phone screens specifically: the filmstrip displays them at a fixed 240px wide (200px on mobile), and the mat inset (section 4) eats a little further into that. Compose phone screens so their key UI element (the thing the caption is actually about, for example "the toggle" or "the error state") sits in the upper two-thirds of the screen, where it stays legible at filmstrip size, not buried at the bottom behind a keyboard or system chrome.

## 3. Mockup style: two distinct systems, by template

This is the most important structural finding. The Rail and Gallery templates use genuinely different image systems, and that difference is intentional evidence in the CSS, not something to unify.

### Rail (Currency Exchange, Toko Mama, myBCA): composed "deck slide" frames

`PROJECT_STRUCTURE.md` already calls these "deck-slide compositions," and the CSS confirms it: `.shot-frame.ts-hero` and `.shot-frame.ts-sec` are bare 16:9 rectangles with **no device chrome at all**, just a flat colored background (currently a placeholder gradient) with two faint radial lime highlights baked into the hero variant only. There is no phone bezel, no laptop frame, no browser chrome implied anywhere in this template's CSS.

This means Rail images should be **composed presentation slides**, not raw device screenshots: a UI screen (or an annotated detail of one) placed within a designed 16:9 frame, on a dark background consistent with the site, the way a single slide from a case-study deck would look. Annotations, callouts, and "before/after" pairings belong inside this composed frame (see section 9), because the frame itself offers no separate space for them.

### Gallery (Account Hub, Aryaduta): literal device frames

`.shot-frame.phone` is a rounded 393:852 rectangle (20px radius), the exact aspect ratio of a modern phone screen, displayed in horizontal scrolling filmstrips (`.phone-row`). `.shot-frame.wide` (12px radius) and `.shot-frame.lead` (4px radius) hold 16:9 desktop/tablet screens for the Aryaduta receptionist console and both pages' lead images.

This means Gallery images should be **closer to literal screen captures**: one UI state per frame, minimal or no in-image annotation, relying on the `gallery-eyebrow`/`gallery-h2`/`gallery-desc` copy beside each block and the `data-caption` shown in the lightbox to carry context instead of on-image labels. The rounded corners already imply "this is a screen," so the image content shouldn't also draw a fake rounded bezel around itself, that would double up the framing.

**Revised, decided 2026-06-30: Gallery screens are matted, not bled to the frame edge.** An earlier draft of this guide recommended edge-to-edge Gallery images (Option A). After review, that was changed to Option B: the screen sits inset within its rounded frame on a consistent dark mat (see section 4 for exact values), still with zero device chrome, zero bezel artwork, zero decorative framing. The reasoning: edge-to-edge bleed reads closer to a raw app-store screenshot than to the matted, generously-spaced presentation typical of European editorial design portfolios, and it was the one place in the whole system where the image treatment broke from the site's own "generous structural whitespace, restraint everywhere" rule (`DESIGN_DECISIONS.md`). Matting extends that same discipline into the gallery instead of exempting it. This does not make the images any less literal or honest, the screen itself is untouched, only how much dark field surrounds it inside the frame changes.

**Rule of thumb:** if it's Rail, design a slide (breathing room inside the composition). If it's Gallery, mat a screen (breathing room around the capture).

## 4. Background treatment

- **Rail hero and section frames**: dark background consistent with `--bg`/`--bg-card` tones (near-black, `#0A0A0A`-`#111111` range), optionally with the same two soft radial lime highlights the hero placeholder already uses (`rgba(200,241,53,.08)` and `.04`), kept subtle. The UI screen or device sits on top of this dark field with generous breathing room, not edge-to-edge device-only crops.

- **Gallery phone/wide/lead frames: matted, with inset calibrated by frame type (decided 2026-06-30, supersedes the original "fills the frame corner to corner" draft).** Every Gallery frame gets a consistent dark mat (`--bg-card`, `#111111`, flat fill, no gradient or texture) visible as a margin between the rounded frame edge and the screen capture itself. The mat is the only "bezel," there is still no device chrome, no fake hardware, no decorative border art:
  - **Phone frames** (`.shot-frame.phone`, 393:852, displayed at 240px in the filmstrip): **light inset, roughly 4-6% margin on all sides.** This is deliberately the smallest mat in the system, chosen because phone screens are the most legibility-sensitive and smallest-displayed image in the entire portfolio (22 of Aryaduta's 24 images alone are phone frames). The mat should read as a deliberate, considered edge, not eat meaningfully into the screen's own legibility.
  - **Wide and lead frames** (`.shot-frame.wide`, `.shot-frame.lead`, 16:9, displayed up to 1080px): **generous inset, roughly 8-12% margin on all sides.** Lower information density and a much larger display size mean there's real room for the editorial rhythm a deeper mat provides, without cost to readability.
  - Center the screen capture within the mat on both axes. Keep the mat width visually consistent within each frame type across both Gallery pages (Account Hub's phones match Aryaduta's phones, Account Hub's lead matches Aryaduta's lead and wide), the same "one continuous system" rule that already governs the Rail family (section 11).
  - This requires a small CSS change when production starts (today's `.shot-frame > img { object-fit: cover }` fills the frame edge-to-edge with no room for a mat). Production note, not an HTML change made by this document: either give the `<img>` `object-fit: contain` with the mat color as the frame's own `background`, or build the mat into the exported image itself (image canvas at the locked ratio, screen capture composed smaller within it, mat color baked in). Building it into the exported image is the safer choice given the no-build, dependency-free architecture (`PROJECT_STRUCTURE.md`), it needs no CSS change at all and keeps every image self-contained.
- Do not introduce contextual photography backgrounds (desks, hands holding phones, coffee cups, office scenes) anywhere, in either template. Nothing in the current CSS or copy supports that register, and it would clash with the flat, typographic, editorial system. The one exception worth a deliberate conversation is the homepage About portrait, which is real environmental photography, see section 12.

## 5. Shadow and lighting

- **No shadows inside any exported image.** Confirmed by CSS: zero `box-shadow` or `filter: drop-shadow` rules target any `.shot-frame`, `.pip`, `.exp-img`, or `.more-img` element or its content. The only shadow in the system is the ambient card-hover shadow, which is a UI effect applied to the whole card container on hover, not something that should be baked into a screenshot.
- For composed Rail slides (section 3), avoid simulating a shadow under a device or UI panel within the image. Let the dark background and the screen's own contrast do the separating.
- Lighting should read as flat and even, consistent with screenshots and clean product photography, not dramatic raking light or stylized highlights. The only "light" already in the system is the two soft lime radial glows on the Rail hero placeholder; if reproduced, keep them faint (4-8% opacity range, matching the existing values) and decorative, never illuminating the UI content itself.

## 6. Device perspective

- **Always flat-on, zero degrees of rotation or tilt.** Nothing in the CSS implies perspective transforms, 3D tilts, or isometric framing (no `transform: perspective(...)`, `rotateY`, or similar exists anywhere in the shot-frame system). Every frame is a flat rectangle and should be filled with a flat, front-on capture of the UI.
- This applies equally to Rail's composed slides and Gallery's literal screens: even where a Rail slide composes a UI screen onto a backdrop, the screen itself stays perspective-free and front-on, just placed with margin/padding within the frame rather than rotated in space.

## 7. Spacing around devices (Rail composed slides only)

Gallery frames are filled edge-to-edge by the screen itself (section 4), so this section applies to Rail's composed deck slides, where a UI screen sits within a larger 16:9 frame with intentional space around it.

- No CSS value exists yet to pin this down exactly (it lives inside the image, not the markup), so this is a recommendation, not an extracted fact: keep generous, consistent margin around the screen content on all sides, roughly matching the site's own generous-whitespace philosophy (`DESIGN_DECISIONS.md`: "generous structural whitespace, restraint everywhere"). A reasonable starting point is the screen content occupying 55-70% of the frame's width, vertically centered, leaving clear dark margin on either side, similar to how a single phone or screen would sit on a presentation slide.
- Keep this spacing **consistent across every Rail slide on every page**. A reader scrolling Currency Exchange, then Toko Mama, then myBCA should feel one consistent "slide" rhythm, even though the three pages have different section counts (8, 6, and 5 respectively per `DESIGN_DECISIONS.md`).

## 8. Image aspect ratios (already locked, restated here for completeness)

From `DESIGN_DECISIONS.md` and confirmed directly in every file's CSS:

| Use | Ratio | CSS class |
|---|---|---|
| Rail hero and in-page section shots | 16:9 | `.shot-frame.ts-hero`, `.shot-frame.ts-sec` |
| Gallery lead/hero shot | 16:9 | `.shot-frame.lead` |
| Gallery desktop/tablet shots (Aryaduta reception) | 16:9 | `.shot-frame.wide` |
| Gallery phone screens | 393:852 | `.shot-frame.phone` |
| Homepage project/exploration cards, cross-link "more work" cards | 3:2 | `.pip`, `.exp-img`, `.more-img` |
| About portrait | 4:3 | `.about-img-placeholder` |

Do not deviate from these. They are locked in `DESIGN_DECISIONS.md` and the CSS already enforces them via `aspect-ratio` plus `object-fit: cover`, so a wrong-ratio source image will simply get cropped unpredictably rather than break the layout, which makes it an easy mistake to miss without checking.

## 9. Color treatment

- **Screenshots stay true to the real product's actual colors.** Nobu Go, Toko Mama's POS, myBCA, the Nobu account hub, and the Aryaduta concept apps each have their own real or proposed UI palette. Do not desaturate, re-tint, or filter real product screenshots to match the site's lime-on-black palette. Truthfulness about what the product actually looks like outranks visual cohesion here, consistent with the project's core "truthful over impressive" rule.
- **Backgrounds and composed-slide surrounds (Rail template) should sit within the site's existing dark palette**, near `--bg`/`--bg-card` tones, so the frame the screenshot sits inside feels native to the page even though the screenshot content itself is full color.
- **The lime accent (`#C8F135`) must never be added into image content.** It already exists as a hover-state hairline and a couple of very faint background glows in the CSS. Do not paint lime UI callouts, arrows, or highlight boxes into an exported image, if annotation is needed, see section 10 for how that should work without touching the accent color.
- A real, evidence-based inconsistency exists today: Currency Exchange and Toko Mama's in-page placeholder gradients are byte-identical (`#0d1f05`/`#1a3a08` for `.ts-sec`, the same amber `#1a1208`/`#3a2410` for `.ts-alt`) despite being two unrelated clients, while myBCA's placeholders are consistently blue throughout. See section 13 for the full writeup; the practical implication here is that there is currently no per-project "brand tint" convention to preserve in the Rail template's composed-slide backgrounds, only myBCA accidentally has one. Recommend treating all three Rail pages' slide backgrounds identically (the same near-black, optionally with the faint lime glow) rather than inventing a new per-client tint system that doesn't exist anywhere else in the locked design.

## 10. Annotation style

- **Two different annotation registers already exist and should stay separate:**
  - **Below-image captions** (`<figcaption class="shot-caption">` on Rail, `data-caption` shown in the Gallery lightbox): small, uppercase, letter-spaced, `var(--text-muted)` gray, sitting outside the image. This is the system's primary way of adding context to an image, and it already works for every image in the inventory.
  - **On-image overlay labels** (`.pip-label`, `.about-img-label`): exist only on homepage cards, small caps text in low-opacity white (`rgba(255,255,255,.15)` for pip-label), positioned bottom-left inside the frame. This is a much rarer, more decorative device, currently only used for "Client · Year" style tags on the three homepage project cards.
- **In-image annotation (callouts, arrows, highlight boxes) should be reserved for Rail composed slides where the copy explicitly describes an annotated view**, for example Currency Exchange's "Six elements, one screen" (Challenge section) or myBCA's before/after toggle composite. These are the only two image slots in the entire inventory whose captions imply the image itself needs to do explanatory work beyond a straight screenshot.
- When in-image annotation is used, keep it typographically consistent with the site: Inter for any label text, thin hairline connector lines rather than thick arrows, and a neutral white/gray palette, never the lime accent (section 9). Treat it the way a careful designer would mark up a screen for a colleague, not the way a marketing deck adds bold callout bubbles.
- Every other image in the inventory (the large majority) should be a clean, unannotated screen or composed slide. Don't add annotation by default; add it only where the copy already implies it.

## 11. Consistency rules between all case studies

- **Within the Rail family** (Currency Exchange, Toko Mama, myBCA): identical frame treatment (16:9, no radius, no border on the frame itself besides the shared hairline), identical composed-slide background tone, identical caption typography. A reader moving between these three pages should feel one continuous "deck," exactly the way the rail's bare-noun labels are already required to feel parallel (`DESIGN_DECISIONS.md`).
- **Within the Gallery family** (Account Hub, Aryaduta): identical phone-frame radius (20px), identical wide/lead radius (12px/4px), identical filmstrip behavior, and identical mat treatment (section 4: same ~4-6% inset on every phone frame, same ~8-12% inset on every lead/wide frame, same `--bg-card` mat fill). Account Hub's 6 phone screens and Aryaduta's 17 should look like they came from the same camera, not two different photographers.
- **Across families, the frame language is intentionally different (sharp Rail vs. rounded Gallery), and that should not be "fixed."** It is the one place a real, deliberate visual distinction between the two templates already exists in the CSS, and it gives the reader a subconscious cue: "this is a deep narrative" (Rail) versus "this is a lighter, image-led tour" (Gallery). Producing all images with the same mockup style everywhere would erase a distinction the design system already encodes.
- **The homepage card thumbnails and the cross-link "more work" thumbnails must be the same file**, not separate exports per occurrence (already established in `IMAGE_ASSETS.md`). This is as much a consistency rule as a production-efficiency one: if Currency Exchange's card looks different on the homepage than it does on Toko Mama's "more work" row, that reads as a craft mistake to a careful reader, exactly the kind of inconsistency `WORKING_RULES.md` says this audience notices.

## 12. When to use a single device, multiple devices, or a contextual scene

- **Single device/screen**: the default for nearly everything in the inventory. Every Rail in-page shot besides the explorations and full-flow sequence, and every Gallery phone or wide frame, shows exactly one screen state.
- **Multiple devices or states in one frame**: reserved for slots whose caption explicitly compares or sequences something. From `IMAGE_ASSETS.md`, the confirmed candidates are: myBCA's Toggle section ("Before, hidden by default, and revealed with one tap," a before/after composite), and Currency Exchange's "Six elements, one screen" (an annotated single screen, not multiple devices, but multiple callouts on one). Currency Exchange's "full transaction flow" slot is the one genuinely open question, see the flagged decision below.
- **Contextual scenes** (a device shown in an environment, a hand, a desk, a real-world setting): nothing in the current CSS, copy, or design decisions calls for this anywhere in the case-study content. The one image in the entire site that is genuinely contextual/environmental is the About portrait, a real photograph of Leo, which is a different category entirely (a person, not a product), already shot and already working. Do not introduce contextual product photography into any case study; it has no precedent in this system and would clash with the flat, frame-based, no-shadow language documented above.

**Flagged decision, not resolved here:** Currency Exchange's "full transaction flow" slot is described in the copy as "From the nobu Go home screen, through Face ID, to a completed exchange," which is a multi-step sequence, not a single screen. `IMAGE_ASSETS.md` already flagged this as needing a decision between a single composited multi-panel image (consistent with the static `.shot-frame` slot that exists today) or a short looped video/GIF (which would require a small markup change beyond what either inventory document covers). This style guide's position: if it stays a static image, treat it as a "multiple devices/states in one frame" composition, 3-4 key screens arranged left to right within the single 16:9 frame, same flat no-shadow treatment as everything else, not a literal device-in-hand sequence.

## 13. How hero images should differ from supporting images

- **Rail hero** (`.ts-hero`): the only frame in the entire site with a baked-in decorative background effect (two faint radial lime glows). This is a deliberate, evidence-based difference: the hero is allowed one small moment of polish that section images don't get. Keep it subtle (the existing opacity values, 8% and 4%, are the ceiling, not a floor to exceed).
- **Rail section shots** (`.ts-sec`): flat, no glow, otherwise identical framing rules to the hero. The visual hierarchy between hero and section comes from position and size in the page, not from a fancier treatment.
- **Gallery lead shot** (`.shot-frame.lead`): 16:9, smallest border-radius of any Gallery frame (4px, nearly square-cornered), which makes it read as slightly more "serious" or "considered" than the rounded phone screens that follow. No baked-in glow effect exists for this class in the CSS (unlike Rail's hero), so don't add one; let the larger size and top-of-page position alone carry the hero weight.
- **Gallery supporting shots** (`.phone`, `.wide`): plain, no decorative treatment, designed to be read quickly in sequence inside a filmstrip or grid.

## 14. How gallery images should differ from storytelling images

This restates and consolidates sections 3 and 11 because it's a separate question worth answering directly: "storytelling images" here means the Rail template's composed 16:9 slides (Currency Exchange, Toko Mama, myBCA), and "gallery images" means the Account Hub/Aryaduta phone and wide frames.

| | Storytelling (Rail) | Gallery |
|---|---|---|
| What it shows | A composed slide: a UI screen (sometimes annotated) placed on a dark backdrop with deliberate margin | A direct screen capture, matted within its frame on a consistent dark fill (light inset on phones, ~4-6%; generous on lead/wide, ~8-12%) |
| Where the breathing room lives | Inside the composition, between the screen and the slide's backdrop | Between the screen and the frame edge, as a visible mat |
| Corner treatment | Sharp, 0 radius | Rounded (20px phone, 12px wide, 4px lead) |
| In-image annotation | Allowed where the copy implies it (2 of 9 Currency Exchange slots, 1 of 3 myBCA slots) | Not used; context comes from `gallery-eyebrow`/`gallery-h2`/`gallery-desc` copy and the lightbox caption |
| Pacing | One image per narrative beat, the reader scrolls through a story | Many images grouped in filmstrips/grids, the reader scans a set |
| Background | Dark, site-native backdrop behind the screen | None visible, screen fills the frame |

## 15. Export recommendations (PNG / JPG / WebP)

No build step exists or should be introduced (`PROJECT_STRUCTURE.md`, `WORKING_RULES.md`), so whatever format is chosen ships as a plain `<img src>` with no responsive `<picture>`/`srcset` pipeline doing format negotiation automatically. That makes the format choice itself the only lever available, so it's worth getting right once rather than mixing formats ad hoc.

**Recommendation, to confirm with Leo before producing anything:**

- **WebP for all screenshots and composed slides** (the vast majority of the 49 outstanding assets in `IMAGE_ASSETS.md`). WebP gives meaningfully smaller files than JPEG at equivalent visual quality for UI screenshots (large flat color areas, text, sharp edges), which matters because the performance pass in `TODO.md` is explicitly post-restructuring, pre-launch work, and Aryaduta alone is 22 images. Quality setting around 80-85 is a reasonable starting point for screenshots; go lossless or higher quality only if visible banding appears on flat UI gradients.
- **JPEG for the About portrait** (and any future real photography), since it's already a JPEG today (the embedded base64 is JPEG) and photographic images don't get as dramatic a size win from WebP as flat UI screenshots do. Converting it to WebP is a fine secondary optimization but not the priority; extracting it from base64 into any real file is the actual priority (`IMAGE_ASSETS.md`).
- **PNG only if a specific asset needs it**: lossless flat-color graphics or anything requiring transparency (for example, if the favicon or Open Graph image ever needs a transparent background, though OG images are typically opaque JPEGs/PNGs anyway). None of the 49 outstanding case-study assets currently need transparency.
- **Browser support note**: WebP has been supported in every evergreen browser (including Safari) since 2020, and `COPYWRITING_GUIDELINES.md`/`PROJECT_RECAP.md` both confirm the audience is European hiring managers on current professional hardware, so there is no realistic legacy-browser risk here. `TODO.md`'s cross-browser test (Chrome, Safari, Firefox) will confirm this in practice before launch.
- This means `IMAGE_ASSETS.md`'s recommended filenames should use a `.webp` extension for every screenshot/slide entry once this is confirmed, not the `.jpg` placeholder extensions used in that document today. Flagging this explicitly since it's a small but real follow-up edit once the format decision is final.

---

## Visual inconsistencies found that would hurt cohesion if assets were produced today

These are concrete, evidence-based findings from reading the live CSS and HTML, not speculation. Each one would visibly undercut "feels like one system" if real images were produced before resolving it.

1. **Currency Exchange and Toko Mama share byte-identical placeholder gradients.** `.shot-frame.ts-sec` is `linear-gradient(135deg, #0d1f05, #1a3a08, #0a100a)` and `.ts-alt` is `linear-gradient(135deg, #1a1208, #3a2410, #0f0a06)` in both files, despite being two unrelated clients (a fintech bank and a retail POS company). myBCA, by contrast, is consistently blue throughout (`.ts-hero`, `.ts-sec`, and `.ts-alt` all in the same blue family). There is currently no real per-project tint convention, myBCA's blue looks intentional but is actually the odd one out, not the rule. **Resolution recommended in section 9**: don't invent a tint system that doesn't exist; let real screenshots carry each product's real colors instead, and keep all three Rail backgrounds the same neutral dark tone.

2. **The homepage card and cross-link thumbnail gradients are inconsistent with each other for the same project.** Currency Exchange's color alone appears in at least three different gradient value sets across the codebase: `#0d2005/#1a4208` (homepage `.pip-currency`), `#0a2a18/#103e26` (used in Toko Mama's and Account Hub's "more work" cards), and `#062b1a/#0a4d33` (used in myBCA's "more work" card). None of these match. This confirms the placeholders were generated independently per occurrence rather than from one shared source, exactly the failure mode `IMAGE_ASSETS.md`'s "reuse, don't re-export" recommendation is meant to prevent once real images exist.

3. **Toko Mama's "more work" thumbnail accidentally reuses Currency Exchange's exact homepage gradient value** (`#0d2005/#1a4208` appears as Toko Mama's color in both myBCA's and Account Hub's cross-link rows). This is very likely a copy-paste artifact from when these placeholder pages were generated from each other (`CHANGELOG.md` notes Account Hub was "generated from the Aryaduta reference so the CSS and JS stayed byte-identical"), not a deliberate choice. Worth knowing about so it isn't mistaken for an intentional pairing once production starts.

4. **The About portrait's `::before` overlay rule likely never renders.** `.about-img-placeholder::before` applies a decorative radial lime tint, but the element it's attached to is a real `<img>` tag, and `::before`/`::after` pseudo-elements are not rendered on replaced elements like `<img>` in any major browser. This is dead CSS today; it has no visible effect on the real photo already in place. Not urgent, but worth a one-line cleanup note for whoever next touches the About section CSS, listed here rather than acted on since this document doesn't modify HTML.

5. **No agreed device-perspective or mockup-chrome convention currently exists for Aryaduta's 17 phone screens**, which is the single largest and most repetitive block of imagery in the entire portfolio. Because there's no prior real image to calibrate against (every single Aryaduta image is currently an unstyled gradient), there's a higher risk of visual drift across 17 separately-produced screens than anywhere else in the site. This document's section 3 and 6 rules (literal screen capture, flat-on, no chrome) apply with extra weight here precisely because there's no existing real image to course-correct against partway through.

None of these block starting production. They're listed so that whoever produces the first batch of images (most likely Currency Exchange, per `IMAGE_ASSETS.md`'s recommended order) does so against a clean, agreed system rather than against the partially-inconsistent placeholder state that exists today.
