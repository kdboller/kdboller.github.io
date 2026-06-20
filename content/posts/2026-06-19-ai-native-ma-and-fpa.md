---
title: "AI-Native M&A and FP&A"
date: 2026-06-19
description: "An examination of AI-native approaches to M&A and FP&A. Spans enterprise AI platforms, compute allocation strategy, and the critical distinction between production-ready harnesses and non-scalable vibe coding."
tags: ["AI", "FP&A", "M&A", "Enterprise AI", "Agentic AI"]
cover:
  image: "/assets/growtika-nGoCBxiaRO0-unsplash.jpg"
  alt: "Abstract image of a sphere with dots and lines"
  caption: "Photo by [Growtika](https://unsplash.com/@growtika?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/photos/an-abstract-image-of-a-sphere-with-dots-and-lines-nGoCBxiaRO0?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
  relative: false
---

## Thesis

Today, most enterprise AI implementations are point solutions with a strategy-enforced ceiling.

**The greatest opportunity for an AI-native M&A or FP&A execution is one that:**

* Establishes an enterprise-wide platform and decision engine that leverages deterministic workflows, parallelizes specialized agent execution, and compounds knowledge over time
* Evaluates and evolves its compute allocation strategy to drive scale and operating leverage, and
* Leverages a build vs. buy framework that provides future optionality to use best of breed solutions throughout

## Anthropic Is Building the Platform

**Opportunistically building the application layer (non-core focus)**

* Anthropic (Claude Code, Cowork, Claude in Excel et al) is building the infrastructure and model layer.
* Does not plan to compete with applications built on top of the Claude platform.

**Priority focus is showing customers what's possible**

* Suite of Claude offerings' primary role is to demonstrate what can be built.
* Note: Will opportunistically go vertical when have model-level insight or ecosystem signaling function

## The Concept of Compute Allocation

> "We're all becoming 'compute allocators' and our main job is to decide what's worth spending compute on."

**What this means in practice**

* Most generated tokens (up to 99%) will not/should not end up as production code.
* These tokens are generated to confirm exactly what should be shipped.
* Problem: a lot of AI implemented into Production today is vibe coded and likely should not be in this 1%.

## Production Ready: Harnesses vs. Vibe Coding

**What is a harness?**

* The surrounding infrastructure, memory, and operational software that transforms a raw, standalone AI model into a reliable, autonomous agent.
* While the model provides the reasoning layer, the harness provides the controls, managing external tools, context, and guardrails.

**Why does it matter?**

* Vibe-coded apps should largely be the 99% of tokens that never make it to Production.
* Enterprise-grade harnesses make the 1% auditable, governable, and safe to deploy at enterprise scale.

## Advanced Thinking: Early Days of the Model Routing Strategy

| | |
| :--- | :--- |
| **The Problem** | Processing all employee AI requests through large frontier models is expensive and often unnecessary for routine tasks. |
| **The Framework for a Solution** | An intelligent routing layer that sits between customers and models. Evaluates query complexity and routes accordingly: complex tasks go to frontier models while simpler tasks can go to smaller, cheaper, and often localized models. |
| **The Business Impact** | Dynamic routing reduces operational and inference costs while optimizing performance across the organization. Similar to operating leverage in finance: increasing revenue while reducing variable costs and overall cost structure. |

## Observations: Demand Forecasting Workflow

**Bespoke workflow that automated a previously tedious, time consuming, and difficult to audit process.**

* While advantageous to the business, the scaling benefits had a ceiling.
* Greater benefits required a larger, enterprise-wide AI platform initiative

**Pre-dated the concept of Model Routing Strategy**

* Non-optimized token consumption, which also introduces a ceiling to the operating leverage that workflows such as this can drive for the business.

## Production Ready Example #1: Sigma

> "You can pretend vibe coding isn't happening and find out the hard way the first time a handbuilt agent takes an action you cannot explain to a regulator, an auditor, or a customer. Or you can put it on a foundation that lets every app and every agent inherit the governance you already have in place." — Mike Palmer, CEO at Sigma

{{< figure src="/assets/sigma_vibe%20coding.png" alt="Sigma on vibe coding governance" width="70%" >}}

## Production Ready Example #2: Summation

To be decision-grade, AI must:

**Understand context.** Connect interdependent datasets across finance and operations and model their relationships, so metrics reflect reality.

**Ensure traceability.** Every answer is verifiable and defensible — with sources, lineage, and auditability.

**Scale analysis.** Explore thousands of questions in parallel so leaders don't miss what matters.

**Summation — Bellevue, WA**

{{< figure src="/assets/summation.png" alt="Summation financial performance dashboard" width="70%" >}}

## Conclusion

[TO COME].
