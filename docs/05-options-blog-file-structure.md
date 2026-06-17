# File & Folder Structure
## Stochastic Waltz — An Options & Quantitative Finance Blog

**Document type:** File & Folder Structure  
**Status:** Draft v1.0  
**Prepared:** June 2026  
**Companion documents:** Design Brief v1.0, Technical Specification v1.0, Development Plan v1.0

---

## 1. Overview

This document describes the complete file and folder structure for the Stochastic Waltz Quarto project. It is intended to be read alongside the Development Plan — Phase 1 (Environment Setup) and Phase 3 (Structure & Navigation) in particular depend on this structure being in place.

Every folder and file listed here has a stated purpose. Claude Code should not create files or folders outside this structure without flagging the deviation.

---

## 2. Top-Level Structure

```
stochastic-waltz/
│
├── CLAUDE.md                    # Auto-loaded by Claude Code — project orientation and behavioral instructions
│
├── docs/                        # Project planning and reference documents (not part of the Quarto site)
│   ├── 01-options-blog-project-brief.md
│   ├── 02-options-blog-design-brief.md
│   ├── 03-options-blog-technical-spec.md
│   ├── 04-options-blog-development-plan.md
│   └── 05-options-blog-file-structure.md
│
├── _quarto.yml                  # Master site configuration
├── index.qmd                    # Homepage — chronological post feed
├── about.qmd                    # About page — standalone, not in sidebar
├── 404.qmd                      # Custom 404 page
├── requirements.txt             # Python dependencies
├── .gitignore                   # Git ignore rules
│
├── posts/                       # All blog posts, organized by topic
│   ├── foundations/
│   ├── volatility-models/
│   ├── pricing-valuation/
│   ├── greeks-hedging/
│   ├── numerical-methods/
│   └── algorithmic-trading/
│
├── styles/
│   └── styles.scss              # Custom SCSS — implements Design Brief palette, typography, spacing
│
├── assets/
│   ├── plot_theme.py            # Shared Matplotlib/Plotly theme (Okabe-Ito palette, white backgrounds)
│   ├── og-default.png           # Default Open Graph image for social sharing
│   └── profile-photo.jpg        # Author photo for About page
│
└── _extensions/                 # Quarto extensions if needed (e.g. custom shortcodes)
```

---

## 3. Posts Folder — Detail

Each topic folder contains the posts that belong to that section of the textbook hierarchy. Every post lives in exactly one topic folder.

```
posts/
│
├── foundations/
│   ├── _metadata.yml            # Shared front matter defaults for this section
│   └── intro-to-options/
│       ├── index.qmd            # Post content
│       └── thumbnail.png        # Post thumbnail (~160×100px, used in homepage feed)
│
├── volatility-models/
│   ├── _metadata.yml
│   └── heston-model/
│       ├── index.qmd
│       └── thumbnail.png
│
├── pricing-valuation/
│   ├── _metadata.yml
│   └── black-scholes-derivation/
│       ├── index.qmd
│       └── thumbnail.png
│
├── greeks-hedging/
│   ├── _metadata.yml
│   └── delta-hedging-pnl/
│       ├── index.qmd
│       └── thumbnail.png
│
├── numerical-methods/
│   ├── _metadata.yml
│   └── monte-carlo-pricing/
│       ├── index.qmd
│       └── thumbnail.png
│
└── algorithmic-trading/
    ├── _metadata.yml
    └── vol-targeting-strategy/
        ├── index.qmd
        └── thumbnail.png
```

### Notes on post folder conventions
- Each post lives in its own subfolder named with a short, lowercase, hyphenated slug (e.g. `heston-model`, `black-scholes-derivation`)
- The post content file is always named `index.qmd` — this produces clean URLs (e.g. `/posts/volatility-models/heston-model/` rather than `/posts/volatility-models/heston-model.html`)
- Each post folder contains its own `thumbnail.png` — the image shown on the homepage feed card
- Any additional assets specific to a post (data files, supplementary images, standalone HTML figures) live in the same post folder alongside `index.qmd`
- `_metadata.yml` in each topic folder sets shared front matter defaults for all posts in that section (e.g. default author, default categories seed)

---

## 4. Post Front Matter Template

Every post `.qmd` file begins with this YAML front matter block:

```yaml
---
title: "Post Title Here"
date: "2026-06-03"
categories: [category-one, category-two]
description: "A 1–2 sentence description used in the homepage feed excerpt and meta tags."
image: thumbnail.png
---
```

### Front matter fields
- `title` — displayed as the H1 on the article page and as the post title on the homepage feed card
- `date` — the original publication date; update this field when the post is revised, and add a revision history entry at the bottom of the post
- `categories` — one or more tags; a post can have multiple categories even though it lives in one topic folder
- `description` — used as the homepage feed excerpt and as the HTML meta description for SEO
- `image` — path to the thumbnail image; relative to the post folder

---

## 5. Key Configuration Files

### `_quarto.yml`
The master site configuration file. Controls:
- Site title (`Stochastic Waltz`)
- Navigation bar (blog name, Posts / Topics / About links, light/dark toggle)
- Left sidebar topic hierarchy (pointing to each topic section)
- Theme base (`cosmo`) and custom SCSS reference (`styles/styles.scss`)
- Open Graph global tags
- RSS feed configuration
- Plausible Analytics script injection
- KaTeX equation rendering
- Per-page table of contents (right sidebar on article pages)

### `styles/styles.scss`
Custom SCSS that overrides the Bootswatch base theme. Implements:
- Full light mode color palette (see Design Brief Section 6)
- Dark mode color overrides
- System font stack for body, headings, code, and UI elements (see Design Brief Section 5)
- Type scale (font sizes, weights, line heights)
- Layout widths and spacing (720px content max-width, 8px base unit)
- Post card styles
- Code block styles (background, language label, copy button)
- Left sidebar active state (3px accent border)
- Equation vertical padding

### `assets/plot_theme.py`
A shared Python module imported at the top of every post that contains code-based visualizations. Defines:
- A Matplotlib style dictionary with white/transparent backgrounds, thin gray axes, and minimal tick marks
- A Plotly layout template with the same conventions
- The Okabe-Ito color palette as a named list for use in both Matplotlib and Plotly
- Helper functions for applying the theme consistently

### `_metadata.yml` (per topic folder)
Sets default front matter for all posts in a section. Minimal — typically just:
```yaml
author: "Author Name"
```

---

## 6. `.gitignore`

At minimum, the `.gitignore` should exclude:

```
# Python
__pycache__/
*.pyc
.venv/
/conda-env/

# Quarto
/.quarto/
/_site/

# OS
.DS_Store
```

The rendered site (`/_site/`) is excluded from the main branch because GitHub Pages is served from the `gh-pages` branch, which `quarto publish gh-pages` manages separately.

---

## 7. URL Structure

The folder structure above produces the following URL pattern on the live site:

| Page | URL |
|---|---|
| Homepage | `/` |
| About | `/about.html` |
| Topic section (foundations) | `/posts/foundations/` |
| Individual post | `/posts/volatility-models/heston-model/` |
| RSS feed | `/index.xml` |
| Sitemap | `/sitemap.xml` |

---

*End of File & Folder Structure v1.0*
