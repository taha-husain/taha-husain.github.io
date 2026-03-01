# taha-husain.github.io

Personal portfolio site built with [Hugo](https://gohugo.io/) and deployed to GitHub Pages.

**Live site:** https://taha-husain.github.io

---

## Stack

- **Hugo** 0.157.0 (extended)
- **Theme:** Custom (fully bespoke layouts, no external theme dependency)
- **Styles:** Single CSS file with CSS custom properties for light/dark mode
- **Hosting:** GitHub Pages (served from `docs/`)
- **CI/CD:** GitHub Actions

---

## Project structure

```
.
├── config.yml              # Site configuration (baseURL, menus, params)
├── content/
│   ├── posts/
│   │   ├── tech/           # Tech blog posts
│   │   └── music/          # Music blog posts
│   ├── portfolio.md        # Portfolio page (content-free, uses layout)
│   └── resume.md           # Resume page (content-free, uses layout)
├── layouts/
│   ├── index.html          # Homepage
│   ├── _default/
│   │   ├── baseof.html     # Base shell (nav, footer, theme toggle)
│   │   ├── single.html     # Blog post
│   │   ├── list.html       # Post listing
│   │   ├── terms.html      # Tag pages
│   │   ├── resume.html     # Resume page layout
│   │   └── portfolio.html  # Portfolio page layout
│   ├── partials/
│   │   └── tech-icon.html  # Tech brand icon helper (Simple Icons + Devicons CDN)
│   └── shortcodes/
│       └── rawhtml.html    # Raw HTML passthrough (for iframes in posts)
├── static/
│   ├── css/style.css       # All site styles
│   ├── avatar.jpg
│   ├── taha-husain-resume.pdf
│   └── favicon_io/
├── docs/                   # Hugo build output (GitHub Pages source)
└── .github/workflows/
    ├── hugo.yaml           # Build + deploy to Pages (main branch only)
    └── build-check.yml     # Build verification (all other branches)
```

---

## Local development

**Prerequisites:** Hugo 0.157.0 extended. Install via Homebrew:

```bash
brew install hugo
```

Or download the extended binary directly from the [Hugo releases page](https://github.com/gohugoio/hugo/releases/tag/v0.157.0).

**Run the dev server:**

```bash
hugo server
```

The site will be available at `http://localhost:1313`. Hugo watches for file changes and live-reloads automatically.

**Build for production:**

```bash
hugo --gc --minify --baseURL "https://taha-husain.github.io/"
```

Output is written to `docs/` (set via `publishDir` in `config.yml`).

---

## Deployment

Deployment is fully automated via GitHub Actions:

- **Push to `main`** → [`hugo.yaml`](.github/workflows/hugo.yaml) builds the site and deploys to GitHub Pages.
- **Push to any other branch** → [`build-check.yml`](.github/workflows/build-check.yml) verifies the build succeeds without deploying.

GitHub Pages is configured to serve from the `docs/` directory on the `main` branch (set in repository Settings → Pages).

---

## Content

### Blog posts

Posts live in `content/posts/tech/` or `content/posts/music/`. Create a new post:

```bash
hugo new posts/tech/my-post-title.md
```

Front matter fields used:

```yaml
---
title: "Post title"
date: 2025-01-01
tags: [ruby, rails]
---
```

To reference an external post (e.g. BigBinary) without duplicating content, add `externalUrl`:

```yaml
---
title: "Post title"
date: 2025-01-01
tags: [ruby]
externalUrl: "https://www.bigbinary.com/blog/..."
---
```

The post will appear in listings with an `↗` indicator and link directly to the external URL.

### Resume PDF

Place the PDF at `static/taha-husain-resume.pdf`. It will be served at `/taha-husain-resume.pdf` and linked from the Download PDF button on the resume page.

### Tech icons

The `layouts/partials/tech-icon.html` partial maps technology names to brand icons from [Simple Icons](https://simpleicons.org/) and [Devicons](https://devicons.io/) CDNs. Add new mappings there to support additional chips/tags.

---

## Configuration

Key settings in `config.yml`:

| Setting | Value |
|---|---|
| `baseURL` | `https://taha-husain.github.io/` |
| `publishDir` | `docs` |
| `params.author` | Taha Husain |
| `params.avatarUrl` | `/avatar.jpg` |
| `services.googleAnalytics.ID` | `G-EMFCZ33WZB` |

Social links and nav menu items are also configured in `config.yml`.
