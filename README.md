# Array Engineering Website

Static site for [arrayeng.org](https://arrayeng.org) built with MkDocs Material, deployed to GitHub Pages.

## Setup

```bash
# Create conda environment (one time)
conda create -n arrayeng_site_env python=3.12 -y
conda activate arrayeng_site_env
pip install -r requirements.txt
```

## Local Development

```bash
conda activate arrayeng_site_env
cd ~/code/arrayeng-site
mkdocs serve
```

Site is at `http://localhost:8000`. Edits to files in `docs/` and `overrides/` auto-reload.

### Project Structure

```
docs/
  index.md              # Landing page (uses custom home template)
  services.md           # Services page
  about.md              # About page
  assets/               # Logo, favicon
  stylesheets/extra.css # Brand colors, fonts
overrides/
  home.html             # Custom landing page template
mkdocs.yml              # Site config (nav, theme, plugins)
```

### Editing Content

- **Pages**: Edit markdown files in `docs/`. Navigation order is set in `mkdocs.yml` under `nav:`.
- **Landing page**: Edit `overrides/home.html` (HTML/Jinja2 template).
- **Styling**: Edit `docs/stylesheets/extra.css`. Brand colors are defined as CSS variables at the top.
- **Config**: `mkdocs.yml` controls site name, URL, theme settings, and navigation.

### Brand

- Colors: `#A54500` (burnt orange), `#FFB74B` (amber), `#454545` (dark gray)
- Headings: Dosis (Google Font)
- Body: Inter (Google Font)
- Logo: `docs/assets/logo.svg`

## Deployment

Deployment is automated via GitHub Actions. Every push to `main` builds and deploys to GitHub Pages.

### First-time setup

1. Create the GitHub repo and push:
   ```bash
   gh repo create arrayeng-site --public --source=. --push
   ```

2. Enable GitHub Pages in the repo:
   - Go to **Settings > Pages**
   - Set **Source** to **GitHub Actions**

3. Connect custom domain:
   - In **Settings > Pages > Custom domain**, enter `arrayeng.org`
   - In Cloudflare DNS, add a CNAME record:
     - Type: `CNAME`
     - Name: `@` (or `arrayeng.org`)
     - Target: `adam-morse.github.io`
   - Also add a `www` CNAME pointing to `adam-morse.github.io`
   - Wait for DNS propagation and HTTPS certificate (can take a few minutes)

### Ongoing deploys

```bash
git add -A
git commit -m "Update site content"
git push
```

Site rebuilds automatically. Check the **Actions** tab on GitHub for build status.
