# Development Plan
## An Options & Quantitative Finance Blog

**Document type:** Development Plan  
**Status:** Draft v1.0  
**Prepared:** June 2026  
**Companion documents:** Design Brief v1.0, Technical Specification v1.0  
**Environment:** macOS, Python, Git, VS Code, GitHub account

---

## Overview

This document describes the phased plan to build and launch the blog. Each phase has a clear goal, a set of tasks, and a definition of done. The phases are designed to be executed sequentially — each one produces a stable, working state before the next begins.

The plan is written to be handed directly to Claude Code. Where decisions have already been made in the Design Brief or Technical Specification, this plan references those documents rather than repeating them.

---

## Phase 1 — Environment Setup

**Goal:** A skeleton Quarto project runs locally and renders in a browser. The GitHub repository is created and connected.

### Tasks

1. **Install Quarto**
   - Download and install the latest Quarto CLI from [quarto.org](https://quarto.org)
   - Verify installation: `quarto --version`

2. **Create the GitHub repository**
   - Create a new public repository on GitHub (e.g. `quant-blog`)
   - Clone it locally: `git clone https://github.com/<username>/quant-blog.git`
   - `cd quant-blog`

3. **Initialize the Quarto project**
   - Create the initial project structure (see File & Folder Structure document)
   - Create a minimal `_quarto.yml` with site title, theme base (`cosmo`), and navigation
   - Create a placeholder `index.qmd` homepage

4. **Set up the Python environment**
   - Environment manager is **conda** — do not use `venv`
   - Ask the user for their preferred environment name before creating it
   - Create the environment: `conda create -n <name> python=3.11`
   - Activate: `conda activate <name>`
   - Install core dependencies: `pip install jupyter matplotlib plotly numpy pandas scipy`
   - Create `requirements.txt`: `pip freeze > requirements.txt`
   - Add the conda environment to `.gitignore`

5. **Verify local rendering**
   - Run `quarto preview` and confirm the site renders in the browser
   - Confirm light/dark mode toggle works

6. **Initial commit**
   - Commit the skeleton project to GitHub: `git add . && git commit -m "Initial Quarto project" && git push`

### Definition of Done
- `quarto preview` renders a working site locally with no errors
- The repository exists on GitHub with the initial commit pushed
- Python environment is configured and `requirements.txt` is committed

---

## Phase 2 — Design Implementation

**Goal:** The site visually matches the Design Brief. Colors, typography, spacing, and key UI elements are correct before any real content is added.

### Tasks

1. **Create the custom SCSS file**
   - Create `styles/styles.scss`
   - Implement the full color palette for light mode (see Design Brief Section 6)
   - Implement dark mode overrides
   - Reference `styles.scss` in `_quarto.yml`

2. **Typography**
   - Apply the system font stack to body, headings, code, and UI elements (see Design Brief Section 5)
   - Set font sizes, weights, and line heights per the type scale

3. **Layout & spacing**
   - Set main content max-width to ~720px
   - Apply 8px base spacing unit consistently
   - Configure left sidebar width (~240px) and right sidebar width (~200px)
   - Ensure generous whitespace between sections

4. **Navigation bar**
   - Configure top nav: blog name (left), `Posts` / `Topics` / `About` links (right), light/dark toggle (far right)
   - Style: thin, no background fill, faint bottom border

5. **Left sidebar**
   - Style active page highlight: 3px accent color left border
   - Section headers: uppercase, small, tracked
   - Collapsible at section level

6. **Post card styles**
   - Implement the post card layout per Design Brief Section 9:
     - Date (muted, small, left)
     - Title (prominent, links to post)
     - Category pill tags
     - Thumbnail (right-aligned, ~160×100px)
     - Excerpt (2–3 sentences, muted)
   - Light horizontal divider between cards
   - Flat, no shadow, no border radius

7. **Code block styles**
   - Apply code background color (`#f3f4f2`)
   - Language label in top-right corner
   - Copy-to-clipboard button on hover
   - Syntax highlighting: GitHub Light theme

8. **Equation styles**
   - Verify KaTeX renders correctly inline and as display equations
   - Apply generous vertical padding around display equations

9. **Visual QA**
   - Review all elements in both light and dark mode
   - Review at three breakpoints: desktop (>1200px), tablet (768–1200px), mobile (<768px)

### Definition of Done
- The site visually matches the Design Brief at all three breakpoints
- Light and dark modes both render correctly
- A design review pass has been completed with no outstanding issues

---

## Phase 3 — Structure & Navigation

**Goal:** The full information architecture is in place. All navigational elements work correctly with placeholder content.

### Tasks

1. **Left sidebar — textbook hierarchy**
   - Define the top-level topic sections in `_quarto.yml` (e.g. *Foundations*, *Volatility Models*, *Pricing & Valuation*, *Greeks & Hedging*, *Numerical Methods*, *Algorithmic Trading*)
   - Create placeholder `.qmd` files for each section
   - Verify the sidebar renders the full hierarchy and collapses correctly

2. **Homepage — chronological feed**
   - Configure the homepage as a Quarto listing page (`type: listing`)
   - Create 3–4 placeholder posts with realistic front matter (title, date, categories, description, thumbnail)
   - Verify posts appear in reverse-chronological order
   - Verify the post card layout matches the design

3. **Right sidebar — categories panel**
   - Configure categories in placeholder post front matter
   - Verify the categories panel renders on the homepage with correct post counts
   - Verify clicking a category filters the feed

4. **Individual article layout**
   - Configure the per-article right-side table of contents (sticky on scroll)
   - Verify the three-column layout renders correctly on an article page
   - Add placeholder article metadata: publication date, estimated read time, category tags
   - Add collapsible revision history section stub at the bottom of article template

5. **About page**
   - Create `about.qmd` as a standalone page
   - Add placeholder content: photo placeholder, bio paragraphs, contact links
   - Link from top navigation bar
   - Verify it is not part of the left sidebar hierarchy

6. **404 page**
   - Create a minimal custom `404.qmd` page consistent with the site design

### Definition of Done
- All navigation elements (top bar, left sidebar, right TOC, categories panel) work correctly
- Clicking through the full site produces no broken links or missing pages
- The three-column article layout renders correctly on desktop
- Responsive behavior is correct at all three breakpoints

---

## Phase 4 — Third-Party Integrations

**Goal:** All services from the Technical Specification are wired up and verified.

### Tasks

1. **Plausible Analytics**
   - Create account at plausible.io and add the site domain
   - Embed the Plausible script tag in `_quarto.yml` under `include-in-header`
   - Verify pageview events appear in the Plausible dashboard after a test visit

2. **visitorbadge.io**
   - Register the homepage URL at visitorbadge.io
   - Embed the generated badge on the homepage
   - Customize badge colors to match the site palette (muted, no red/pink)

3. **Giscus comments**
   - Enable GitHub Discussions on the repository
   - Install the Giscus GitHub App at giscus.app
   - Generate the embed script and add it to the article template
   - Verify comments render in both light and dark mode
   - Verify the comment section appears below the revision history and above the footer on article pages only

4. **RSS Feed**
   - Configure the feed in `_quarto.yml` (20 items, full type)
   - Verify the feed renders correctly at `/index.xml`
   - Add RSS feed link to the site footer

5. **Buttondown email subscriptions**
   - Create account at buttondown.com
   - Configure RSS-to-email so new posts trigger automatic notifications
   - Embed the minimal subscription form (email field only) in the site footer
   - Verify the footer copy reads: *"New posts by email — no spam, unsubscribe anytime."*
   - Verify no subscription prompt appears anywhere except the footer and About page

6. **Open Graph / SEO**
   - Configure global Open Graph tags in `_quarto.yml` (title, description, default image)
   - Create a default OG image (`/assets/og-default.png`) in the site's color palette
   - Verify a test post's Open Graph tags render correctly using the [Open Graph debugger](https://developers.facebook.com/tools/debug/)

7. **Privacy notice**
   - Add a one-paragraph privacy notice to the site footer
   - Content: note that Plausible analytics are in use, no personal data is collected passively

### Definition of Done
- All six integrations are live and verified
- Plausible is recording visits
- A test comment can be posted and displayed via Giscus
- The RSS feed validates correctly
- A test email subscription and delivery works end-to-end

---

## Phase 5 — First Content

**Goal:** Two real posts are written, rendered correctly, and look exactly as intended. All content elements — equations, code, plots, and interactive figures — are verified in context.

### Tasks

1. **Define the first two posts**
   - Choose two posts that together exercise all content elements:
     - Post 1: equation-heavy (e.g. Black-Scholes derivation) — tests KaTeX rendering
     - Post 2: code and visualization-heavy (e.g. volatility surface plot) — tests Plotly, code blocks, and interactive figures
   - Write the posts in `.qmd` format with full front matter (title, date, categories, description, thumbnail)

2. **Establish the Python plot theme**
   - Create a shared Matplotlib/Plotly stylesheet in `/assets/plot_theme.py`
   - Apply the Okabe-Ito color palette (see Design Brief Section 8)
   - White/transparent plot backgrounds
   - Thin light gray axes, minimal tick marks
   - Use this theme in both first posts and all subsequent posts

3. **Verify content rendering**
   - Inline and display equations render correctly via KaTeX
   - Code blocks display with correct syntax highlighting, language label, and copy button
   - Show/hide toggle works for long code cells
   - Plotly interactive figures embed natively (no iframe border)
   - Thumbnails display correctly on the homepage post cards
   - Publication date and read time display correctly in article header
   - Category tags display correctly below the title
   - Revision history section is present, collapsed by default

4. **Cross-browser and responsive check**
   - Verify both posts render correctly in Safari and Chrome
   - Verify mobile layout at 375px width

### Definition of Done
- Two complete, real posts are published locally and render with no visual or functional issues
- The shared plot theme is established and committed
- All content elements (equations, code, plots) are verified

---

## Phase 6 — Launch

**Goal:** The site is live on GitHub Pages and has been shared with the first communities.

### Tasks

1. **Pre-launch checklist**
   - [ ] All placeholder content removed or replaced
   - [ ] About page complete with real bio and photo
   - [ ] No broken links (run `quarto check`)
   - [ ] All images have `alt` text
   - [ ] Open Graph tags verified for homepage and both posts
   - [ ] RSS feed validates at `/index.xml`
   - [ ] Plausible tracking confirmed live
   - [ ] Giscus comments confirmed working
   - [ ] Buttondown subscription confirmed working
   - [ ] Site renders correctly at all three breakpoints
   - [ ] Light and dark modes both confirmed

2. **Publish to GitHub Pages**
   ```bash
   quarto publish gh-pages
   ```
   - Verify the live site at `https://<username>.github.io/<repository-name>/`
   - Confirm all pages, assets, and integrations work on the live URL (not just locally)

3. **Submit to Quantocracy**
   - Submit the blog URL at [quantocracy.com/submit](https://quantocracy.com/submit)
   - Quantocracy is the primary aggregator for quant finance content; inclusion here is the single highest-value distribution action at launch

4. **Share first posts**
   - Post on Reddit: r/quant, r/algotrading (follow subreddit rules on self-promotion)
   - Post on Twitter/X with relevant hashtags (#quant #options #volatility)
   - Share on LinkedIn if relevant to your network

5. **Post-launch monitoring**
   - Check Plausible dashboard in the first 48 hours for traffic sources
   - Monitor Giscus / GitHub Discussions for first comments
   - Note any rendering issues reported or observed on the live site

### Definition of Done
- The site is publicly accessible at the GitHub Pages URL
- Both posts are live and rendering correctly
- The site has been submitted to Quantocracy
- No critical issues observed in the first 48 hours

---

## Appendix: Ongoing Workflow (Post-Launch)

For each new post after launch, the standard workflow is:

1. Create a new `.qmd` file in the appropriate topic folder
2. Write front matter: `title`, `date`, `categories`, `description`, `image` (thumbnail)
3. Write content in Quarto markdown — equations in LaTeX, code in Python chunks, plots via Plotly
4. Run `quarto preview` locally to verify rendering
5. Commit to GitHub: `git add . && git commit -m "Add post: <title>" && git push`
6. Publish: `quarto publish gh-pages`
7. Share on relevant communities

For post updates:
- Edit the `.qmd` file
- Update the `date` field in front matter to the current date
- Add an entry to the revision history section at the bottom of the post
- Follow steps 4–6 above

---

*End of Development Plan v1.0*
