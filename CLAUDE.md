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

## Project Frontmatter Template
```yaml
---
title: "Project Title"
date: YYYY-MM-DD
description: "One or two sentence description (used as meta description and homepage card summary)."
link: ""           # live product/demo URL, renders "View Project →" if set
linkedin: ""       # LinkedIn post URL, renders "LinkedIn Post →" if set
post: ""           # relative path to a related content/posts/ entry, renders "Related Post →" if set
image: "/assets/projects/filename.png"
featured: true     # optional, see Featured Projects below
weight: 1          # optional, influences ordering among featured/default-sorted pages
tags: ["Tag1", "Tag2"]
---
```
- All three link fields (`link`, `linkedin`, `post`) are optional and independent: set only the ones that apply, per `layouts/partials/project-card.html`
- The homepage's "Recent Projects" list and `/projects/` both use `project-card.html`

## Featured Projects
- Homepage shows the first 2 pages (any type) with `featured: true` in `params`, via `layouts/index.html`
- Exactly 2 should be featured at a time. When adding a new featured project, un-feature (remove `featured: true` and any `weight`) from an existing one first
- The featured card's summary is auto-derived: it takes the page's rendered `.Summary` and truncates to the text before the *first period*, then appends one period. Keep the first sentence of the body short, end it with a period (not a `?` or `!`), and put any longer follow-up detail in a second sentence/paragraph so it doesn't bleed into the card

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

## Links
- `layouts/_markup/render-link.html` is a Goldmark render hook: any markdown link (`[text](url)`) whose host differs from the site's own automatically gets `target="_blank" rel="noopener noreferrer"`. Internal links stay same-tab.
- Do **not** hand-add `target="_blank"` to markdown links: the hook already covers it site-wide. Only a raw HTML `<a>` tag (not markdown syntax) would need it added manually, since those bypass the hook.

## Content Style
- No em dashes (—) anywhere in post/project copy or frontmatter: use a comma, period, colon, or parentheses instead

## Nav Menu
About (weight 10) → Projects (weight 20) → Posts (weight 30)

## Key Config
- Site title: "Data Informed Narratives"
- Base URL: `https://kdboller.github.io/`
- `resume.md` exists at repo root but is intentionally not wired into Hugo nav — do not touch
