# Personal Website — CLAUDE.md

## Stack
- **Hugo** 0.160.1 Extended + **PaperMod** theme (git submodule at `themes/PaperMod`)
- Deployed to **kdboller.github.io** via GitHub Actions (`.github/workflows/deploy.yml`) — push to `main` auto-deploys
- Hugo binary: `hugo` (available on PATH after shell restart, or full path at `C:\Users\kdbol\AppData\Local\Microsoft\WinGet\Packages\Hugo.Hugo.Extended_Microsoft.Winget.Source_8wekyb3d8bbwe\hugo.exe`)

## Local Preview
```
hugo server        # live site (drafts excluded)
hugo server -D     # include draft posts
```

## Content Structure
```
content/
  posts/           # blog posts (dated filenames: YYYY-MM-DD-slug.md)
  projects/        # project pages
  about.md
  investing.md
  resources.md
static/assets/     # all images
hugo.toml          # site config
```

## Post Frontmatter Template
```yaml
---
title: "Post Title"
date: YYYY-MM-DD
description: "One or two sentence description."
tags: ["Tag1", "Tag2"]
draft: false       # omit or set true to hide from live site
cover:
  image: "/assets/filename.jpg"
  alt: "Alt text"
  caption: "Photo by [Name](url) on [Unsplash](url)"
  relative: false
---
```

## Images
- Store all images in `static/assets/`
- Reference in markdown: `![alt](/assets/filename.png)`
- To control size, use Hugo's figure shortcode:
  ```
  {{< figure src="/assets/filename.png" alt="description" width="70%" >}}
  ```
- URL-encode spaces in filenames: `sigma_vibe%20coding.png`

## hugo.toml Notes
- Do **not** use actual newlines in TOML basic strings — use `\n` escape sequences or triple-quoted strings
- `buildDrafts = false` — drafts never appear on the live site
- GA4 property: `G-4Z5WDRZPV1` (PaperMod injects the script automatically via `env = "production"`)
- `markup.goldmark.renderer.unsafe = true` — required for inline HTML in markdown

## Nav Menu
About (weight 10) → Projects (weight 20) → Posts (weight 30)

## Key Config
- Site title: "Data Informed Narratives"
- Base URL: `https://kdboller.github.io/`
- `resume.md` exists at repo root but is intentionally not wired into Hugo nav — do not touch
