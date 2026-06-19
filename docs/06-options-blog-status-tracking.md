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

## Phase 3 — Structure & Navigation

**Status:** Not started

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
