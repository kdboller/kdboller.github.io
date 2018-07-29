---
layout: post
title:  "Python for Finance:  Plotly Dash"
date:   2018-07-13 12:00:00 -0500
categories: 
---

## Expanding Jupyter Notebook Stock Portolio Analyses with Interactive Charting in Plotly Dash.

<img src="/assets/plotly_dash_dashboard_hero.png" alt="Python Finance" height="500"  style="width: 100%">

## Part 2 of Leveraging Python for Stock Portfolio Analyses.

**As of 7/13, this post is currently in process.  Look forward to sharing a follow-up to the Python in Finance post with a dashboard, which includes some interactivity, using Plotly's Dash.**

In [part 1](https://towardsdatascience.com/python-for-finance-stock-portfolio-analyses-6da4c3e61054) of this series I discussed how, since I've become more accustomed to using ``pandas``, that I have signficantly increased my use of ``Python`` for financial analyses.   During the part 1 post, we reviewed how to largely automate the tracking and benchmarking of a stock portfolio's performance leveraging ``pandas`` and the ``Yahoo Finance API``.  At the end of that post you had generated a rich dataset, enabling calculations such as the relative percentage and dollar value returns for portfolio positions versus equally-sized S&P 500 positions during the same holding periods.  You could also determine how much each position contributed to your overall portfolio return and, perhaps most importantly, if you would have been better off investing in an S&P 500 ETF or index fund.  Finally, you used ``Plotly`` for visualizations, which made it much easier to understand which positions drove the most value, what their YTD momentum looked like relative to the S&P 500, and if any had traded down and you might want to consider divesting, aka hit a "Trailing Stop".

I learned a lot as part of building this initial process in Jupyter notebook, and I also found it very helpful to write a post which walked through the notebook, explained the code and related my thinking behind each of the visualizations.  This follow-up post will be much shorter than the prior one and more direct in its purpose.  While I've continued to find the notebook that I created helpul to track my stock portfolio, it had always been my intention to learn and incorporate a ``Python`` framework for building analytical dashboards / web applications.  One of the most important use cases for me is having the ability to select specific positions and the desired timeframe and evaluate the relative performances of each position.  In the future, I will most likely expand this evaluation case to positions I do not own but am considering acquiring.  For the rest of this year, I'm looking to further develop my understanding of building web applications in ``Flask``, deploying apps with ``Heroku``, and ideally developing some type of a data pipeline to automate the extracting and loading of new data for the end web application.  While I'm still rather early on in this process, in this post I will discuss the extension of the notebook I discussed last time with my initial development using ``Dash by Plotly``, aka ``Dash``.    

## Dash by Plotly.
If you have read or reference [part 1](https://towardsdatascience.com/python-for-finance-stock-portfolio-analyses-6da4c3e61054), you will see that once I created my master dataframe, you used ``Plotly`` to generate the visualizations which evaluate portfolio performance relative to the S&P 500.  While I really believe that Plotly is a very rich library and I prefer to create visualizations using ``Plotly`` relative to other Python visualization libraries such as ``Seaborn`` and ``Matplotlib``, I ultimately wanted to create an interactive dashboard / web app for my portfolio analysis.  I'm continuing to search for the optimal solution for this, and in the meantime I've begun exploring the use of ``Dash``.  Plotly defines [Dash](https://plot.ly/products/dash/) as a Python framework for building web applications with the added benefit that no JavaScript is required.  As indicated on the landing page which I link to, it's built on top of Plotly.js, React, and Flask.  

The initial benefit that I've seen thus far is that, once you're familiar and comfortable with ``Plotly``, ``Plotly Dash`` is a natural dashboard / web app extension.  Rather than simply house your visualizations within the ``Jupyter`` notebook where you conduct your analysis, I definitely see value in creating a stand-alone web app for review and analysis.  Additionally, the benefit of ``Dash`` is increased interactivity and the ability to manipulate data with "modern UI elements like dropdowns, sliders and graphs".  This functionality directionally supports what I want in my ultimate goal for my stock portfolio analyses, including the ability to conduct 'what if analyses', as well as interactively research potential opportunities and quickly understand key drivers / scenarios.  Another key goal is to build a data pipeline which refreshes data on a scheduled cadence, which is a future deliverable that I intend to run to ground.  With all of this considered, the learning curve with ``Dash``, at least for me, is not insignificant, and developing a polished dashboard with, e.g., Bootstrap, is not easily executed.  

### Jose Portilla's "Interactive Python Dashboards with Plotly and Dash"
To short circuit the time that it would have taken for me to read through and extensively troubleshoot Dash's documentation, I enrolled in [Jose Portilla's](https://medium.com/@josemarcialportilla) ``Plotly and Dash`` course on Udemy.  The detail page for that course can be found [here](https://www.udemy.com/interactive-python-dashboards-with-plotly-and-dash/).  I have taken a few of Jose's courses and am currently taking his ``Flask`` course.  I view him as a very sound and helpful instructor -- while he generally does not presume extensive programming experience as prerequisites for his courses, in this ``Dash`` course he does recommend at least a strong familiarity with ``Python``.  In particular, having a strong understanding of ``Plotly's`` syntax for visualization, including using ``pandas``, are highly recommended.  After taking the course, you would really still be scratching the surface in terms of ``Dash``.  However, I found the course to be a very helpful jump start, particularly because Jose uses ``datareader`` and also uses financial data, including dynamically pulling stock price charts, for his examples.

## Porting Data from Jupyter Notebook to Interact with it in Dash.

### Getting Started
As provided in [part 1](https://towardsdatascience.com/python-for-finance-stock-portfolio-analyses-6da4c3e61054), I have created [a repo on Github](https://github.com/kdboller/pythonsp500-plotly-dash) with all of the files and code required to create the final ``Dash`` dashboard. 

Below is a summary of what is included and how to get started:
1. First ordered item.


```python
# Placeholder


```


* analyzed query csv generated by Jupyter notebook.
* ticker csv generated by Jupyter notebook. 
* where the graph lives within the div; describe how set up, slight modifications in syntax.
* call back
* function
* talk about how the rest of the charts are from Python notebook.

### Requirements File.
[Placeholder -- discuss Portilla's course].

Benefits:
* interactivity.
* what / if type analysis.
* love working with Jupyter notebook when not sure what end result will look like -- Dash can serve as a polished end product.


## Future considerations.
* Mode with Google BigQuery
* Heroku with Postgres and Data Pipeline



[Conclusion].
