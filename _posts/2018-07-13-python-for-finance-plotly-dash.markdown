---
layout: post
title:  "Python for Finance:  Dash by Plotly"
date:   2018-07-13 12:00:00 -0500
categories: 
---

## Expanding Jupyter Notebook Stock Portolio Analyses with Interactive Charting in Dash by Plotly.

<img src="/assets/carlos-muza-84523-unsplash.jpg" alt="Python Finance" height="500"  style="width: 100%">

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
As provided in [part 1](https://towardsdatascience.com/python-for-finance-stock-portfolio-analyses-6da4c3e61054), I have created [a repo on GitHub](https://github.com/kdboller/pythonsp500-plotly-dash) with all of the files and code required to create the final ``Dash`` dashboard. 

Below is a summary of what is included and how to get started:
1. **Investment Portfolio Python Notebook_Dash_blog_example.ipynb** -- this is very similar to the Jupyter notebook from part 1; the additions include the final two sections: a 'Stock Return Comparisons' section, which I built as a proof-of-concept prior to using ``Dash``, and 'Data Outputs', where I create csv files of the data generated which will be the data sources used in the ``Dash`` dashboard.
2. **Sample stocks acquisition dates_costs.xlsx** -- this is the toy portfolio file, which you will use or modify for your portfolio assessments.
3. **requirements.txt** -- this should have all of the libraries you will need.  I recommend creating a virtual environment in Anaconda, discussed further below.
4. **Mock_Portfolio_Dash.py** -- this has the code for the ``Dash`` dashboard which we'll cover below.

As per my repo's [README file](https://github.com/kdboller/pythonsp500-plotly-dash/blob/master/README.md), I recommend creating a virtual environment using Anaconda.  Here's a quick explanation and a link to more detail on Anaconda virtual environments:

I recommend Python 3.6 or greater so that you can run the Dash dashboard locally with the provided csv files.
[Here](https://medium.freecodecamp.org/why-you-need-python-environments-and-how-to-manage-them-with-conda-85f155f4353c) is a very thorough explanation on how to set up virtual environments within Anaconda.

Last, as mentioned in part 1, once your environment is set up, in addition to the libraries in the requirements file, if you want the Yahoo Finance datareader piece to run in the notebook, you will also need to ``pip install fix-yahoo-finance`` within your virtual environment. 

### Working with Dash
If you have followed along thus far in setting up a virtual environment using Python 3.6, and have installed the necessary libraries, you should be able to run the ``Python`` file with the Dash dashboard code.

If you would like the full explanation on the Jupyter notebook and generating the portfolio data set, please refer to [part 1](https://towardsdatascience.com/python-for-finance-stock-portfolio-analyses-6da4c3e61054).  At the end of the Jupyter notebook, you will see the below code in the 'Data Outputs' section.  These minor additions will send CSV files into your local directory.  The first is the full portfolio dataset, from which we can generate all of the visualizations, and the second provides the list of tickers will use in the first, new stock chart's dropdown.

```python
# Generate the base file that will be used for Dash dashboard.

merged_portfolio_sp_latest_YTD_sp_closing_high.to_csv('analyzed_portfolio.csv')
```

I'll highlight some key aspects of the Mock Portfolio Python file and share how to run the dashboard locally.  

For reference while we breakdown the .py file, below is a screen grab of what you should see when running this ``Dash`` dashboard.

<img src="/assets/Mock Portfolio Dash_sample screenshot.png" alt="Dash Dashboard" height="500"  style="width: 100%">

At the beginning of the .py file, you import the libraries included in the requirements.txt file, and then write ```python app = dash.Dash() ``` in order to run the dashboard from the command line.
You then create two dataframe objects, ``tickers`` and ``data``.  Tickers will be used for the stock tickers in one of chart's dropdowns, and the data dataframe is the final data set which is used for all of the visualization evaluations.

You wrap the entire dashboard in a div, and then 






* analyzed query csv generated by Jupyter notebook.
* ticker csv generated by Jupyter notebook. 
* where the graph lives within the div; describe how set up, slight modifications in syntax.
* call back
* function
* talk about how the rest of the charts are from Python notebook.


## Conclusion and Future considerations.

Benefits:
* interactivity.
* what / if type analysis.
* love working with Jupyter notebook when not sure what end result will look like -- Dash can serve as a polished end product.

* Mode with Google BigQuery
* Heroku with Postgres and Data Pipeline



[Conclusion].
