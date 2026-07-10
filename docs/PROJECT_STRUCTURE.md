# PROJECT_STRUCTURE

How the project is organized on disk, how it is named, and what to know for deployment.

## Current folder structure

```
/ (repo root, also the GitHub Pages root)
  index.html                                   homepage, entry point, served at /
  study-case/
    currency-exchange/index.html                Rail case study
    toko-mama/index.html                         Rail case study
    mybca/index.html                             Rail case study
    (each study-case/<project>/ also has its own assets/ subfolder)
  visual-lab/
    account-hub/index.html                       Gallery case study
    aryaduta/index.html                          Gallery case study
    (each visual-lab/<project>/ also has its own assets/ subfolder)
  CV/
    LeonardoBudi_CV2026_EU.pdf
  assets/                                        site-wide images, icons, videos (not yet populated)
  docs/                                          this documentation
  references/                                    source material, not shipped (screenshots, old designs, exports, inspiration)
```

This is a deliberate, intentional nesting (not a flat single-directory layout). The homepage stays at the repo root because GitHub Pages requires `index.html` at the root to serve the site at `/`; every case study lives one level deeper under `study-case/` or `visual-lab/`, each in its own named folder.

## HTML organization

Every page is a single self-contained `.html` file. Inside each file, in order: `<head>` with meta, Google Fonts link, and a full inline `<style>` block; then `<body>` with the page markup; then a single inline `<script>` block at the end. There are no external CSS or JS files. This is deliberate: a no-build, dependency-free static site that anyone can open by double-clicking.

Design tokens (`:root` custom properties) and the shared component CSS are duplicated in every file. There is no shared stylesheet. A token or shared-component change must therefore be made in all six files. When editing shared CSS, change every file and verify they stay identical.

## Internal link conventions (relative paths)

Because pages live at different folder depths, every internal link is a **relative path computed from that file's location**, not a bare filename:

- From the **homepage** (`index.html` at root) to a case study: `href="study-case/currency-exchange/index.html"`, `href="visual-lab/account-hub/index.html"`, etc. CV: `href="CV/LeonardoBudi_CV2026_EU.pdf"`.
- From a **case study** (one level under `study-case/` or `visual-lab/`, so two levels deep) back to the homepage: `href="../../index.html"`. To the CV: `href="../../CV/LeonardoBudi_CV2026_EU.pdf"`.
- From a case study to a **sibling in the same folder** (e.g. Currency Exchange to Toko Mama, both under `study-case/`): `href="../toko-mama/index.html"`.
- From a case study to a project in the **other** folder (e.g. Currency Exchange under `study-case/` to Aryaduta under `visual-lab/`): `href="../../visual-lab/aryaduta/index.html"`.

When adding a new page or a new cross-link, work out the relative path from the actual folder depth of both files; do not assume a flat sibling relationship.

## Assets organization

**All imagery is now real production exports; no CSS gradient placeholders remain anywhere in the site.** Each project folder has its own `assets/` subfolder (e.g. `study-case/currency-exchange/assets/`) for project-specific exports; the root `/assets` holds site-wide images (homepage cards, the About portrait once it's extracted from inline base64). If you're wiring a new image into an existing or new `.shot-frame` button:

- Place project-specific exports in that project's own `assets/` subfolder; site-wide assets go in the root `/assets`.
- Wire an `<img>` inside the `.shot-frame` button; the hover-zoom and lightbox already expect this.
- Respect the locked ratios: 16:9 (Landscape Showcase) for case-study/hero/section frames, 3:2 (Portfolio Card) for cards, 9:16 (Portrait Device Showcase) for Gallery phone frames, 4:3 for the About portrait only. The phone-frame ratio was standardized to 9:16 on 2026-07-03, superseding an earlier 393x852 spec, see `FIGMA_PRODUCTION_GUIDE.md` section 1 for the full ratio system and the reasoning.
- Rail case studies (Currency Exchange, Toko Mama, myBCA) use 16:9 frames that map to deck-slide compositions. Gallery pages (Account Hub, Aryaduta) use 9:16 phone frames in horizontal `phone-row` filmstrips.
- Add meaningful `alt` text on every real image. Decorative SVGs stay `aria-hidden`.

## Naming conventions

- **Folder and filenames are all lowercase**, words separated by hyphens (`account-hub`, `currency-exchange`). The myBCA folder is `mybca`, lowercase, to match this convention and the links that point to it.
- **Project display names** have one canonical form each; see `DESIGN_DECISIONS.md`.
- **Asset filenames** follow the same lowercase-hyphen convention. In-page case-study assets use an asset-ID prefix, for example `ce-01-hero.jpg`, `ce-04-challenge.jpg` (see `docs/FIGMA_PRODUCTION_GUIDE.md` section 4). Site-wide assets (card thumbnails, the about portrait) keep a project prefix instead, for example `mybca-toggle-before-after.jpg`.

## Deployment considerations (GitHub Pages)

- The repo root is the site root; `index.html` is served at `/`. Every case study is served at its nested path, for example `/study-case/currency-exchange/` (or `/study-case/currency-exchange/index.html`).
- **Case sensitivity is the critical gotcha.** GitHub Pages runs on Linux, which is case-sensitive. macOS is case-insensitive, so a wrong-case link or folder name works locally and 404s in production. All folder names, filenames, and links must match exactly, in lowercase. This is why the myBCA folder is `mybca` and why every internal link was verified case-sensitively.
- If a folder or file is ever created with the wrong case, force the rename with `git mv` (a plain rename can be silently ignored by git on macOS for case-only changes), then confirm on GitHub that it shows as lowercase. Do not let both cases coexist.
- All internal links are relative and depth-aware (see "Internal link conventions" above), which works correctly under a project-pages subpath too.
- The CV (`CV/LeonardoBudi_CV2026_EU.pdf`) must be present at that path under the repo root; it is linked from every page (with the correct relative depth) and opens in a new tab with `rel="noopener noreferrer"`.
- External links (LinkedIn) already use `target="_blank"` and `rel="noopener noreferrer"`.

## Future file organization

If the project grows (for example a future systems case study), keep this nested structure: a new lowercase-hyphen folder under `study-case/` or `visual-lab/` containing its own `index.html` and `assets/`, the same duplicated tokens and shared CSS, and the same two-template system. Compute relative links from the new folder's actual depth, exactly as described above. Do not introduce a build step, a framework, or a shared stylesheet without a deliberate decision, because the no-build simplicity is a feature.
