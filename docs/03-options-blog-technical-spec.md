# Technical Specification
## An Options & Quantitative Finance Blog

**Document type:** Technical Specification  
**Status:** Draft v1.0  
**Prepared:** June 2026  
**Companion document:** Design Brief v1.0

---

## 1. Overview

This document specifies the technical infrastructure, third-party integrations, and site capabilities for the options and quantitative finance blog. It is a companion to the Design Brief, which covers visual design and information architecture. Together, the two documents provide a complete picture of what to build.

The guiding principle here mirrors the design philosophy: **keep it simple, keep it clean, and add complexity only when it earns its place.** Every tool and integration listed below has been chosen for its fit with a minimalist, content-first technical blog.

---

## 2. Core Stack

### Publishing Framework
**Quarto** is the authoring and publishing framework. It provides:
- Jupyter/R Markdown source file support
- Native KaTeX equation rendering
- Code execution and output display
- Light/dark mode toggle
- Left sidebar navigation via `_quarto.yml`
- Per-page table of contents
- Automatic RSS feed generation
- Native blog listing page (`type: listing`) for the chronological post feed
- `categories` field in post YAML front matter for the categories panel

### Theme Base
Start from the `cosmo` or `flatly` Bootswatch theme, overriding with a custom `styles.scss` that implements the palette, typography, and spacing defined in the Design Brief. Do not use a dark theme base — dark mode is handled via Quarto's toggle, not baked into the base theme.

### Source Control
All source files (`.qmd`, `_quarto.yml`, `styles.scss`, assets) live in a **GitHub repository**. This serves double duty: version control for content and the deployment source for GitHub Pages.

---

## 3. Hosting & Deployment

### Platform
**GitHub Pages** — free static site hosting, directly integrated with Quarto's publish workflow.

Publishing is a single command:
```bash
quarto publish gh-pages
```

This renders the site and pushes the output to the `gh-pages` branch of the repository, which GitHub Pages serves automatically.

### URL
The site launches on the default GitHub Pages URL:
```
https://<username>.github.io/<repository-name>/
```

### Custom Domain (Future)
When ready, a custom domain (e.g. `yourblog.com`) can be added by:
1. Registering a domain with any registrar (~$12/year for a `.com`)
2. Adding a `CNAME` file to the repository root
3. Configuring DNS records with the registrar to point to GitHub Pages

This migration requires no changes to content or site structure — it is a configuration-only change. GitHub Pages also automatically provisions HTTPS via Let's Encrypt for custom domains.

### Build Process
Quarto renders the site locally and pushes pre-built HTML to GitHub Pages. There is no server-side build step. If a CI/CD pipeline is desired later (e.g. auto-build on push via GitHub Actions), this can be added without changing the underlying setup.

---

## 4. SEO

### What Quarto Handles Automatically
- Page `<title>` tags from post titles
- Meta description from post `description` field in YAML front matter
- Canonical URLs
- XML sitemap at `/sitemap.xml`
- RSS feed at `/index.xml`

### Open Graph Configuration
Open Graph tags control how links appear when shared on LinkedIn, Twitter/X, and other platforms — post title, description, and thumbnail image. Configure globally in `_quarto.yml`:

```yaml
website:
  open-graph:
    title: "Blog Name"
    description: "A rigorous, open-access blog on options pricing, volatility, and algorithmic trading."
    image: "/assets/og-default.png"
```

Per-post overrides can be set in individual post YAML front matter using the same `open-graph` key.

### What Not to Over-Engineer
Technical SEO (structured data markup, Core Web Vitals optimization, backlink schemes) is not worth significant investment for this blog. The primary discovery channels for a niche technical audience are community sharing — Quantocracy, Reddit (r/quant, r/algotrading), Twitter/X, and word of mouth — not organic search. Content quality is the only SEO lever that matters here.

---

## 5. Analytics

### Private Analytics — Plausible
**Plausible Analytics** is used for private, detailed site analytics.

Key properties:
- Privacy-respecting: no cookies, no personal data collected
- No cookie consent banner required (GDPR/CCPA compliant by design)
- Lightweight: ~1KB script, negligible performance impact
- Not blocked by most ad blockers (unlike Google Analytics)
- Provides: page views, unique visitors, referrer sources, geographic distribution, top pages, devices
- Cost: ~$9/month (or ~$90/year) after the free trial

Setup: create an account at [plausible.io](https://plausible.io), add your domain, and embed the provided script tag in Quarto's HTML head via `_quarto.yml`:

```yaml
format:
  html:
    include-in-header:
      - text: |
          <script defer data-domain="yourdomain.com" src="https://plausible.io/js/script.js"></script>
```

### Public Visitor Counter — visitorbadge.io
A small public visitor count badge is embedded on the homepage (and optionally the About page), matching the approach used by quantgirluk.

Setup: register the page URL at [visitorbadge.io](https://visitorbadge.io) and embed the generated badge image. The badge displays a running total of page visits and requires no ongoing maintenance.

Badge styling should be customized to use muted colors consistent with the site palette — avoid the default red/pink color in the generated badge.

---

## 6. Comments

### Platform
**Giscus** — an open-source, ad-free comment system backed by GitHub Discussions.

Key properties:
- Free, no ads, no tracking
- Comments are stored as GitHub Discussions in the site's repository (or a dedicated repo)
- Readers authenticate with their GitHub account to comment — a natural fit for a technical audience
- Supports light/dark mode, matching the site toggle
- Renders Markdown in comments, including code blocks and equations
- Maintained and actively developed

### Setup
1. Install the Giscus GitHub App on the repository at [giscus.app](https://giscus.app)
2. Enable GitHub Discussions on the repository
3. Generate the embed script at giscus.app and add it to the Quarto article template

### Placement
Comment section appears at the bottom of each article page, below the article content and revision history, above the footer. Not shown on the homepage or About page.

---

## 7. RSS Feed

Quarto generates an RSS feed automatically at `/index.xml` when the blog listing page is configured. No additional setup is required beyond ensuring the feed includes full post metadata (title, date, description, categories).

Configure in `_quarto.yml`:
```yaml
website:
  feeds:
    - items: 20
      type: full
```

The feed URL should be linked in:
- The site footer (plain text link: "RSS Feed")
- The HTML `<head>` as a `<link rel="alternate">` tag (Quarto adds this automatically)

---

## 8. Email Subscriptions

### Approach
A simple, unobtrusive email subscription option — readers can opt in to receive notifications of new posts. This is not a newsletter operation; there are no regular digests, no marketing emails, no prominent CTAs. The subscription link appears in the site footer and on the About page only.

### Platform
**Buttondown** — a lightweight, developer-friendly email tool.

Key properties:
- Free tier supports up to 100 subscribers; paid tier starts at ~$9/month
- Clean, minimal interface with no engagement-bait features
- Supports RSS-to-email (automatically sends new posts to subscribers)
- No tracking pixels by default (aligns with the privacy-respecting analytics approach)
- Simple API for embedding a subscription form

### Implementation
A minimal single-field form (email address only, no name field) embedded as a small block in the footer. No popup, no modal, no sticky banner. Suggested copy: *"New posts by email — no spam, unsubscribe anytime."*

---

## 9. Performance

### Baseline
Quarto's static HTML output is fast by default. The system font stack (no external font loading) and minimal JavaScript further reduce page weight. Target: **under 500KB total page weight** for a standard article page, excluding interactive figures.

### Interactive Figures
Plotly HTML widgets are the primary performance risk — a single complex 3D surface plot can exceed 1MB. Mitigations:
- Use `include: false` on heavy outputs during development to test page weight
- Prefer 2D Plotly charts over 3D where the insight is equivalent
- For very large figures, consider linking to a standalone HTML page rather than embedding inline
- Lazy-load figures below the fold where Quarto supports it

### Images
- Post thumbnail images: compress to JPEG, target ~50–80KB per image
- All images should have explicit `width` and `height` attributes to prevent layout shift
- Use descriptive `alt` text on all figures (required for accessibility, also improves SEO)

---

## 10. Accessibility

The site targets **WCAG 2.1 AA** compliance. The design choices in the Design Brief already support this:
- High contrast between body text (`#1a1a1a`) and background (`#fafaf8`) exceeds AA requirements
- System font stack renders at native OS legibility
- No reliance on color alone to convey information (red/green reserved only for P&L content)

Additional requirements during build:
- All interactive elements (links, toggles, sidebar navigation) must be keyboard-navigable
- Focus indicators must be visible (do not suppress the browser's default `:focus` outline)
- All images and figures must have descriptive `alt` text
- Code blocks should be accessible to screen readers (Quarto handles this via semantic HTML)
- Giscus comment widget supports keyboard navigation natively

---

## 11. Privacy & Compliance

- **No cookies** are set by any first-party code (Plausible is cookieless)
- **No cookie consent banner** is required as a result
- Giscus sets cookies only when a user actively initiates the GitHub OAuth login to comment — this is user-initiated and exempt from passive tracking rules
- Buttondown subscription is opt-in only; no pre-checked boxes
- No advertising networks, no cross-site tracking scripts
- A minimal **Privacy Notice** (one short paragraph, not a full policy page) should be linked from the footer, noting that Plausible analytics are in use and that no personal data is collected passively

---

## 12. Domain Migration Checklist (When Ready)

For future reference, when migrating from `github.io` to a custom domain:

- [ ] Register domain with preferred registrar
- [ ] Add `CNAME` file to repository root containing the custom domain
- [ ] Configure DNS: add `A` records pointing to GitHub Pages IPs, or a `CNAME` record for `www`
- [ ] Enable "Enforce HTTPS" in GitHub Pages repository settings
- [ ] Update `site-url` in `_quarto.yml` to the new domain
- [ ] Update Plausible dashboard to track the new domain
- [ ] Update visitorbadge.io badge URL
- [ ] Update Giscus configuration if repository URL is referenced
- [ ] Verify Open Graph tags reflect the new URL
- [ ] Set up redirect from old `github.io` URL (GitHub Pages handles this automatically for the root)

---

## 13. Third-Party Services Summary

| Service | Purpose | Cost | URL |
|---|---|---|---|
| GitHub Pages | Hosting & deployment | Free | pages.github.com |
| Quarto | Publishing framework | Free | quarto.org |
| Plausible | Private analytics | ~$9/month | plausible.io |
| visitorbadge.io | Public visitor counter | Free | visitorbadge.io |
| Giscus | Comments | Free | giscus.app |
| Buttondown | Email subscriptions | Free / ~$9/month | buttondown.com |

---

*End of Technical Specification v1.0*
