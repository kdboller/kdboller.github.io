---
title: "AI-Native House Manager App (Next.js + Supabase)"
date: 2026-06-15
description: "Building an AI-native household management app for busy parents that learns about your family over time and drives actionable workflows rather than piecemeal outputs."
link: ""
linkedin: ""
post: ""
image: "/assets/projects/House Manager Dashboard.png"
featured: true
tags: ["Next.js", "TypeScript", "Supabase", "PostgreSQL", "Claude API", "Tailwind CSS", "Vercel", "AI"]
---

Building an AI-native household management app designed for busy parents. Provides households with an intuitive application that learns more about your family and improves over time. Eliminates the setup, development, maintenance, API-cost tracking, and overall burden of building with Claude Cowork/Claude Code, while delivering a comprehensive household management solution that drives actionable workflows rather than piecemeal outputs, like an email digest of the week ahead.

**Tech stack:** Next.js 16 (App Router), TypeScript, Supabase/Postgres, Claude API, Tailwind CSS + shadcn/ui, deployed on Vercel. Claude API calls run server-side.

**Applied AI features:**

- **Agent email triage:** Gmail integration with a per-sender monitoring gate. Claude triages opted-in senders: summarizes, extracts structured data, classifies, drafts replies, and surfaces everything in an Action Needed queue
- **Family context layer:** Server function assembles a structured prompt block from the DB for Claude API calls. Structured context upfront means outputs are more deterministic and consistent across features
- **Skill-based AI behaviors:** AI tasks (weekly digest generation, email triage, assistant Q&A) are encoded as versioned skill files that capture domain rules and edge cases. Skills define the expected behavior and are independently improvable without touching application code
- **Week-ahead digest:** AI-generated "Next Two Weeks" summary card surfaces upcoming health appointments, school events, vendor visits, and tasks. Refreshable on demand
- **Draft → Approve → Act pattern:** The AI never takes unilateral action. The focus is on keeping humans in the loop before anything is sent or committed
- **Telemetry on every AI call:** input_tokens, output_tokens, cache_read_tokens, latency_ms, and prompt_version captured per feature at build time. Usage tab shows API cost by day, supporting per-feature cost tracking and prompt regression debugging

**Key technical work:**

- 8-module app: Dashboard, Email Triage, Kids Health, Car Maintenance, Home Vendors, Utilities, Pets, and a Calendar screen (FullCalendar supporting different school feeds)
- 40+ table Postgres schema in Supabase, including staging/prod split via Supabase CLI with a migration workflow
- Deployed to Vercel with feature-branch workflow