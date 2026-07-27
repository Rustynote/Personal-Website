# wparcanum.com — Hugo site

Personal site for Jaroslav Suhanek, built with [Hugo](https://gohugo.io) and deployed to GitHub Pages via GitHub Actions.

## Structure

```
hugo.toml               site config, params (name, tagline, email, social links)
content/_index.md        homepage front matter (about paragraph)
data/experience.yaml      experience timeline entries
data/projects.yaml        project cards
data/stack.yaml           stack tags, split into "engineering" and "leadership" groups
layouts/_default/baseof.html   base HTML shell (head, fonts, fingerprinted CSS)
layouts/index.html             homepage template (renders all sections)
assets/css/style.css      site styles (processed via Hugo Pipes, fingerprinted for cache-busting)
static/CNAME               custom domain for GitHub Pages (wparcanum.com)
.github/workflows/hugo.yml  CI: build with Hugo, deploy to Pages
```

**Note on the stylesheet**: `style.css` lives in `assets/`, not `static/`. `baseof.html` runs it through `resources.Get` + `resources.Fingerprint`, which appends a content hash to the filename (e.g. `style.a1b2c3.css`). This means every edit to the CSS produces a new URL, so browsers can never serve a stale cached copy — if you ever see old styling stick around after a CSS change, it's a sign this pipeline isn't wired up, not a browser problem to work around with hard refreshes.

## Local development

Install Hugo (extended version) — see https://gohugo.io/installation/

```bash
hugo server -D
```

Then open http://localhost:1313.

## Editing content

- **About text**: edit the `about` field in `content/_index.md`.
- **Experience**: add/edit entries in `data/experience.yaml`.
- **Projects**: add/edit entries in `data/projects.yaml`.
- **Stack tags**: add/edit entries in `data/stack.yaml` (set `on: true` to highlight a tag).
- **Name / tagline / email / social links**: edit `[params]` in `hugo.toml`.

## Deployment

Deployment is automatic via `.github/workflows/hugo.yml`:

1. Push to `master`.
2. GitHub Actions installs Hugo, runs `hugo --minify`, and publishes `public/` to GitHub Pages.

