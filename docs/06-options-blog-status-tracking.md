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

**Status:** In progress  
**Last updated:** 3 July 2026

### What was done

- **Task 4 (RSS Feed)**: `site-url` added to `_quarto.yml` (resolves the pre-existing feed warning); feed configured with 20 items, full type; RSS link added to site footer (bottom-left)
- **Task 6 (Open Graph / SEO)**: `open-graph` block added to `_quarto.yml` with site title, description, and default image; `assets/og-default.png` generated — stochastic GBM paths on dark background with $P_t$ / $t$ axes
- **Task 7 (Privacy notice)**: One-line notice added to site footer (bottom-right): "This site uses Plausible Analytics — no cookies, no personal data collected."
- **About page updates**: Title changed to "About me"; author name updated to "Ayo"
- **Task 3 (Giscus comments)**: GitHub Discussions enabled on the repo; Giscus GitHub App installed; comment widget configured with `mapping: pathname`, `category: Announcements` (restricts new thread creation to the maintainer, preventing spam). Implemented via Quarto's native `comments.giscus` key in `posts/_metadata.yml` — first attempt used `include-after-body` script injection, which rendered outside the page grid (misaligned, appeared below the footer); corrected to use Quarto's native support, which places the widget correctly inside the article content area, above the footer
- **Task 5 (Buttondown email subscriptions)**: Account created (`ayo.obembe`); subscription form embedded in site footer (center) — email field + Subscribe button, styled with darker input border and accent-colored button for visibility; caption reads "New posts by email — no spam, unsubscribe anytime."

### Decisions made

- **OG image**: Stochastic GBM paths on dark background (`#0f1117`) chosen over plain text card — more visually distinctive for social sharing; three-layer path rendering (background, mid, hero) for depth; no text overlay (platform displays title/description from meta tags automatically)
- **Privacy notice**: Added as footer text now, even though Plausible is not yet active — notice is accurate once Plausible is configured
- **Giscus category**: `Announcements` chosen over `General` — only the maintainer can open new discussion threads, which maps naturally to "one thread per post" and prevents off-topic spam threads
- **Buttondown plan**: Staying on the **Free plan** for now rather than upgrading to Basic (~$9/month) for RSS-to-email. New posts will be sent to subscribers manually until subscriber count justifies the upgrade. Tracked in new `docs/07-options-blog-future-upgrades.md`; Technical Spec Section 8 updated to reflect the Free-tier limitation

### Outstanding items (Phase 4)

- None — remaining domain-dependent tasks (Plausible Analytics, visitorbadge.io) moved to the new Phase 5 (see below)

### Plan restructuring note

- **Development Plan restructured (3 July 2026)**: "Publish to GitHub Pages" pulled out of the old Phase 6 (Launch) and promoted to its own **Phase 5 — Deploy to GitHub Pages**, sequenced before First Content. Reasoning: (1) gives a visible progress milestone before content-writing begins, (2) confirms the live site URL early, which unblocks Plausible Analytics and visitorbadge.io — both of which require a live domain and were previously stuck waiting until the very end of the project. These two tasks moved from Phase 4 into the new Phase 5. Old Phase 5 (First Content) renumbered to Phase 6; old Phase 6 (Launch) renumbered to Phase 7 and now only covers pre-launch checklist, re-publishing with real content, Quantocracy submission, sharing, and monitoring. Flagged: the site will go live in Phase 5 with placeholder/toy posts still in place — acceptable since the repo isn't being promoted yet.

---

## Phase 5 — Deploy to GitHub Pages

**Status:** In progress  
**Last updated:** 3 July 2026

### What was done

- **Task 1 (Publish to GitHub Pages)**: `gh-pages` branch did not exist on the remote, causing `quarto publish gh-pages` to fail with a misleading "initialize the remote repository" error even after the first attempt. Fixed by manually creating an empty orphan `gh-pages` branch and pushing it, then re-running the publish command, which succeeded
- Site confirmed live at `https://danielobembe.github.io/stochastic-waltz`
- **Sidebar hover bug found and fixed post-deploy**: empty sidebar sections (no subpages, e.g. "Volatility Models") render as a plain `<span class="sidebar-item-text">` rather than an `<a>` tag, so the existing `.sidebar-item a:hover` CSS rule never applied to them — they didn't turn blue on hover like sections with subpages. Fixed by broadening the selector to `.sidebar-item-text:hover`, which covers both `<a>` and `<span>` elements. Re-published to `gh-pages` after the fix

### Decisions made

- **First-publish fix**: Manually creating an orphan `gh-pages` branch is a one-time workaround for this Quarto version's first-publish behavior when the branch doesn't already exist remotely — not needed for subsequent publishes

### Outstanding items (Phase 5)

- **Task 2 — Plausible Analytics**: Not yet started — requires plausible.io account creation
- **Task 3 — visitorbadge.io**: Not yet started — requires visitorbadge.io registration

---

## Phase 6 — First Content

**Status:** Not started

---

## Phase 7 — Launch

**Status:** Not started

---

*End of Status Tracking*
