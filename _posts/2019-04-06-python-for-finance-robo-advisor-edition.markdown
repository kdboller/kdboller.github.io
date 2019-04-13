---
layout: post
title:  "Python for Finance:  Robo Advisor Edition"
date:   2019-04-06 12:00:00 -0500
categories: 
---

## Extending Stock Portfolio Analyses and Dash by Plotly to track Robo Advisor-like Portfolios.

<img src="/assets/aditya-vyas-783075-unsplash.jpg" alt="Wall St Stock Exchange" height="500"  style="width: 100%"> 

<> Photo by Aditya Vyas on Unsplash https://unsplash.com/photos/6Ih4UoqzaAs

## Part 3 of Leveraging Python for Stock Portfolio Analyses.

**As of early April 2019, this post is a work in progress.**

Outline.

1. Intro -- this is the third installment of a series on how to leverage ``Python``, ``pandas``, ``Dash`` and financial data APIs in order to automate personal portfolio tracking.

1. Overview of what a Robo Advisor is; i) passive versus active investing. ii) who are the main Robo Advisors; iii) how you can decently replicate their strategies bsaed on what's provided in this post.

1. Recent data points:  https://www.cnbc.com/2019/03/15/active-fund-managers-trail-the-sp-500-for-the-ninth-year-in-a-row-in-triumph-for-indexing.html; active fund managers trail; Bogle's recent book and quote on 'top decile returns when you invest in index funds'; Howard Marks book on where we are at in the credit cycle. 

1. Personal Capital benchmarking, which we'll use as our example. 

1. Limitations from prior time and how they've been addressed; the limitations from prior time included i) not including dividends and total shareholder return (addressed here); ii) not looking at divested positions (to be decided how I'll handle); iii) automate data pipelines to feed a live web dashboard (de-prioritized in order to focus on the right overall investment strategy).

1. Code -- only need to highlight the additions, which are focused on pulling in dividends, allocation comparison, comparing total shareholder return and then rolling up total return versus benchmark.

1. Conclusion -- I've not found a service out there that replicates this type of analysis, which I believe is imperative to make sure you're properly investing your money -- just tells you absolute portfolio return, doesn't effectively compare to benchmarks, and does not show total shareholder return.  A robo-advisor can do this for you, but every dollar you invest is subject to their fee structure, versus your time.  Still have a strategy that focuses on stocks with accelerating revenue growth and are industry leaders in high growth industries; for long-term portfolio strategy, believe a robo advisor / gone fishing is very sensible approach as part of an overall holistic strategy.  Will continue to evolve this idea to see if there is a consumer-facing product down the line and welcome any constructive feedback and additonal ideas.

If you enjoyed this post, it would be awesome if you would click the "claps" icon to let me know and to help increase circulation of my work.

Feel free to also reach out to me on twitter, <a href="https://twitter.com/kevinboller" target="_blank">@kevinboller</a>, and my personal blog can be found <a href="https://kdboller.github.io/" target="_blank">here</a>.  Thanks for reading!
