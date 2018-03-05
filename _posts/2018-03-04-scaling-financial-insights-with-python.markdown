---
layout: post
title:  "Scaling Financial Insights with Python"
date:   2018-03-04 12:00:00 -0500
categories: 
---

<img src="/assets/Python_Finance_hero.jpg" alt="Python Finance" height="500"  style="width: 100%">

<strong>As of 3/4, 2018, this post is currently in process.</strong>

<p>My two most recent blog posts were about Scaling Analytical Insights with Python; part 1 can be found <a href="https://kdboller.github.io/2017/07/09/scaling-analytical-insights-with-python.html">here</a> and part 2 can be found here.  It has been several months since I wrote those, largely due to the fact that I relocated my family to Seattle to join Amazon in November; the general consensus that Amazon presents a significant learning curve proved to be true in my situation and I spent most of my working hours becoming acclimated to my primary project and determining our global rollout plan and related business intelligence roadmap. </p> 

<p>At my former company, FloSports, prior to my departure we were in the process of overhauling our analytics reporting across the organization (data, marketing, product et al), and part of this overhaul included our financial reporting.  While I left prior to us getting too far along in that implementation, over the past several months I’ve continued using Python extensively, particularly pandas.  In this post, I will share how I leveraged some very helpful online resources, the Yahoo Finance API (which requires a work around and may require a future replacement), and Jupyter notebook in order to build a Python notebook which allows me to almost completely automate the tracking of my individual ticker and overall personal stock portfolio performance, as well compare relative performance to the S&P 500 at the individual position level.</p>
