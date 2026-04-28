---
title: "Agentic Demand Forecasting Data Product with Automated Workflows"
date: 2026-01-05
description: "Led a 0-to-1 subscription, advertising, and engagement demand forecasting data product with agentic workflows integrated into Salesforce, Slack, and Snowflake."
link: "https://claude.ai/public/artifacts/4e7e8f7c-b8bc-49ec-8076-8f5673d8beb2"
linkedin: ""
post: ""
image: "/assets/projects/agentic-demand-forecasting.png"
featured: true
weight: 1
tags: ["Python", "Sigma", "Snowflake", "Agentic AI", "Forecasting"]
---

Led a 0-to-1 subscription, advertising, and engagement demand forecasting data product.

When you're streaming 50k+ events per year, you cannot possibly forecast demand without an automated, scalable data infrastructure and continually improving ML-based forecasting models. You also should be able to dynamically compare alternative portfolio scenarios, such as decisions to add a new rights contract, to optimize revenue and profitability.

In our second iteration after our initial Streamlit application, I led the development of a Sigma-based AI and data application that projects signups, subscribers, subscription and ad revenue, and engagement at the contract level across all of our sports verticals. The underlying Python forecasting engine uses a cohort-based retention framework, historical plan mix, and viewership and live minutes 1P data to allocate revenue across signup, engagement, inactive, and dormant components. Ad revenue layers in based on forecasted engagement and inventory monetization, producing contract-level base forecasts that can also be compared dynamically against alternative portfolio scenarios.

I also led an agentic signup forecasting workflow that directly integrates into and drives this foundation. When a deal request is submitted via Salesforce, an automated workflow triggers the forecast models, posts outputs to Slack for human-in-the-loop review, and writes the confirmed forecast back to Salesforce and Snowflake.

Rights fees and cost per viewer hour became significantly more efficient through improved programming mix and renewal decisions, as we exited or did not renew deals where marginal cost exceeded marginal revenue. As a result, profitability in the largest vertical improved approximately 1,500 basis points in 2023, with an additional 500 basis points in each of 2024 and 2025, while revenue and engagement grew at more than 25% CAGR over the same period.
