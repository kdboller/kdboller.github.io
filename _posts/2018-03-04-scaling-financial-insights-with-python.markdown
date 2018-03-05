---
layout: post
title:  "Scaling Financial Insights with Python"
date:   2018-03-04 12:00:00 -0500
categories: 
---

<img src="/assets/Python_Finance_hero.jpg" alt="Python Finance" height="500"  style="width: 100%">

<strong>As of 3/4, 2018, this post is currently in process.</strong>

<p>My two most recent blog posts were about Scaling Analytical Insights with Python; part 1 can be found <a href="https://kdboller.github.io/2017/07/09/scaling-analytical-insights-with-python.html" target="_blank">here</a> and part 2 can be found here.  It has been several months since I wrote those, largely due to the fact that I relocated my family to Seattle to join Amazon in November; the general consensus that Amazon presents a significant learning curve proved to be true in my situation and I spent most of my working hours becoming acclimated to my primary project and determining our global rollout plan and related business intelligence roadmap. </p> 

<p>At my former company, FloSports, prior to my departure we were in the process of overhauling our analytics reporting across the organization (data, marketing, product et al), and part of this overhaul included our financial reporting.  While I left prior to us getting too far along in that implementation, over the past several months I’ve continued using Python extensively, particularly pandas.  In this post, I will share how I leveraged some very helpful online resources, the Yahoo Finance API (which requires a work around and may require a future replacement), and Jupyter notebook in order to build a Python notebook which allows me to almost completely automate the tracking of my individual ticker and overall personal stock portfolio performance, as well compare relative performance to the S&P 500 at the individual position level.</p>

<h2>Overview of PME and benchmarking individual stock performance</h2>

<p>As a quick background, I have been investing in my own stock portfolio since 2002.  I have used several brokers over the years and developed an overall financial model for my portfolio a number of years ago.  Each week I export stock prices from my broker and load the data into the financial model -- while my broker calculates all returns, income and dividends, I generally like to have this data in the model as I conduct my own analysis and determine if there are positions I should sell (“cut losses early and let winners run”).  One view which I’ve not yet seen from any of these brokers is how to create a “Public Market Equivalent”-like analysis.  In short, the Public Market Equivalent (PME) is a set of analyses used in the private equity industry to compare the performance of a private equity fund relative to an industry benchmark.  Much more detail here.  </p>

<p>Without getting into too much detail, it is very difficult to pick individual stocks which outperform the broader market, e.g., S&P 500.  Even if some of your individual stocks do outperform, the underperformance of others could outweigh these better performing stocks, meaning overall you’re worse off than simply investing in an index fund.  During business school I learned about PME, and I incorporated a conceptually similar analysis into the evaluation of my current portfolio holdings.  To do this properly, you should measure the timing of investment inflows specific to each portfolio position (holding periods) relative to an S&P 500 equivalent dollar investment over the identical time period.  As an example, if you bought a stock on 6/1/2016 and you still own it, you would want to compare an equal dollar investment on 6/1/2016 of the S&P 500 and compare the stock’s return to the S&P 500 equivalent return.</p>
    
<p>In the past, I have downloaded historical prices data from Yahoo Finance and used an INDEX and MATCH function combination in excel in order to calculate the relative performance of each position versus the S&P 500.  While this is an OK way to accomplish this goal, conducting the same in Python is much more scalable and flexible.  Whenever you download new data and load into excel, you inevitably need to modify some formulas and validate for errors.  Given market volatility, I’m very glad that I switched to the Python approach, as re-running this every Saturday morning is fairly trivial, whereas before using excel I only did this once every month or two.  The additional benefits are adding new calculations, such as cumulative ROI multiple (which I’ll cover), take about 30 seconds.  And the visualizations, which I use Plotly for, are highly reproducible to generate new insights.</p>

<p><strong>Disclosure:</strong>  <i>Nothing in this post should be considered investment advice.  These are general examples about how to download data for a small sample of stocks across different time intervals and benchmark their performance against an index.  You should direct all investment related questions that you have to your financial advisor.</i></p>

<p>Further, I am not an expert on this topic and I outline some limitations as well as future areas for development at the end of this post.  However, I believe the approach herein should still be very helpful, particularly for novice to intermediate-level professionals, especially since this approach and the visualizations extend to other types of financial analyses.  <strong>This approach is “PME-like” in the sense that’s it’s measuring inflows over equal holding periods, however, I have more work to do on the exited positions side of things.  As public market investments are much more liquid than private equity, and presuming you follow a trailing stop approach, from my perspective it’s more important to focus on active holdings -- you should be divesting holdings which underperform a benchmark or which you no longer want to own for various reasons, while I take a long-term view and am happy to own outperforming stocks for as long as they’ll have me.</strong></p>

<p>Resources:
    <ul>
    <li>I am a current DataCamp subscriber (future post forthcoming on DataCamp) and this community tutorial on Python for Finance is great.</li>
    <li>I have created a repo for this post including the Python notebook here, and the excel file here.</li>
    <li>If you want to see the full interactive version (because Jupyter <<-->> Github integration is awesome), you can view using nbviewer here.</li>
  </ul>
  <p>Outline of what we want to accomplish:
  <ul>
    <li>Import S&P 500 and sample ticker data, using the Yahoo Finance API</li>
    <li>Create a merged portfolio file which combines the sample portfolio dataframe with the historical ticker and historical S&P 500 data</li>
    <li>Determine what the S&P 500 close was on the date of acquisition of each investment, which allows us to calculate the S&P 500 equivalent share position with the same dollars invested</li>
    <li>Calculate the relative % and value returns for the portfolio positions over time, compared to the S&P 500 returns over that time</li>
    <li>Calculate cumulative investment returns and ROI multiple, in order to assess how well your portfolio compared to a market index</li>
    <li>One of the most important items:  dynamically calculate how each position is doing relative to a trailing stop, e.g., if a position closes 25% below it’s closing high, sell the position on the next trading day.</li>
    <li>Visualizations</li>
    <ul>
      <li>YTD and Trailing Stop Charts -- how is relative performance YTD and is the stock in violation of your trailing stop investing rules?</li>
      <li>Total Return Comparisons -- % return of each position relative to index benchmark</li>
      <li>Cumulative Returns Over Time -- $ Gain / (Loss) relative to benchmark</li>
      <li>Cumulative Investments Over Time</li>
    </ul>
  </ul></p>
  </p>
