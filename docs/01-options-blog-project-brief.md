# Project Brief
## Stochastic Waltz — An Options & Quantitative Finance Blog

**Document type:** Project Brief  
**Status:** Draft v1.0  
**Prepared:** June 2026

---

## What This Project Is

Stochastic Waltz is a minimalist, white, academic-style blog covering options pricing, volatility modeling, algorithmic trading, and quantitative finance. It is rigorous enough for practitioners and researchers, yet public and openly accessible.

The blog has a dual identity: organized like a graduate-level textbook (by topic) and updated like a blog (by date). Both views coexist without conflict.

---

## Stack

| Layer | Choice |
|---|---|
| Publishing framework | Quarto |
| Language | Python |
| Environment manager | conda |
| Source control | GitHub |
| Hosting | GitHub Pages |

---

## Project Documents

Supporting documents — read in this order after this brief:

1. **Design Brief** — visual design, layout, typography, color palette, information architecture
2. **Technical Specification** — hosting, analytics, comments, RSS, email, SEO, performance
3. **Development Plan** — the six-phase build sequence, tasks, and definitions of done
4. **File & Folder Structure** — the complete project file tree, naming conventions, and URL structure

---

## Key Conventions

- **Folder naming:** lowercase, hyphenated slugs (e.g. `volatility-models`, `heston-calibration`)
- **Post files:** always named `index.qmd` inside their own subfolder — produces clean URLs
- **Python environment:** conda — ask the user for the environment name before creating it
- **Fonts:** system font stack — no external fonts loaded
- **Plot theme:** all visualizations use the shared `assets/plot_theme.py` (Okabe-Ito palette, white backgrounds)
- **Do not** create files or folders outside the structure defined in the File & Folder Structure document without flagging it first

---

## Current Status

| Phase | Description | Status |
|---|---|---|
| Phase 1 | Environment Setup | Complete |
| Phase 2 | Design Implementation | Complete |
| Phase 3 | Structure & Navigation | Not started |
| Phase 4 | Third-Party Integrations | Not started |
| Phase 5 | First Content | Not started |
| Phase 6 | Launch | Not started |

---

*End of Project Brief v1.0*
