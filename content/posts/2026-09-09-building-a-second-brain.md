---
title: "Building a Second Brain: From Concept Based on Karpathy's Tweet to a Compound Engineering Loop"
date: 2026-09-09
description: "How I built a git-backed second brain: a capture layer, an AI compiler that turns raw ingestion into a durable wiki, and a compound-engineering loop that lets every session start smarter than the last."
tags: ["AI", "Second Brain", "Compound Engineering", "MCP", "Claude Code"]
draft: false
cover:
  image: "/assets/projects/second-brain-architecture.png"
  alt: "Two loops: one repo, one portfolio - Second Brain system architecture diagram"
  caption: "System architecture: capture, compile, and the inner/outer compound-engineering loops"
  relative: false
---

Since I read Andrej Karpathy's [viral tweet](https://x.com/karpathy/status/2039805659525644595) back in April, I've wanted to tackle building a 'second brain' where an LLM handles the organization, thinking, and maintenance. For as long as I can remember, I've had the consistent urge to streamline all that I consume across articles, newsletters, posts, Tweets, YouTube videos, and everything in between. I even created [a separate Household Manager harness](https://kdboller.github.io/projects/ai-native-house-manager/) to manage everything across our family and household. While my [Rube Goldberg machine](https://en.wikipedia.org/wiki/Rube_Goldberg_machine) of cobbled-together processes and tools worked alright, the room for improvement grew starker as I learned about implementations that "rode the latest AI model" capabilities. The gap was sharpest around continual improvement that compounds over time: a system that gets smarter with everything you feed it, instead of starting over from zero each session.

As an added bonus to achieving my second brain implementation, through this process I learned how to tie together all of my personal and work-related projects, leveraging the fundamentals of [compound engineering](https://lethain.com/everyinc-compound-engineering/). Given that this project summary is not a full recipe for how to set up a second brain, below I share the best resources that I've found that you can also reference to set up your own.

1. Andrej Karpathy's [viral tweet](https://x.com/karpathy/status/2039805659525644595) that started it all.
2. Andrej Karpathy's [follow up](https://x.com/karpathy/status/2040470801506541998?lang=en) to his viral tweet that linked to [a gist with instructions on how to implement](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).
3. [Aakash Gupta's instructional post](https://www.aibyaakash.com/p/karpathy-second-brain) on how to execute against Karpathy's original idea.

**How is this relevant to SMB / enterprise?**

[In this very recent podcast](https://pocketcasts.com/podcast/how-i-ai/29804190-0039-013e-0c58-0e1d7f698bfd/build-your-own-company-brain-the-enterprise-ai-playbook-from-stripes-engineering-team-sharadh-krishnamurthy/24133d0c-418a-4298-9028-f2ecc190b778), Claire Vo interviewed Sharadh Krishnamurthy, an engineering manager at Stripe, about his implementation of Kai, the company brain at Stripe that "unlocks AI for everyone" at Stripe. Here is the underlying premise:

1. The hard part about enterprise AI isn't getting the models right, it's replicating how the company already works, at scale, safely.
2. Kai works because Stripe over-invested in boring infra (DevEx, data platform, analytics layers) *before* AI existed, and that's what let agents run without tipping Production over.
3. Many people by now are familiar with [Projects in Claude](https://support.claude.com/en/articles/9517075-what-are-projects)/GPT et al, but **Projects** for Kai is the actual governance unit, not just a folder with relevant chats and files.
   1. Each Kai Project determines which model tier is allowed (cost/latency guardrails), which tools are permitted, and which tool calls require human-in-the-loop confirmation
   2. Kai even leverages a separate backend/harness for teams with sensitive data (HR runs a fully separate secure instance).

As I believe that organization infrastructure with the same underlying principles, framework, guardrails, and architecture as Kai is paramount for successful AI and agentic implementations, **I plan to engage SMB clients in the near to intermediate term in similar implementations that democratize AI for all employees in the most efficient and scalable way that also empowers full utilization of agentic capabilities.**

**What does Kai have in addition to my second brain approach given it's for enterprise?**

* Governance/permissions (needed once >1 person or any live action is involved)
* Live connectors (vs. static raw/)
* A skill lifecycle (needed once skill count outgrows what a human can eyeball)
* Execution sandboxing for individual customers (needed once the agent acts, not just answers)

---

**Summary of my personal Second Brain implementation.**

I've provided an outline and accompanying diagram of the architecture that I use. While the original idea dates back to April, the sticking point for me that I could not find time to finalize was **the ingestion layer**. I've used Instapaper and Pocket in the past, but neither met the full need. After some additional research and a bit of luck, I stumbled across [Reader](https://readwise.io/read), which I had a cursory awareness of.

<img src="/assets/projects/reader.png" alt="Readwise Reader" style="width: 100%">

I've found that Reader delivers as advertised, streamlining everywhere that I consume content. And for those who like to use coding agents and are familiar with MCP, it gets better! If you're not familiar with MCP, I suggest that you correct for that as well with all of the tremendous learning resources at your disposal, such as [this Anthropic course](https://anthropic.skilljar.com/introduction-to-model-context-protocol).

Here's a summary in the FAQ regarding Reader's MCP (my emphasis added):

**Does Reader work with AI assistants like ChatGPT and Claude?**

Yes, and it's becoming one of Reader's most powerful features. The [Readwise MCP server](https://readwise.io/mcp) connects Claude, ChatGPT, Cursor, or any MCP-compatible assistant directly to your library. ***Your AI can easily utilize the full content of your documents to answer questions grounded in your own reading, and the MCP can even organize your documents for you***. There's also a full [command line interface](https://readwise.io/cli) for the terminally inclined.

Here is a quick summary of my setup and a diagram that outlines the workflows.

<img src="/assets/projects/second-brain-architecture.png" alt="Two loops: one repo, one portfolio - Second Brain system architecture diagram" style="width: 100%">

**Summary:** A git-backed repo with a capture layer, a compilation layer, and a cross-project operating layer.

**Capture:** Readwise Reader is my inbox and ingestion layer for everything I consume: articles, highlights, forwarded emails, uploaded PDFs, plus Google Drive for working docs; live external tools (DataCamp, Sigma, Snowflake, Gmail, Calendar) get queried on demand via MCP rather than statically stored, so structured, dynamic data sits alongside all ingested document knowledge.

**Compilation:** as Karpathy outlines, sources land in a raw/ folder untouched, and Claude/Codex compile them into a wiki/ organized by entity type (people, projects, frameworks, sources); one source at a time, cross-linked, contradictions flagged rather than silently resolved, no RAG or vector DB.

**Loop.** The entire framework runs on a compound-engineering loop: Plan (consult the wiki before starting) → Work (complete relevant tasks) → Review (check against what's already stored/summarized/known) → Compound (write any new lessons back in).

As a result, each session starts at an elevated level relative to the last time.

**This project is also extensible to all of my work:** a separate skills/ layer at the repo root holds general operating practices that are shared across every other project repo I run as part of both my consulting business and my personal projects. The intent, which I'm still refining, is for a lesson learned in any of my projects to improve not only that project, via compounding engineering, but also harden the baseline for all my other projects, both current and future. The ultimate objective is that any new project starts at the elevated baseline of my entire second brain and the re-learning and re-training of implementation guidelines and best practices for the new project is minimized to the fullest extent.
