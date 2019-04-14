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


### Introduction.
This post is the third installment in my series on leveraging ``Python`` for finance, specifically stock portfolio analyses.  In <a href="https://towardsdatascience.com/python-for-finance-stock-portfolio-analyses-6da4c3e61054" target="_blank">part 1</a>, I reviewed a Jupyter notebook with all of the code needed to extract financial time series data from the Yahoo Finance API and create a rich dataframe for analyzing portfolio performance across individual tickers.  The code also included a review of some key portfolio metrics with several visualizations created using the ``Plotly`` library.  In <a href="https://towardsdatascience.com/python-for-finance-dash-by-plotly-ccf84045b8be" target="_blank">part 2</a>, I extended Part 1's analyses and visualizations by providing the code needed to take the data sets generated and visualize them in a ``Dash by Plotly`` (``Dash``) web app.  

In this series continuation, I will provide an overview of Robo Advisors and then share additional code and details on how to evaluate a diversified index strategy.  This strategy can be used for several personal finance uses cases, including as part of a holistic approach that combines ETFs with individual stocks and bonds.  It could also be used to evaluate the efficacy of a Robo Advisor alongside a personally managed ETF strategy.  

Finally, one of the largest limitations from my initial approach was that the analyses did not account for dividends and compare <a href="https://www.investopedia.com/terms/t/tsr.asp" target="_blank">total shareholder return</a>.  Total shareholder return is now incorporated -- in my view, this is one of the largest gaps I've seen in retail investor personal portfolio apps.  It is extremely difficult to get an all-up view of portfolio performance, including investment timings and earned dividends.  My approach now accounts for both of these, which was a personal pain point that led me to solve this with my own product.  I will continue to evolve this portfolio performance web app; and I'll share future updates to see if there is a potential market for this approach as a consumer-facing app.     

### Overview of Robo Advisor.

Per <a href="https://www.nerdwallet.com/blog/investing/best-robo-advisors/" target="_blank">NerdWallet</a>, a robo-advisor is "an online, automated portfolio management service".  Robo Advisors use algorithms, which are based on rules that the individual user inputs and drive investment selection for the individual based on her risk tolerance and investment horizon (aka, time to retirement and/or financial objectives).  Robo Advisors offer much lower costs than traditional human financial advisory, with the tradeoff being that you generally do not have anyone to personally consult with regarding your financial objectives.  Robo Advisors are typically best suited for passive investors, who are comfortable with someone else building and optimizing a personal portfolio, and who also do not have complex financial situations.

Some of the major and most well known Robo Advisors include Wealthfront, SoFi and Betterment.  Personal Capital is another option in this space, although the company does not believe it should be classified as a Robo Advisor -- this is due to the fact that Personal Capital combines a sophisticated budgeting and portfolio monitoring application with virtual human financial advisors.  Personal Capital markets itself as a financial technology platform that can also advise higher net worth individuals and families who have more complicated financial situations.  

In this post, we will leverage a diversified ETF example that Personal Capital provides on its <a href="https://www.personalcapital.com/wealth-management/performance" target="_blank">Wealth Management performance page</a>.  I believe this is informative because I respect Personal Capital's approach, they're very transparent with their performance relative to benchmarks, and in my view the representative ETFs in the footnotes could be used to construct a sound investment strategy.

### Why Implement a Passive Investment Strategy.

[Active managers lose]...

[Don't try and time the market]... 

Outline.

1. Intro [**draft complete**] -- this is the third installment of a series on how to leverage ``Python``, ``pandas``, ``Dash`` and financial data APIs in order to automate personal portfolio tracking.

1. Overview Robo Advisor [**draft complete**]; i) passive versus active investing. ii) who are the main Robo Advisors; iii) how you can decently replicate their strategies bsaed on what's provided in this post.

Recent data points:  https://www.cnbc.com/2019/03/15/active-fund-managers-trail-the-sp-500-for-the-ninth-year-in-a-row-in-triumph-for-indexing.html; active fund managers trail; Bogle's recent book and quote on 'top decile returns when you invest in index funds'; Howard Marks book on where we are at in the credit cycle. 

1. Personal Capital benchmarking, which we'll use as our example. 

1. Limitations from prior time and how they've been addressed; the limitations from prior time included i) not including dividends and total shareholder return (addressed here); ii) not looking at divested positions (to be decided how I'll handle); iii) automate data pipelines to feed a live web dashboard (de-prioritized in order to focus on the right overall investment strategy).

1. Code -- only need to highlight the additions, which are focused on pulling in dividends, allocation comparison, comparing total shareholder return and then rolling up total return versus benchmark.

1. Conclusion -- I've not found a service out there that replicates this type of analysis, which I believe is imperative to make sure you're properly investing your money -- just tells you absolute portfolio return, doesn't effectively compare to benchmarks, and does not show total shareholder return.  A robo-advisor can do this for you, but every dollar you invest is subject to their fee structure, versus your time.  Still have a strategy that focuses on stocks with accelerating revenue growth and are industry leaders in high growth industries; for long-term portfolio strategy, believe a robo advisor / gone fishing is very sensible approach as part of an overall holistic strategy.  

If you enjoyed this post, it would be awesome if you would click the "claps" icon to let me know and to help increase circulation of my work.

Feel free to also reach out to me on twitter, <a href="https://twitter.com/kevinboller" target="_blank">@kevinboller</a>, and my personal blog can be found <a href="https://kdboller.github.io/" target="_blank">here</a>.  Thanks for reading!
