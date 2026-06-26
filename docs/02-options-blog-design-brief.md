# Design Brief
## An Options & Quantitative Finance Blog

**Document type:** Design Brief  
**Status:** Updated v1.1 — revised after Phase 2 implementation  
**Prepared:** June 2026

---

## 1. Concept & Philosophy

This blog occupies a rare position: rigorous enough for practitioners and researchers, yet public and accessible. It is not a newsletter, not a trading signals service, not a course platform. It is closer to a living textbook — one that happens to also have a publication date on every page.

The design should reflect that dual identity. It should feel like a well-typeset academic paper that has been made native to the web: clean, precise, confident, and entirely without decoration that does not earn its place. Every design decision defers to the content — equations, code, and visualizations are the stars; the surrounding chrome exists only to frame them clearly.

The governing principle is **restraint with purpose**. White space is not emptiness — it is the room that complex ideas need to breathe.

**In one sentence:** A minimalist, white, academic design that treats mathematical and technical content as first-class material, organized simultaneously as a textbook and a blog.

---

## 2. Inspiration & Reference Sites

| Site | What to borrow |
|---|---|
| [dienhoa.github.io/dhblog](https://dienhoa.github.io/dhblog/) | **Primary visual reference.** Overall aesthetic, clean white layout, minimal navbar, chronological post feed, post card layout (date + title + category pills + thumbnail + excerpt), right-side categories panel. Built on Quarto `litera` theme. |
| [quantgirluk.github.io](https://quantgirluk.github.io/Understanding-Quantitative-Finance/intro.html) | Left sidebar structure — section headers with individual posts nested beneath them, textbook-style hierarchy |
| [distill.pub](https://distill.pub) | Interactive figures, article typography, the feeling that a page is a peer-reviewed artifact |

> **Implementation note:** quantgirluk is built on Jupyter Book (PyData Sphinx Theme), not Quarto — direct replication is not possible. dhblog is a native Quarto blog and was adopted as the primary reference during Phase 2.

---

## 3. Information Architecture

The blog has three simultaneous organizational layers that coexist without conflict.

### 3.1 Left Sidebar — Textbook Navigation
A persistent, hierarchical table of contents organized by topic. This is the "book" view of the site. Topics might include sections such as *Foundations*, *Volatility Models*, *Pricing & Valuation*, *Greeks & Hedging*, *Algorithmic Trading*, *Numerical Methods*, etc.

- Each post lives in **exactly one** place in this hierarchy
- The sidebar is always visible on desktop, collapsible on mobile
- Active section and active page are highlighted
- Mirrors the structure of a graduate-level textbook

### 3.2 Center Panel — Chronological Feed (Homepage)
The landing page of the site. Rather than a static welcome message, the center panel displays a **reverse-chronological list of posts** — the traditional blog view. Each post card shows:
- Publication date (left-aligned, muted)
- Post title (prominent)
- Category tags (small pill labels)
- A thumbnail or representative figure (right-aligned)
- A 2–3 sentence excerpt

This gives returning readers an immediate sense of what is new, while the left sidebar serves new readers who want to explore by topic.

### 3.3 Right Sidebar — Categories Panel (Homepage only)
Visible on the homepage alongside the chronological feed. A flat list of all content categories with post counts — e.g. `stochastic-vol (8)`, `greeks (5)`, `monte-carlo (4)`. 

- A post can belong to **multiple categories** even though it appears in only one place in the left sidebar's topic hierarchy
- Categories are clickable and filter the feed
- This distinction is intentional: the left nav answers *"where does this fit intellectually?"* — categories answer *"what topics does this touch?"*

### 3.4 Individual Article Layout
Each article page follows a consistent three-column structure:

- **Left:** Persistent site-wide topic sidebar (same as everywhere)
- **Center:** Article content — full width for reading comfort, generous line length (~68 characters)
- **Right:** Per-article table of contents, auto-generated from headings, sticky on scroll

Article pages also include:
- Category tag(s) displayed below the title
- Publication date — displayed in the article header in small muted metadata text, near the title:
  - If the article has never been updated: "Published: June 3, 2026"
  - If the article has been updated: "Published: June 3, 2026 · Last updated: January 12, 2027"
- Estimated read time
- Toggle to show/hide code cells (for Quarto notebook-style posts)
- Clean equation rendering via KaTeX
- Interactive figures embedded inline (Plotly/Observable)
- **Revision history** — a collapsible section at the bottom of each article, above the footer. Collapsed by default. Each entry is a date and a one-line description of what changed, listed in reverse-chronological order, e.g.:
  - *January 12, 2027 — Updated calibration code to use QuantLib 2.1; corrected equation 4.3*
  - *June 3, 2026 — First published*

### 3.5 About Page
A standalone page, linked from the top navigation bar. Not embedded in the content hierarchy. Contains author bio, background, and contact information. Modeled after dhblog's `/about` — personal but professional, with a photo and a brief statement of purpose for the blog.

---

## 4. Layout & Spacing

### Grid
- Three-column layout on desktop: left sidebar (~240px) | main content (flexible, max ~720px) | right sidebar (~200px)
- On tablet: left sidebar collapses to a hamburger/drawer; right sidebar hides
- On mobile: single column; both sidebars accessible via drawer/toggle

### Spacing Philosophy
Generous. Sections are separated by whitespace alone — no decorative rules or dividers. The page should never feel crowded. Margins and padding are consistent and based on a simple 8px base unit.

### Content Width
The main reading column is capped at approximately 720px. This enforces a comfortable ~65–68 character measure for body text — the range proven optimal for sustained reading of technical material.

---

## 5. Typography

Typography is the primary design element on a white, minimalist site. These choices must be made carefully and applied consistently.

### Type Roles & Families

The typography directly mirrors quantgirluk's approach, which uses the **system font stack** throughout — no external fonts are loaded. This means the site renders in whatever the OS's default UI font is: San Francisco on macOS/iOS, Segoe UI on Windows, Roboto on Android/Chrome. The result is fast-loading, crisp, and deeply familiar to readers on each platform.

| Role | Typeface | Notes |
|---|---|---|
| Body text | **System sans-serif stack** | `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif` — the sphinx-book-theme / PyData Sphinx Theme default |
| Headings | **Same system stack, heavier weight** | Weight 500–600; no separate heading typeface, consistent with quantgirluk |
| Code | **System monospace stack** | `SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace` — can optionally be overridden with JetBrains Mono if a more distinctive code style is desired later |
| Equations | **KaTeX** | LaTeX-quality math rendering; faster than MathJax; natively supported in Jupyter Book / Quarto |
| UI labels / navigation | **Same system stack** | Consistent with the rest of the site |

**Note on the system font approach:** This is a deliberate and principled choice, not a default by neglect. System fonts are instantly legible, require zero loading time, and give the site a clean, software-tool aesthetic that suits a technical audience. The tradeoff is that the typography looks subtly different across operating systems. If a more controlled typographic personality is desired in future, switching to a single loaded sans-serif (e.g. Inter or IBM Plex Sans) would be a minimal change that preserves the same overall feel.

### Type Scale

| Element | Size | Weight | Notes |
|---|---|---|---|
| Post title / H1 | 2rem (32px) | 600 | Only one per page |
| Section heading / H2 | 1.5rem (24px) | 500 | |
| Subsection / H3 | 1.25rem (20px) | 500 | |
| Body text | 1rem (16px) | 400 | quantgirluk's default; clean at this size in system sans-serif |
| Code (inline) | 0.9rem | 400 | System monospace |
| Code (block) | 0.875rem (14px) | 400 | System monospace |
| Tags / metadata | 0.75rem (12px) | 500 | Uppercase, tracked |
| Caption | 0.875rem (14px) | 400 | Italic |

### Line Height & Measure
- Body text: `line-height: 1.65` (sphinx-book-theme default; comfortable for technical prose in sans-serif)
- Headings: `line-height: 1.25`
- Code blocks: `line-height: 1.6`
- Equations: generous vertical margin above and below; displayed equations centered with `1.5rem` vertical padding

---

## 6. Color Palette

The palette is near-monochrome with a single restrained accent. Color is used to convey information, not decoration.

### Light Mode (Default)

| Name | Hex | Usage |
|---|---|---|
| Background | `#fafaf8` | Page background — warm off-white, not pure white; reduces harshness |
| Surface | `#ffffff` | Cards, code block backgrounds, sidebar panels |
| Body text | `#1a1a1a` | Primary text — dark charcoal, not pure black |
| Secondary text | `#6b7280` | Metadata, captions, dates, tag labels |
| Border / divider | `#e5e7eb` | Subtle separators; used sparingly |
| Accent | `#2563a8` | Links, active nav items, interactive elements, tag borders; a calm ink blue |
| Accent hover | `#1d4e89` | Slightly darker on hover |
| Code background | `#f3f4f2` | Barely-there warm gray for inline and block code |
| Tag background | `#eef2f7` | Pill tags on post cards and article headers |

### Dark Mode

Dark mode is supported (Quarto handles the toggle). The dark mode palette should feel like the light mode inverted in spirit — still academic, still restrained.

| Name | Hex | Usage |
|---|---|---|
| Background | `#0f1117` | Deep near-black |
| Surface | `#1a1d27` | Cards, sidebars |
| Body text | `#e8e8e6` | Warm off-white text |
| Secondary text | `#9ca3af` | Muted text |
| Accent | `#5b9bd5` | Lightened blue for readability on dark |
| Code background | `#1e2130` | Slightly lighter than page background |

### Color Rules
- **Red and green are reserved** for P&L and directional contexts in charts and content only — never used for UI decoration
- The accent color should appear sparingly: links, active states, one or two highlights per page maximum
- All plots and interactive figures use the same color system (see Section 8)

---

## 7. Navigation & Header

### Top Navigation Bar
Minimal. Contains:
- Blog name / wordmark (left) — typeset in system font, weight 600, not a logo
- Right side: `About` link, LinkedIn icon, GitHub icon, search icon, light/dark mode toggle
- No Posts/Topics navigation links in the navbar — sidebar handles all topic navigation

The top bar is thin, unobtrusive, and does not compete with content. No background fill — it sits directly on the page background color with a very faint bottom border.

> **Dark mode status:** Dark mode toggle is present but deferred — full dark mode implementation requires resolving CSS specificity conflicts between the `litera` and `darkly` Quarto themes. Parked for a future session.

### Left Sidebar
- Collapsible at section level
- Active page highlighted with accent color left border (a 3px rule)
- Section headers in system font, uppercase, small, tracked (these are structural labels, not reading content)
- Page links in system font, normal case

---

## 8. Figures, Plots & Equations

These are the most important design elements in the entire site. They must be treated with the same care as typography.

### Equations
- Rendered via KaTeX (Quarto default)
- Inline equations: seamlessly integrated in text flow
- Display equations: centered, generous vertical whitespace above and below, numbered on the right where referenced
- Font size should match body text for inline; slightly larger for display
- Equations should never be images — always rendered math

### Plots & Visualizations
- **Backgrounds:** White or transparent — plots should feel like they are part of the page, not framed boxes dropped in
- **Axes:** Thin, light gray lines; minimal tick marks; no chartjunk
- **Color palette for data series:** Use the Okabe-Ito palette as default — colorblind-safe, works beautifully on white backgrounds:
  - `#E69F00` (orange), `#56B4E9` (sky blue), `#009E73` (green), `#F0E442` (yellow), `#0072B2` (blue), `#D55E00` (vermilion), `#CC79A7` (pink)
- **Labels:** Direct labels on chart where possible, rather than a separate legend
- **Interactive figures:** Embedded as Plotly HTML widgets or Observable; they should be native to the page, not iframed in a box with a border
- A single consistent plot theme (Matplotlib stylesheet or ggplot2 theme) should be defined early and reused across all posts

### Code Blocks
- Language label displayed in top-right corner of the block (e.g., `python`, `r`)
- Copy-to-clipboard button on hover
- Show/hide toggle for long code cells (especially in Quarto notebook posts)
- Syntax highlighting: a light, low-contrast theme — something like GitHub Light or a custom theme with the blog's code background color
- No heavy borders or drop shadows — just the subtle background color difference

---

## 9. Post Cards (Homepage Feed)

Each entry in the chronological feed:

```
┌─────────────────────────────────────────────────────────┐
│ Jun 3, 2026                                             │
│                                                         │
│ The Heston Model: Calibration from First Principles  ████│
│                                                      ████│
│ [stochastic-vol]  [calibration]  [python]            ████│
│                                                         │
│ We derive the characteristic function of the Heston     │
│ model and implement a fast calibration routine using     │
│ Fourier inversion...                                     │
└─────────────────────────────────────────────────────────┘
```

- Date: muted, small, system font
- Title: prominent, system font weight 500–600, links to post
- Tags: small pill labels, muted accent color background
- Thumbnail: right-aligned, fixed size (~160×100px), shows a representative figure from the post
- Excerpt: 2–3 sentences, body text size, muted color
- Horizontal divider between cards (very light, `#e5e7eb`)
- No card shadow or border radius — flat and clean

---

## 10. About Page

A standalone page, not part of the textbook hierarchy. Modeled on dhblog's About page layout.

- Photo: circular crop, medium size, centered above the bio
- Title ("About") centered below the photo
- Short bio: 2–3 paragraphs centered below the title — background, motivation for the blog, areas of focus
- No testimonials, no "hire me" language, no social proof widgets
- Links to LinkedIn and GitHub below the bio — rendered as small pill buttons (matching dhblog)
- The tone should match the blog: precise, unpretentious, technically confident

---

## 11. Responsive Behavior

| Breakpoint | Behavior |
|---|---|
| Desktop (>1200px) | Full three-column layout |
| Tablet (768–1200px) | Left sidebar collapses to drawer; right TOC sidebar hides; main content expands |
| Mobile (<768px) | Single column; both sidebars accessible via header toggle; post card thumbnails stack below text |

---

## 12. Technical Stack & Implementation Notes

This brief is designed to be implemented in **Quarto**, the scientific publishing framework that natively supports:
- Jupyter/R Markdown source files
- KaTeX equation rendering
- Code execution and output display
- Light/dark mode toggle
- Left sidebar navigation from `_quarto.yml`
- Per-page table of contents

**Quarto theme base:** `litera` (Bootswatch) — adopted during Phase 2 as the closest match to dhblog's clean white aesthetic. Overridden with `styles/styles.scss` for colors, typography, sidebar, and post card styles.

**Fonts:** System font stack — no external fonts loaded. `litera` provides this by default.

**Interactive figures:** Use `plotly` (Python) or `plotly`/`htmlwidgets` (R) for interactive charts; they embed natively as self-contained HTML in Quarto output.

**Blog listing page:** Use Quarto's native `listing` page type for the homepage chronological feed. Configure it with `type: default` and a custom template to match the post card design specified in Section 9.

**Categories:** Use Quarto's `categories` field in post YAML front matter. The right-sidebar categories panel is populated automatically from this metadata.

---

## 13. What This Design Is Not

To keep the vision clear, it is worth stating what to actively avoid:

- **Not dark-themed** — the primary experience is white/light
- **Not dashboard-like** — no data widgets, no live feeds, no heavy UI chrome
- **Not newsletter-like** — no subscribe popups, no engagement bait, no "you might also like" widgets
- **Not a personal brand site** — the author is present but secondary to the content
- **Not overdesigned** — if an element's purpose cannot be stated in one sentence, it should be removed

---

*End of Design Brief v1.0*
