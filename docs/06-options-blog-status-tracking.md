# Status Tracking
## Stochastic Waltz — An Options & Quantitative Finance Blog

**Document type:** Status Tracking  
**Updated:** June 2026

---

## Purpose

A running log of what was planned, what was actually built, decisions made, and outstanding items for each phase. Updated at the end of every phase.

---

## Phase 1 — Environment Setup ✅

**Completed:** June 2026

### What was done
- Installed Quarto 1.9.38 via Homebrew
- Created conda environment `stochwaltz` (Python 3.11) with core dependencies: jupyter, matplotlib, plotly, numpy, pandas, scipy
- Built the full Quarto project skeleton: `_quarto.yml`, `index.qmd`, `about.qmd`, `404.qmd`, `.gitignore`, `requirements.txt`, six topic folders under `posts/`
- Connected to GitHub at `https://github.com/danielobembe/stochastic-waltz` via SSH
- Initial commit pushed

### Decisions made
- Docs folder (`docs/`) created to house planning documents — not listed in original file structure, added as a deviation
- GitHub repo initialized with MIT license; CC BY 4.0 to be noted on About page for post content

### Outstanding items carried forward
- None

---

## Phase 2 — Design Implementation ✅

**Completed:** June 2026

### What was done
- Switched base Quarto theme from `cosmo` to `litera` — closest match to dhblog's clean white aesthetic
- Rewrote `styles/styles.scss` from scratch: color palette, typography, navbar, sidebar, post cards, code blocks, equation spacing
- Restructured navbar: removed Posts/Topics/About links; now has About + LinkedIn + GitHub + search + dark mode toggle on the right only
- Fixed sidebar to show clean section headers only (no duplicate child entries)
- Removed `_metadata.yml` placeholder files from topic folders
- Restructured placeholder posts into correct subfolder format (`posts/<topic>/<slug>/index.qmd`)
- Added two placeholder posts with realistic chart thumbnails generated via matplotlib:
  - `posts/algorithmic-trading/backtesting-a-strategy/` — GBM price series thumbnail
  - `posts/greeks-hedging/delta-hedging-vanilla-option/` — implied vol surface thumbnail
- Updated Design Brief (v1.1) to reflect actual decisions made

### Decisions made
- **Primary visual reference changed** from quantgirluk (Jupyter Book / PyData theme — not replicable in Quarto) to dhblog (native Quarto blog using `litera` theme)
- **Layout**: dhblog-style visual aesthetic + quantgirluk-style left sidebar topic hierarchy
- **Navbar**: sidebar handles all topic navigation; navbar is minimal (blog name + utility icons only)
- **Background color**: `#ffffff` pure white (changed from `#fafaf8` warm off-white in original brief)
- **Text color**: `#222832` (adopted from PyData theme)

### Outstanding items carried forward
- **Dark mode deferred** — toggle is present but non-functional. Full dark mode requires resolving CSS specificity conflicts between `litera` (light) and `darkly` (dark) Quarto themes. Both currently set to `litera` as a placeholder.
- **Sidebar section styling** — section names could benefit from a subtle visual treatment to distinguish them as labels vs links; minor, deferred to Phase 3

---

## Phase 3 — Structure & Navigation ✅

**Completed:** 25 June 2026

### What was done

- **Task 1 — Sidebar structure**: Explicit post contents wired into `_quarto.yml` for Foundations, Greeks & Hedging, and Algorithmic Trading sections; empty sections (Volatility Models, Pricing & Valuation, Numerical Methods) retain header-only entries as placeholders
- **Task 2 — Homepage feed**: 5 posts rendering in reverse chronological order with thumbnails, category pills, and descriptions; categories panel visible on the right
- **Task 3 — Categories panel**: Verified — clicking a category filters the feed
- **Task 4 — Article layout**:
  - All 5 posts updated with realistic body content distinct from their description
  - Section headings added to each post, enabling right-side TOC (`toc: true`, `toc-depth: 3`)
  - `reading-time: true` enabled in `_quarto.yml`
  - Category pills on article pages styled to match homepage cards (`.quarto-category`)
  - Collapsible revision history block added to all posts — `<details>` element with `--sw-code-bg` tinted background, preceded by a full-width `hr.revision-divider`
  - Quarto's native BibTeX citation system added to all posts — one `references.bib` per post folder, `nocite: '@*'` to list all entries; styled References section (small, muted, uppercase label)

### Decisions made

- **References system**: Quarto native BibTeX (`bibliography: references.bib` per post) chosen over manual markdown lists — better suited to academic/quant finance content
- **Revision history placement**: Below References, separated by `hr.revision-divider`
- **HR divider**: Uses `margin-left: calc(-1 * var(--bs-gutter-x, 1.5rem))` for responsive full-width alignment with the sidebar border
- **Reading time**: Will only display on posts with sufficient word count — not visible on current short placeholder posts; expected to appear naturally on real content

- **Task 5 — About page**: Implemented using Quarto's `jolla` about page template — circular photo centered at top, bio below, LinkedIn and GitHub pill buttons at bottom; bio text overridden to left-align via `.quarto-about-jolla main p` CSS; `sidebar: false` set to suppress left nav on this page
- **Task 6 — 404 page**: Verified — renders cleanly with a clear message and link back to homepage; no changes needed

### Decisions made

- **About page layout**: Changed from Design Brief's original "photo left-aligned with text wrapping" to dhblog-style centered layout (photo centered, bio centered below); Design Brief updated to reflect this
- **About page photo**: Using cartoon illustration (`profile_with_lola.png`) — photo of author and cat; `assets/` folder created to house profile photos
- **About page template**: Quarto `jolla` template chosen for the centered photo/bio layout
- **404 page**: Kept minimal — title + one-line message + homepage link; consistent with blog's restraint principle
- **`site-url` warning**: Pre-existing warning about missing `site-url` for RSS feed — harmless for now, to be resolved in Phase 4 when site URL is configured

### Outstanding items carried forward

- **Dark mode**: Still deferred from Phase 2 — toggle present but non-functional
- **`site-url`**: To be added in Phase 4 when configuring RSS and analytics

---

## Phase 4 — Third-Party Integrations

**Status:** Not started

---

## Phase 5 — First Content

**Status:** Not started

---

## Phase 6 — Launch

**Status:** Not started

---

*End of Status Tracking*
