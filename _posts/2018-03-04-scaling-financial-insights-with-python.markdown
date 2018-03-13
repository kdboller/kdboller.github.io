---
layout: post
title:  "Scaling Financial Insights with Python"
date:   2018-03-04 12:00:00 -0500
categories: 
---

<img src="/assets/Python_Finance_hero.jpg" alt="Python Finance" height="500"  style="width: 100%">

<strong>As of 3/4, 2018, this post is currently in process.</strong>

<p>My two most recent blog posts were about Scaling Analytical Insights with Python; part 1 can be found <a href="https://kdboller.github.io/2017/07/09/scaling-analytical-insights-with-python.html" target="_blank">here</a> and part 2 can be found <a href="https://kdboller.github.io/2017/10/11/scaling-analytical-insights-with-python_part2.html" target="_blank">here</a>.  It has been several months since I wrote those, largely due to the fact that I relocated my family to Seattle to join Amazon in November; the general consensus that Amazon presents a significant learning curve proved to be true in my situation and I spent most of the time on my primary project determining our global rollout plan and related business intelligence roadmap. </p> 

<p>At my former company, FloSports, prior to my departure we were in the process of overhauling our analytics reporting across the organization (data, marketing, product et al), and part of this overhaul included our financial reporting.  While I left prior to us getting too far along in that implementation, over the past several months I’ve continued using Python extensively, particularly pandas.  In this post, I will share how I leveraged some very helpful online resources, the Yahoo Finance API (which requires a work around and may require a future replacement), and Jupyter notebook in order to build a Python notebook for my stock portfolio.  This approach allows me to almost completely automate the tracking of my individual ticker and overall personal stock portfolio performance, as well compare relative performance to the S&P 500 at the individual position level.</p>

<h2>Overview of PME and benchmarking individual stock performance</h2>

<p>As a quick background, I have been investing in my own stock portfolio since 2002.  I have used several brokers over the years and developed an overall financial model for my portfolio a number of years ago.  Each week I export stock prices from my broker and load the data into the financial model -- while my broker calculates all returns, income and dividends, I generally like to have this data in the model as I conduct my own analysis and determine if there are positions I should sell (“cut losses early and let winners run”).  One view which I’ve not yet seen from any of these brokers is how to create a <a href="https://en.wikipedia.org/wiki/Public_Market_Equivalent" target="_blank">“Public Market Equivalent”</a>-like analysis.  In short, the Public Market Equivalent (PME) is a set of analyses used in the private equity industry to compare the performance of a private equity fund relative to an industry benchmark.  Much more detail <a href="http://docs.preqin.com/reports/Preqin-Special-Report-PME-July-2015.pdf" target="_blank">here.</a>  </p>

<p>The vast majority of portfolio managers are unable to select a portfolio of stocks which outperform the broader market, e.g., S&P 500.  Even when some individual stocks outperform, the underperformance of others can outweigh the better performing stocks, meaning overall the investor is worse off than simply investing in an index fund.  During business school I learned about PME, and I incorporated a conceptually similar analysis into the evaluation of my current portfolio holdings.  To do this properly, you should measure the timing of investment inflows specific to each portfolio position (holding periods) relative to an S&P 500 equivalent dollar investment over the identical time period.  As an example, if you bought a stock on 6/1/2016 and you still own it, you would want to compare an equal dollar investment on 6/1/2016 of the S&P 500 and compare the stock’s return to the S&P 500 equivalent return.  This will tell you, among other things, that even if a stock has done relatively well it may still trail the S&P 500's return over that time period.</p>
    
<p>In the past, I have downloaded historical prices data from Yahoo Finance and used an INDEX and MATCH function combination in excel to calculate the relative performance of each position versus the S&P 500.  While this is an OK way to accomplish this goal, conducting the same in Python is much more scalable and flexible.  Whenever you download new data and load into excel, you inevitably need to modify some formulas and validate for errors.  Given the recent market volatility, I’m very glad that I switched to the Python approach, as re-running this every Saturday morning is fairly trivial; before using excel I only did this once every month or two.  The additional benefits are adding new calculations, such as cumulative ROI multiple (which I’ll cover), take about 30 seconds.  And the visualizations, which I use Plotly for, are highly reproducible and very useful in generating insights.</p>

<p><strong>Disclosure:</strong>  <i>Nothing in this post should be considered investment advice.  Past performance is not necessarily indicative of future returns.  These are general examples about how to download data for a small sample of stocks across different time intervals and benchmark their performance against an index.  You should direct all investment related questions that you have to your financial advisor.</i></p>

<p>Also, I am not an expert on this topic and I outline some limitations as well as future areas for development at the end of this post.  However, I believe this approach is rather helpful, particularly for novice to intermediate-level professionals, especially since this approach and the visualizations extend to other types of financial analyses.  <strong>This approach is “PME-like” in the sense that’s it’s measuring inflows over equal holding periods.  As public market investments are much more liquid than private equity, and presuming you follow a trailing stop approach, from my perspective it’s more important to focus on active holdings -- it's generally advisable to divest holdings which underperform a benchmark or which you no longer want to own for various reasons, while I take a long-term view and am happy to own outperforming stocks for as long as they’ll have me.</strong></p>

<p>Resources:
    <ul>
    <li>I am a current DataCamp subscriber (future post forthcoming on DataCamp) and <a href="https://www.datacamp.com/community/tutorials/finance-python-trading" target="_blank">this community tutorial</a> on Python for Finance is great.</li>
    <li>I have created <a href="https://github.com/kdboller/pythonsp500" target="_blank">a repo for this post</a> including the Python notebook <a href="https://github.com/kdboller/pythonsp500/blob/master/Investment%20Portfolio%20Python%20Notebook_03_2018_blog%20example.ipynb" target="_blank">here</a>, and the excel file <a href="https://github.com/kdboller/pythonsp500/blob/master/Sample%20stocks%20acquisition%20dates_costs.xlsx" target="_blank">here.</a></li>
    <li>If you want to see the full interactive version (because Jupyter <<-->> Github integration is awesome), you can view using nbviewer <a href="http://nbviewer.jupyter.org/github/kdboller/pythonsp500/blob/320e49404e18ec5c1978ed793d58bfc0ae344cf3/Investment%20Portfolio%20Python%20Notebook_03_2018_blog%20example.ipynb" target="_blank">here.</a></li>
  </ul>
  <p>Outline of what we want to accomplish:
  <ul>
    <li>Import S&P 500 and sample ticker data, using the Yahoo Finance API</li>
    <li>Create a merged portfolio file which combines the sample portfolio dataframe with the historical ticker and historical S&P 500 data</li>
    <li>Determine what the S&P 500 close was on the date of acquisition of each investment, which allows us to calculate the S&P 500 equivalent share position with the same dollars invested</li>
    <li>Calculate the relative % and value returns for the portfolio positions over time, compared to the S&P 500 returns over that time</li>
    <li>Calculate cumulative investment returns and ROI multiple, in order to assess how well this example portfolio compared to a market index</li>
    <li>One of the most important items:  dynamically calculate how each position is doing relative to a trailing stop, e.g., if a position closes 25% below it’s closing high, sell the position on the next trading day.</li>
    <li>Visualizations</li>
    <ul>
      <li>YTD and Trailing Stop Charts -- how is relative performance YTD and is the stock in violation of trailing stop investing rules?</li>
      <li>Total Return Comparisons -- % return of each position relative to index benchmark</li>
      <li>Cumulative Returns Over Time -- $ Gain / (Loss) of each position relative to benchmark</li>
      <li>Cumulative Investments Over Time -- given the above, how do the overall investment returns compare to the equal weighting and time period of S&P 500 investments?</li>
    </ul>
  </ul></p>
  </p>

<h2>Investment Portfolio Python Notebook</h2>

<h3>Data Import and Dataframe Manipulation</h3>

We will begin by importing the necessary Python libraries, import Plotly's offline module, and read in our sample portfolio dataframe, which, as mentioned previously, can be found here.

```python
# Import initial libraries

import pandas as pd
import numpy as np
import datetime
import matplotlib.pyplot as plt
import plotly.graph_objs as go
%matplotlib inline

# Imports in order to be able to use Plotly offline.
from plotly import __version__
from plotly.offline import download_plotlyjs, init_notebook_mode, plot, iplot

print(__version__) # requires version >= 1.9.0

init_notebook_mode(connected=True)

# Import the Sample worksheet with acquisition dates and initial cost basis:

portfolio_df = pd.read_excel('Sample stocks acquisition dates_costs.xlsx', sheetname='Sample')

portfolio_df.head(10)
```

Now that we have read in our sample portfolio file, we'll create a few variables which capture the date ranges for the S&P 500 and all of the tickers in our sample file.  Note that this is one of the few aspects of this notebook which requires an update each week (adjust the date range to include the most recent trading week).  

```python
# Date Ranges for SP 500 and for all tickers
# Modify these date ranges each week.

# The below will pull back stock prices from the start date until end date specified.
start_sp = datetime.datetime(2013, 1, 1)
end_sp = datetime.datetime(2018, 3, 9)

# This variable is used for YTD performance.
end_of_last_year = datetime.datetime(2017, 12, 29)

# These are separate if for some reason want different date range than SP.
stocks_start = datetime.datetime(2013, 1, 1)
stocks_end = datetime.datetime(2018, 3, 9)
```

As mentioned in the Python Finance training post, the pandas-datareader package enables us to read in data from sources like Google, Yahoo! Finance and the World Bank, among others.  In this post, I'll focus on Yahoo! Finance, although I've worked very preliminarily in Quantopian and have also begun looking into quandl as a data source.  As also mentioned in the DataCamp post, the Yahoo API endpoint recently changed and this requires the installation of a temporary fix in order for Yahoo! Finance to work.  I've made this slight adjustment in the code below, as noted.  I have noticed some minor data issues where the data does not always read in when hitting the endpoint, or the last trading day is sometimes missing.  While these issues have been infrequent, I'm continuing to monitor whether or not Yahoo! is the best and most reliable data source.

```python
# Leveraged from the helpful Datacamp Python Finance trading blog post.

from pandas_datareader import data as pdr
import fix_yahoo_finance as yf
yf.pdr_override() # <== that's all it takes :-)

sp500 = pdr.get_data_yahoo('^GSPC', 
                           start_sp,
                             end_sp)
    
sp500.head()
```

If you're following along with your own notebook, you should see something like the below once you've successfully read in the data from Yahoo's API:

<img src="/assets/Yahoo Finance_SP500 dataframe head.png" alt="S&P 500 Initial Import">
<!-- height="200"  style="width: 100%" -->

After loading in the S&P 500 data, you'll see that I inspect the head and tail of the dataframe, as well as condense the dataframe to only include the Adj Close column.  The difference between the adjusted close and the close column is that adjusted close reflects dividends.  When a company issues a dividend, the stock price will adjust down by the size of the dividend per share, as the company is distributing a portion of the company's earnings.  For purposes of this analysis, we will only need to analyze this column.  I also create a dataframe which only includes the S&P's adjusted close on the last day of 2017 (start of 2018); this is in order to run YTD comparisons of individual tickers relative to the S&P 500's performance.


In the below code, we create an array of all of the tickers in our sample portfolio dataframe, and then write a function to read in all of the tickers and their relevant data into a new dataframe (this is the same approach we took for the S&P500), but it is applied to all of the tickers.

```python
# Generate a dynamic list of tickers to pull from Yahoo Finance API based on the imported file with tickers.
tickers = portfolio_df['Ticker'].unique()
tickers

# Stock comparison code

def get(tickers, startdate, enddate):
    def data(ticker):
        return (pdr.get_data_yahoo(ticker, start=startdate, end=enddate))
    datas = map(data, tickers)
    return(pd.concat(datas, keys=tickers, names=['Ticker', 'Date']))
               
all_data = get(tickers, stocks_start, stocks_end)

```

As with the S&P 500 dataframe, we'll create an adj_close dataframe which only has the Adj Close column for all of our stock tickers.  If you look at the notebook in the repo I link to above, this code is chunked out in more code blocks, but for purposes of describing this here, I've included below all of the code which leads up to our initial merged_portfolio dataframe.

```python
# Also only pulling the ticker, date and adj. close columns for our tickers.

adj_close = all_data[['Adj Close']].reset_index()
adj_close.head()

# Grabbing the ticker close from the end of last year
adj_close_start = adj_close[adj_close['Date']==end_of_last_year]
adj_close_start.head()

# Grab the latest stock close price

adj_close_latest = adj_close[adj_close['Date']==stocks_end]
adj_close_latest

adj_close_latest.set_index('Ticker', inplace=True)
adj_close_latest.head()

# Set portfolio index prior to merging with the adj close latest.
portfolio_df.set_index(['Ticker'], inplace=True)

portfolio_df.head()

# Merge the portfolio dataframe with the adj close dataframe; they are being joined by their indexes.

merged_portfolio = pd.merge(portfolio_df, adj_close_latest, left_index=True, right_index=True)
merged_portfolio.head()

# The below creates a new column which is the ticker return; takes the latest adjusted close for each position
# and divides that by the initial share cost.

merged_portfolio['ticker return'] = merged_portfolio['Adj Close'] / merged_portfolio['Unit Cost'] - 1

merged_portfolio

```

<img src="/assets/Merged portfolio initial returns.png" alt="Merged Portfolio Initial Returns">

Depending on your level of familiarity with Python, this will be very straightforward to slightly overwhelming.  Below, I'll unpack what these lines are doing:

<ul>
<li>The overall approach we are taking is an example of split-apply-combine.  A helpful overview of this can be found here.</li>
<li>The all_data[['Adj Close']] line creates a new <u>dataframe</u> with only the columns provided in the list; here Adj Close is the only item provided in the list.</li>
<li>Using this line of code, adj_close[adj_close['Date']==end_of_last_year], we rae filtering the adj_close dataframe to only the row where the data's Date column equals the date which we earlier specified in the end_of_last_year variable.</li>
<li>We also set the index of the adj_close_latest and portfolio_df dataframes.  I did this because this is how we'll merge the two dataframes.  The merge function, very similar to SQL joins, is an extremely useful function which I use very often.</li>
<li>Within the merge function, we specify our left dataframe (portfolio_df) and our right dataframe (adj_close_latest).  By specifying left_index and right_index True, we are stating that the two dataframes share a common index and we will join both on this.</li>
<li>Last, we create a new column called 'ticker return'.  This calculates the percent return by dividing the Adj Close by the Unit Cost (initial purchase price for stock) and subtracting 1.  This is similar to calculating a formula in excel and carrying it down, but in pandas this is accomplished with one-line of code.</li>
</ul>












