---
title: "Personal Website Overhaul"
date: 2026-04-24
description: "Migrated personal website from Jekyll to Hugo with a full redesign and new Projects section."
link: "https://kdboller.github.io"
linkedin: ""
post: ""
image: "/assets/projects/claude-code-desktop.png"
featured: true
tags: ["Hugo", "GitHub Actions", "GLightbox", "Web Development", "Claude Code"]
---

Migrated personal website from Jekyll to Hugo, replacing a stale Jekyll 3.6.3 + Minima stack (last updated ~2021, Ruby 2.3.1) with Hugo 0.160.1 + PaperMod theme, that is now deployed via GitHub Actions to GitHub Pages.

**Key technical work:**

- Built a GitHub Actions CI/CD pipeline for automated deployment on push to main; subsequently upgraded all actions to Node.js 24-compatible versions ahead of GitHub's June 2026 forced cutover
- Implemented GLightbox for all post images. This auto-wires via JavaScript, no markup changes required per post, with "Photo by..." caption detection
- Designed and built a Projects content type from scratch: custom list and single-page templates, expandable/collapsible cards using native HTML `<details>`/`<summary>` (no JS), thumbnail support with full-width banner and lightbox, and a reusable partial as a single source of truth across the home page and Projects page
- Customized the home page with a Recent Projects section above the posts feed with both being driven by separate Hugo page queries
- Front matter supports link, LinkedIn, and post fields per project for flexible attribution
- Initial stand up of this website took an entire Saturday many years ago; working with Claude it was completely overhauled in ~1-2 hours
