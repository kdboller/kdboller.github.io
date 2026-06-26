---
title: "AI-Native M&A and FP&A"
date: 2026-06-19
description: "An examination of AI-native approaches to M&A and FP&A. Spans enterprise AI platforms, compute allocation strategy, and the critical distinction between production-ready harnesses and non-scalable vibe coding. Let's make Jevons paradox the great reality!"
tags: ["AI", "FP&A", "M&A", "Enterprise AI", "Agentic AI"]
cover:
  image: "/assets/growtika-nGoCBxiaRO0-unsplash.jpg"
  alt: "Abstract image of a sphere with dots and lines"
  caption: "Photo by [Growtika](https://unsplash.com/@growtika?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/photos/an-abstract-image-of-a-sphere-with-dots-and-lines-nGoCBxiaRO0?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
  relative: false
---

With all of the investment in and implementation of enterprise AI, one would think that AI should be transformative for so many aspects of work. AI will drive higher revenue, increase efficiency, and improve productivity while transforming the toil of labor into a more enjoyable existence for knowledge workers. However, as has become common knowledge at this point, despite the seeming panacea that AI transformation is touted to be, [the majority of businesses continue to not see a return on their AI investments](https://www.forbes.com/sites/timkeary/2026/04/30/the-roi-crisis-why-companies-fail-to-see-returns-from-ai-pilots/).

While this is covered quite extensively by [McKinsey](https://www.mckinsey.com/capabilities/business-building/our-insights/the-seven-operating-truths-of-ai-native-companies?stcr=2195024BD0DE435B9CD22901DDAE02BE&cid=mgp_opr-eml-alt-dna_lp-mgp-glb--&hlkid=6396044309804a0b8890bbfc9a6918aa&hdpid=7901c200-89e6-40a8-b2f8-c406df93335a) and others, my summary view is that **most enterprise AI implementations are point solutions with a strategy-enforced ceiling**. Layering AI on top of sub-optimal workflows, or ones that should no longer exist, is an obvious path to failed AI implementation outcomes.

In order to succeed, before any AI implementation starts, all companies should step back and:

1. Determine the objectives they'll work backwards from,
2. Outline a before and after state of their workflows that will be continued, added, or deprecated in order to drive to their end objectives, and then
3. Establish the appropriate new departmental structures and the future job responsibilities that drive the success of these new structures.

With this organizational re-structure established, to be successful in the AI-native pursuit and to lay the foundation for ROI, an organization must then outline the software and technical foundation for enterprise-grade AI decisioning. Complexities here include picking the right AI stack (more on this further below) and defining a department by department approach to **compute allocation**. Additionally, finance orgs need to establish a continually evolving revenue and cost forecasting engine that incorporates an organizational LLM "model routing strategy" for all agentic AI workflows. The goal here is to prudently allocate token consumption and spend that is tied to workflow complexity and related model requirements.

---

With this backdrop established, let's take a look at the specific marketplace activity that supports this thesis, including some exciting announcements and fascinating innovations that have taken place in just the past few months.

## Anthropic CFO

In May, Anthropic's CFO, Krishna Rao, appeared on [the Invest with the Best podcast](https://colossus.com/episode/the-cone-of-uncertainty/). The following were my takeaways from the discussion. First, Anthropic is focused on building **the platform for enterprises**. Yes, the company is opportunistically building the application layer, but this is a non-core focus (for now). With products including Claude Code, Cowork, and Claude in Excel, Anthropic is focused on establishing the infrastructure and model layer. In general, the company does not plan to compete with applications built on top of the Claude platform. Rather, the priority focus is showing customers what's possible and demonstrating **what can be built** while still signaling that they will opportunistically go vertical when they have a model-level insight or ecosystem signaling function.

## The Concept of Compute Allocation

[Thariq Shihipar, from Anthropic, spoke with Claire Vo on "How I AI"](https://www.chatprd.ai/how-i-ai/claude-code-anthropic-thariq-shihipar-on-replacing-markdown-with-html) about how he uses HTML to brainstorm ideas, build micro apps for editing, and manage living design systems with Claude. The primary takeaway from the discussion was that "we're all becoming 'compute allocators' and our main job is to decide what's worth spending compute on." In practice, this means that most generated tokens (up to 99%) will not/should not end up as production code. Instead, **these tokens are generated to confirm exactly what should be shipped**. Which brings us to one of the underpinnings of the lack of enterprise AI returns on investment: many companies are executing the inverse of this approach where a lot of AI implementations in Production today are vibe coded apps. Given this, production challenges are not surprising, as the 99% of tokens that are meant to serve in deciding what should be in Production are instead becoming the enterprise deployed application.

## Advanced Thinking: Early Days of the Model Routing Strategy

While we're all becoming "compute allocators", it's still not enough to determine what projects, applications, and even features are worth spending compute on. Once compute allocation decisions are made, you must also determine the right mix of frontier and open source models to satisfy the necessary compute. **The problem:** processing all employee AI requests through large frontier models is expensive and often unnecessary for routine tasks. **The solution**, which is becoming more broadly established, is an intelligent routing layer that sits between customers and models. This routing layer evaluates query complexity and routes accordingly: complex tasks go to frontier models while simpler tasks can go to smaller, cheaper, and often localized models. At this point, the business impact should be clear. Dynamic routing reduces operational and inference costs while optimizing performance across an organization. **This is an operating leverage unlock: revenue expansion while reducing variable costs and overall cost structure.**

## Production Ready: Harnesses vs. Vibe Coded Apps

If the vast majority of vibe coded apps should largely not be in the 1% of tokens that make their way into production, what's the right framing that allows departments to understand what enterprise AI deployments should look like?

This brings us to the difference between a harness and a vibe coded app. As discussed previously, Anthropic (Claude Code et al) is largely building the platform, and for the most part enterprises will leverage its infrastructure capabilities rather than buy applications directly from Anthropic. So what is a harness? A harness is the surrounding infrastructure, memory, and operational software that transforms a raw, standalone AI model into a reliable, autonomous agent. While the model provides the reasoning layer, the harness provides the controls, managing external tools, context, and guardrails.

**Why does this matter in practice?**

* Vibe-coded apps should largely be the 99% of tokens that never make it to Production.
  * These are very helpful for prototyping.
  * For example, you can now collapse what was once a very detailed product requirements document (PRD) into a paragraph of text and a vibe coded prototype app.
  * This accelerates an organization's timeline in determining what should be built and where to prioritize alongside much clearer communication.
* By contrast, **harnesses** ensure that the 1% of token consumption that makes it into an enterprise-wide decision engine is auditable, governable, and safe to deploy at scale.

## Enterprise-Grade Harness Example #1: Sigma

> "You can pretend vibe coding isn't happening and find out the hard way the first time a handbuilt agent takes an action you cannot explain to a regulator, an auditor, or a customer. Or you can put it on a foundation that lets every app and every agent inherit the governance you already have in place." — Mike Palmer, CEO at Sigma

{{< figure src="/assets/sigma_vibe%20coding.png" alt="Sigma on vibe coding governance" width="70%" >}}

Sigma has had a tremendous start to 2026, as covered in [this April-June 2026](https://www.sigmacomputing.com/blog/new-on-sigma-spring-2026) post by Luke Stanke. Their recent innovations include:

1. [Sigma Agents](https://www.sigmacomputing.com/product-launch/sigma-agents-2026). AI agents that live inside Sigma and take action on your data via Sigma's robust action framework. These Agents can now plug into a company's software development lifecycle, support governed metrics as context, and have a rebuilt building experience that makes assembling an agent feel closer to configuring a workbook than writing a spec.
2. [Sigma Assistant](https://www.sigmacomputing.com/blog/introducing-sigma-assistant). Ask a question and Sigma Assistant answers it using the context an organization has already built, including data models, certified metrics, and the endorsed workbooks that signal which sources the organization trusts. Also, customers can describe what they want to build, and Sigma Assistant builds it, whether that is a single chart or the scaffolding of a full application.
3. [Code-backed Sigma](https://www.sigmacomputing.com/blog/migrate-from-legacy-bi-to-sigma): Over the spring, Sigma became a platform where you can write in code. This is a huge step forward: "when a workbook is code, a coding agent can read a legacy dashboard, interpret its structure, and generate the Sigma equivalent programmatically, from discovery through verified data parity, in a single run, with a final check comparing every chart's numbers back to the source. What used to be a quarter of manual rebuild work now looks like a supervised afternoon."

## Enterprise-Grade Harness Example #2: Summation

Summation, based in Bellevue, WA, serves as [a decision-grade AI platform for enterprises](https://www.summation.com/resources/introducing-summation). The platform is founded in large part on the "Monday Morning test": on a Monday morning, the executive team walks in and is met with dashboards, a heavy presentation, and various spreadsheets. While the business performance is summarized in terms of financial outputs and recent outcomes, the second- and third-order questions that demand connected context are the ones that escape answerability. In other words, business insights are incomplete or altogether missing, cannot be retrieved on demand, and require special, time consuming projects to root cause and report back on.

As Summation states, to be decision-grade, AI must:

**Understand context.** Connect interdependent datasets across finance and operations and model their relationships, so metrics reflect reality.

**Ensure traceability.** Every answer is verifiable and defensible — with sources, lineage, and auditability.

**Scale analysis.** Explore thousands of questions in parallel so leaders don't miss what matters.

{{< figure src="/assets/summation.png" alt="Summation financial performance dashboard" width="70%" >}}

With this underlying business foundation, Summation is an AI-native platform that is structured to transform how enterprises make decisions. It aims to accomplish this by unifying fragmented data, orchestrating AI agents at scale, and enforcing traceable verification. This enables leaders to have the confidence to make decisions based on verified data and scalable insights that identify the impact that key levers are having on recent and future expected performance.

## Conclusion

My professional work that relates to the adoption of enterprise AI principally resides within corporate development (M&A execution and integration) and financial planning and analysis (FP&A). As mentioned, in order to build AI-native M&A and FP&A departments, organizations must first establish the infrastructure that unlocks an AI-native organizational decision engine. The success of this decision engine will be predicated on the business context and workflow knowledge that is codified, continually maintained and evaluated, and incorporated into the organization's agentic AI workflows. A first principled implementation then permits AI to execute against largely deterministic workflows and verified data sources, minimizing probabilistic evaluations. After all, probability is where hallucinations can occur, and incorporating observability into continual applied AI evaluations ensures that any model drift as time goes on can be proactively identified and corrected.

Excitingly, once a department, such as FP&A, is reconfigured for the future state and its deterministic workflows have been wired to run through specialized agents with the appropriate business knowledge and context, the company should capture operational gains. These can include accelerated revenue, higher retention and upsell of recurring revenue, and expanding operating margins. However, those gains do not need to end there. **With the constant advancements in open-sourced and frontier models, this enforces the need to continually evaluate and evolve compute allocation strategies that can further adoption, scale, and operating leverage within the business**. In other words, as models advance, overall token costs can go down while performance and knowledge are able to increase. This allows for continued opportunity for value capture, providing operating leverage where revenue can compound at a higher rate than fixed and variable costs.

Last, and perhaps most critically, in order to capture the full opportunity that AI presents, **companies must wisely determine where to place their bets in terms of technical infrastructure and software**. Focusing on core competencies and where expertise lies is now more critical than ever. On the one hand, Company A could move off of Salesforce and build a vibe-coded CRM product that is non-core to its DNA and expertise. While this is arguably possible given the unlock that is Claude Code/Codex, it reminds me of the prescient quote from Dr. Ian Malcolm in Jurassic Park: "Your scientists were so preoccupied with whether or not they could, they didn't stop to think if they should." However, Company A will be on the hook for all future support, maintenance, security, and all of the related challenges that come with enterprise software. Separately, Company B could choose to build all of its reporting in bespoke artifacts built off of a Claude Code foundation. However, similar to Company A, Company B is now on the hook for any innovation needed to generate more powerful insights and self-serve analytics, as well as data modeling, governance, and potential security risks.

My straightforward advice to Company A and Company B would be the following: give a thorough look at Sigma and Summation, respectively. 99% of token consumption is likely better served in your business than trying to evolve the platform underneath your enterprise grade decision engine. And, the benefits of selecting platforms like these is the same as it has always been in "build versus buy" decisioning: 1) all of the investment in vendor innovations can accrue to the benefit of enterprise customers; and 2) the learning these vendors apply to their platforms is based on all of their customers, way more signal than an individual business will get from its usage and business cases. Plus, as seen in the first 6 months of this year, the advancement cycle in these platforms is only accelerating. In terms of risk mitigation, I'd argue that software lock-in is lower than it has ever been. The ability to transition from one platform to another has never been easier due the facilitation of coding agents such as Claude Code. As a direct example, [Sigma's Tableau to Sigma repo](https://github.com/twells89/sigma-migration-skills/tree/main/plugins/tableau-to-sigma).

**When enterprise AI implementation is done successfully, which is non-trivial per the details in this post, my hope is that this will also justify additional knowledge worker hires who can further growth opportunities across the organization.** We can all do more to make [Jevons paradox](https://en.wikipedia.org/wiki/Jevons_paradox) the great reality!
