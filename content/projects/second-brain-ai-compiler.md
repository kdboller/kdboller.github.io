---
title: "Second Brain: AI Compiler & Compound Engineering System"
date: 2026-09-09
description: "A git-backed personal 'second brain': a capture layer (Readwise Reader, Drive, live MCP tools) feeds an AI compiler that turns raw ingestion into a durable, cross-linked wiki, run on a compound-engineering loop so every session starts smarter than the last."
link: ""
linkedin: ""
post: "/posts/2026-09-09-building-a-second-brain/"
image: "/assets/projects/second-brain-architecture.png"
tags: ["AI", "Second Brain", "Compound Engineering", "MCP", "Claude Code"]
---

Inspired by Andrej Karpathy's "second brain" concept, this is a git-backed system where an LLM handles the organization, thinking, and maintenance of everything I consume and everything I build.

**Capture:** Readwise Reader is the inbox and ingestion layer for articles, highlights, forwarded emails, and uploaded PDFs, plus Google Drive for working docs. Live external tools (DataCamp, Sigma, Snowflake, Gmail, Calendar) are queried on demand via MCP rather than statically stored, so structured, dynamic data sits alongside all ingested document knowledge.

**Compile:** Sources land untouched in a `raw/` landing zone. Claude and Codex act as an AI compiler, reading each source alongside a hand-authored schema and compiling it into a `wiki/` organized by entity type (people, projects, frameworks, sources), one source at a time, cross-linked, with contradictions flagged rather than silently overwritten. No RAG, no vector DB.

**Loop:** The whole system runs on a compound-engineering loop: Plan (consult the wiki before starting) → Work (do the actual task) → Review (check against what's already known) → Compound (write new lessons back in). A periodic lint loop separately checks the wiki and index for contradictions, stale claims, and orphaned pages.

**Outer loop:** A `skills/` layer at the repo root holds general operating practices shared across every other project repo I run, personal and consulting alike (including [AI-Native House Manager](/projects/ai-native-house-manager/) and [StreamingLTV](/projects/streaming-ltv-third-age/)), each running its own local Plan/Work/Review/Compound cycle. A lesson learned in any one project hardens the baseline for all the others, so any new project starts at the current baseline of the whole system instead of relearning it from scratch.

Full writeup, including how this connects to enterprise implementations like Stripe's internal "Kai" system, in the [related post](/posts/2026-09-09-building-a-second-brain/).
