# Stochastic Waltz

A minimalist, academic-style blog covering options pricing, volatility modeling, numerical methods, and quantitative finance. Rigorous enough for practitioners, openly accessible to all.

## Stack

| Layer | Choice |
|---|---|
| Publishing framework | Quarto |
| Language | Python |
| Environment manager | conda |
| Hosting | GitHub Pages |

## Running locally

1. Activate the conda environment:
   ```bash
   conda activate stochwaltz
   ```

2. Start the preview server:
   ```bash
   quarto preview
   ```

The site will open at `http://localhost:4848` and live-reload on file changes.

## Publishing

```bash
quarto publish gh-pages
```
