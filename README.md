# Monika Avila — Academic Website (Quarto)

A clean academic personal site built with [Quarto](https://quarto.org), deployable to GitHub Pages in minutes.

## Quick start

### 1. Install Quarto
Download from https://quarto.org/docs/get-started/

### 2. Preview locally
```bash
quarto preview
```
Opens at http://localhost:4848 with live reload.

### 3. Build
```bash
quarto render
```
Output goes to `/docs` (configured in `_quarto.yml`).

## Deploy to GitHub Pages

### Option A — Render locally, push docs/
```bash
quarto render
git add docs/
git commit -m "Render site"
git push
```
Then in your repo: **Settings → Pages → Source → Deploy from branch → main → /docs**.

### Option B — GitHub Actions (auto-deploy on push)
Create `.github/workflows/publish.yml`:

```yaml
name: Publish site
on:
  push:
    branches: [main]
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: quarto-dev/quarto-actions/setup@v2
      - run: quarto render
      - uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
This renders and pushes to the `gh-pages` branch automatically.

## Customisation checklist

- [ ] Replace `MA` initials in `index.qmd` with `<img>` tag once you have a photo
- [ ] Update all `href="#"` placeholder links with real URLs
- [ ] Fill in supervisor name in the education table
- [ ] Add teaching entries in `teaching.qmd`
- [ ] Drop your CV PDF at `assets/cv.pdf`
- [ ] Set your real GitHub username in `_quarto.yml` navbar links
- [ ] Add Google Analytics ID to `_quarto.yml` if wanted:
  ```yaml
  website:
    google-analytics: "G-XXXXXXXXXX"
  ```

## File structure

```
quarto-site/
├── _quarto.yml        ← site config, navbar, theme
├── index.qmd          ← home / about page
├── research.qmd       ← full paper list
├── teaching.qmd       ← teaching
└── assets/
    └── custom.css     ← all custom styles
```
