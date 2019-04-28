---
layout: post
title:  "Python for Finance:  Robo Advisor Edition"
date:   2019-04-06 12:00:00 -0500
categories: 
---

## Extending Stock Portfolio Analyses and Dash by Plotly to track Robo Advisor-like Portfolios.

<img src="/assets/aditya-vyas-783075-unsplash.jpg" alt="Wall St Stock Exchange" height="500"  style="width: 100%"> 

Photo by Aditya Vyas on Unsplash.

## Part 3 of Leveraging Python for Stock Portfolio Analyses.

### Introduction.
This post is the third installment in my series on leveraging ``Python`` for finance, specifically stock portfolio analyses.  In <a href="https://towardsdatascience.com/python-for-finance-stock-portfolio-analyses-6da4c3e61054" target="_blank">part 1</a>, I reviewed a Jupyter notebook with all of the code needed to extract financial time series data from the Yahoo Finance API and create a rich dataframe for analyzing portfolio performance across individual tickers.  The code also included a review of some key portfolio metrics with several visualizations created using the ``Plotly`` library.  In <a href="https://towardsdatascience.com/python-for-finance-dash-by-plotly-ccf84045b8be" target="_blank">part 2</a>, I extended Part 1's analyses and visualizations by providing the code needed to take the data sets generated and visualize them in a ``Dash by Plotly`` (``Dash``) web app.  

In this series continuation, I will provide an overview of Robo Advisors and then share additional code and details on how to evaluate a diversified index strategy.  This strategy can be used for several personal finance use cases, including as part of a holistic approach that combines ETFs with individual stocks and bonds.  It could also be used to evaluate the efficacy of a Robo Advisor alongside a personally managed ETF strategy.  

Finally, one of the largest limitations from my initial approach was that the analyses did not account for dividends and compare <a href="https://www.investopedia.com/terms/t/tsr.asp" target="_blank">total shareholder return</a>.  Total shareholder return is now incorporated -- in my view, this is one of the largest gaps I've seen in retail investor personal portfolio apps.  It is extremely difficult to get an all-up view of portfolio performance, including investment timings and earned dividends.  My approach now accounts for both of these, which was a personal pain point that led me to solve this with my own product.  I will continue to evolve this portfolio performance web app; and I'll share future updates to see if there is a potential market for this approach as a consumer-facing app.     

### Overview of Robo Advisors.
Per <a href="https://www.nerdwallet.com/blog/investing/best-robo-advisors/" target="_blank">NerdWallet</a>, a robo-advisor is "an online, automated portfolio management service".  Robo Advisors use algorithms, which are based on rules that the individual user inputs and drive investment selection for the individual based on her risk tolerance and investment horizon (aka, time to retirement and/or financial objectives).  Robo Advisors offer much lower costs than traditional human financial advisory, with the tradeoff being that you generally do not have anyone to personally consult with regarding your financial objectives.  Robo Advisors are typically best suited for passive investors, who are comfortable with someone else building and optimizing a personal portfolio, and who also do not have complex financial situations.

Some of the major and most well known Robo Advisors include Wealthfront, SoFi and Betterment.  Personal Capital is another option in this space, although the company does not believe it should be classified as a Robo Advisor -- this is due to the fact that Personal Capital combines a sophisticated budgeting and portfolio monitoring application with virtual human financial advisors.  Personal Capital markets itself as a financial technology platform that can also advise higher net worth individuals and families who have more complicated financial situations.  

In this post, we will leverage a diversified ETF example that Personal Capital provides on its <a href="https://www.personalcapital.com/wealth-management/performance" target="_blank">Wealth Management performance page</a>.  I believe this is informative because I respect Personal Capital's approach, they're very transparent with their performance relative to benchmarks, and in my view the representative ETFs in the footnotes could be used to construct a sound investment strategy.

### Passive versus Active Investment Strategies.
Over the years since I initially started investing, **I've focused more and more on making my investing strategy as boring as possible**.  This means that I've subscribed to more of a passive investment strategy and I acknowledge that attempting to time the market is nearly impossible.  In Part 1 of this series, I noted that over the long-term 1 in 20 actively managed domestic funds beat index funds (<a href="https://www.marketwatch.com/story/why-way-fewer-actively-managed-funds-beat-the-sp-than-we-thought-2017-04-24" target="_blank">link</a>).  Outperformance over a prolonged period is very difficult to maintain and previous outperformers tend to revert to the mean of benchmark performance over the long term.  Further emphasizing this point, it was recently announced that, for the 9th year in a row, <a href="https://www.cnbc.com/2019/03/15/active-fund-managers-trail-the-sp-500-for-the-ninth-year-in-a-row-in-triumph-for-indexing.html" target="_blank">active fund managers trailed the S&P 500</a>.  Active managers, who previously claimed they would do better during periods of increased volatility, will have to go back to the drawing board once again.

Given this, I now focus a majority of my assets in a diversified ETF strategy -- my core strategy employs high quality ETFs that have a very low cost structure and provide diversification across asset classes.  These include US and international equities, investment grade bonds, commodities, gold and real estate.  While I prefer that my investment strategy is as boring as possible, I continue to also invest in individual stocks that meet several investment criteria, including accelerating revenue growth, earnings outperformance and, ideally, the development of products that I personally love.  Part 1 and Part 2 of this series cover in detail how to track individual stock performance relative to the S&P 500, which is similar to how we'll evaluate a diversified ETF strategy in this post.    

### Part 3 Code Implementation.
**Setup.**  Similar to Parts 1 and 2, I created <a href="https://github.com/kdboller/pythonsp500-robo-advisor-edition" target="_blank">a repo on GitHub </a>with all files and code required to create the final ``Dash`` dashboard.  For this post, I will explain the following aspects of the code:

1. Target allocation for ETFs relative to current allocation.
1. Adding earned dividends to each position, and the benchmark, in order to calculate total shareholder return.
1. Evaluating total shareholder return for the toy portfolio relative to a single benchmark, in this case the S&P 500.

The Jupyter notebook in the repo for this post has all the code needed from start to finish, but if you would like the full explanation on generating the portfolio data set, please refer to <a href="https://towardsdatascience.com/python-for-finance-stock-portfolio-analyses-6da4c3e61054" target="_blank">part 1</a>.  If you would like more detail on working with Anaconda, virtual environments, and working with Dash, please see the **Getting Started** section in <a href="https://towardsdatascience.com/python-for-finance-dash-by-plotly-ccf84045b8be" target="_blank">part 2</a>.

As discussed at the end of Part 2, the limitations to the previous approach were i) it did not account for dividends, ii) it evaluated active positions and did not include previously divested ones, and iii) there were opportunities to automate the overall process by generating data pipelines that could feed into a live web application.

In my view, not including dividends and evaluating total shareholder return (TSR) was the largest gap; and this updated approach now evaluates TSR.  I'm less concerned with divested positions, because this evaluation is most useful for evaluating how well your strategy is performing and if there are positions you continue to hold that you probably should not, e.g., lagging benchmark and therefore representing both overall performance drag and opportunity cost from holding a better investment.  While I would like to fully automate this process, I've de-prioritized that in favor of refining my overall strategy.  If I do decide to pursue a fully automated approach, I may or may not write a detailed post about that automation.

**Target Allocation.**
For the code discussion, we'll begin with the Jupyter notebook - an interactive version can be found <a href="https://towardsdatascience.com/python-for-finance-stock-portfolio-analyses-6da4c3e61054" target="_blank">here</a>.  If you would like details on the dataframe development and closing high evaluation, please review <a href="https://towardsdatascience.com/python-for-finance-stock-portfolio-analyses-6da4c3e61054" target="_blank">part 1</a>.  Below I'll highlight the primary addition to the dataframe development, which is understanding and comparing target allocation versus actual allocation.  In our model portfolio, we would like to have 50% of our investment allocated to VTI, which is a total stock index ETF for US equities.  As prices change post investment, our allocation will shift away from 50% based on the movement of this asset, as well as the other assets in our model portfolio.  For that reason, we should monitor this movement and adjust the assets held in order to get back to our target allocation.  For example, if VTI increases above 50% and VEU dips below 25%, then we should sell down some of VTI and/or purchase more of VEU to get back to our targets.  The below starts on line 32 and stops on line 36 in the notebook.

```python
# This dataframe will only look at the positions with an intended contribution, if applicable.

merged_portfolio_sp_latest_YTD_sp_contr = merged_portfolio_sp_latest_YTD_sp[merged_portfolio_sp_latest_YTD_sp['Target_Alloc']>0]

merged_portfolio_sp_latest_YTD_sp_contr

# Shorten dataframe to focus on columns that will be used to look at intended versus current allocations.

merged_portfolio_sp_latest_YTD_sp_contr_subset = merged_portfolio_sp_latest_YTD_sp_contr[['Ticker', 'Target_Alloc', 'Cost Basis', 'Ticker Share Value']]

merged_portfolio_sp_latest_YTD_sp_contr_subset

# If you've bought multiple positions at different times, this pivot table will aggregate the sums for each position.

merged_portfolio_sp_latest_YTD_sp_contr_subset_pivot = merged_portfolio_sp_latest_YTD_sp_contr_subset.pivot_table(
    index=['Ticker', 'Target_Alloc'], values='Ticker Share Value', aggfunc='sum')

merged_portfolio_sp_latest_YTD_sp_contr_subset_pivot.reset_index(inplace=True)

merged_portfolio_sp_latest_YTD_sp_contr_subset_pivot

# These new columns calculate the actual allocation to compare to the target allocation.

merged_portfolio_sp_latest_YTD_sp_contr_subset_pivot['Total'] = merged_portfolio_sp_latest_YTD_sp_contr_subset_pivot.loc[:, 'Ticker Share Value'].cumsum()

merged_portfolio_sp_latest_YTD_sp_contr_subset_pivot['Allocation'] = merged_portfolio_sp_latest_YTD_sp_contr_subset_pivot['Ticker Share Value'] / merged_portfolio_sp_latest_YTD_sp_contr_subset_pivot.iloc[-1, -1]

merged_portfolio_sp_latest_YTD_sp_contr_subset_pivot

merged_portfolio_sp_latest_YTD_sp_contr_subset_pivot.sort_values(by='Target_Alloc', ascending=False, inplace=True)

merged_portfolio_sp_latest_YTD_sp_contr_subset_pivot
```

* In the file we read in, we look at all positions that we have noted with have a Target Allocation; this provides flexibility in the event you want to track positions but are not actively investing in them while evaluating.
* We subset the dataframe, and then use the pivot_table method to aggregate total market value of holding.  As noted in the code, we run this pivot due to the fact that, over several years, you'll invest in the positions in this model portfolio a number of different times - this pivot lets you look at your all-up allocation given current market prices for each, and as the allocation evolves over time.
* We then sum up each position's total market value (Ticker Share Value) and divide it by the total market value of the portfolio; this allows you to compare current allocation, based on market price changes, relative to your target allocations. 

**Total Shareholder Return.**
Above line 54 in the notebook, you'll see a Dividends section.  Here I've gathered dividend data for each position and you'll see the URLs for the sites where you can gather the dividend information.  Here, I'll be self-critical in that this section of the code has some room for improvement.  I've investigated accessing Quandl's API to automate dividend information, but decided to not pay for a subscription.  I'm also looking into developing a scraper for these sites; but for now I'm copying/pasting data from the sites into the Historical Dividends excel file.  This is generally fine as dividends tend to be paid quarterly and model portfolio has 7 total positions, but I definitely welcome suggestions on how to improve this section of the code.  Note, however you decide to aggregate dividend data, you should make sure that you only account for dividends where your acquisition date of the position is <= to the Ex-Div Date (see function, from line 60, shown as the first code block below).  

```python 
# This function determines if you owned the stock and were eligible to be paid the dividend.

def dividend_post_acquisition(df):
    if df['Ex-Div. Date'] > df['Acquisition Date'] and df['Ex-Div. Date'] <= stocks_end:
        val = 1
    elif df['Ex-Div. Date'] <= df['Acquisition Date']:
        val = 0
    else:
        val = 0
    return val
```

```python

# subset the df with the needed columns that includes total dividends received for each position.

merged_subsets_eligible_total = merged_subsets_eligible.pivot_table(index=['Ticker #', 'Ticker', 'Acquisition Date', 'Quantity'
                                                                           , 'Latest Date', 'Equiv SP Shares']
                                                                          , values='Dividend Amt', aggfunc=sum)

merged_subsets_eligible_total.reset_index(inplace=True)

merged_subsets_eligible_total

```

* Once you have created the eligible dividends dataframe, based on the ex-div dates for the stock since you've held it, the above code aggregates the total dividends received for each and also includes the Equiv SP Shares column; this is needed to compare each position's dividends received relative to what an equal SP500 investment returned.

```python

# This df adds all of the columns with the SP500 dividends paid during the range that each stock position was held.
# For comparative holding period purposes.

dividend_df_sp500_2 = dividend_df_sp500

agg0_start_date = datetime.datetime(2014, 4, 21)
dbc1_start_date = datetime.datetime(2014, 4, 21)
igov3_start_date = datetime.datetime(2014, 4, 21)
veu4_start_date = datetime.datetime(2014, 4, 21)
vnq5_start_date = datetime.datetime(2014, 4, 21)
vti6_start_date = datetime.datetime(2014, 4, 21)
vti7_start_date = datetime.datetime(2014, 5, 5)

dividend_df_sp500_2.loc[:, 'agg0_sum'] = dividend_df_sp500_2[(dividend_df_sp500_2['Ex-Div. Date'] > agg0_start_date) & (dividend_df_sp500_2['Ex-Div. Date'] <= stocks_end)].sum()['Amount']
dividend_df_sp500_2.loc[:, 'dbc1_sum'] = dividend_df_sp500_2[(dividend_df_sp500_2['Ex-Div. Date'] > dbc1_start_date) & (dividend_df_sp500_2['Ex-Div. Date'] <= stocks_end)].sum()['Amount']
dividend_df_sp500_2.loc[:, 'igov3_sum'] = dividend_df_sp500_2[(dividend_df_sp500_2['Ex-Div. Date'] > igov3_start_date) & (dividend_df_sp500_2['Ex-Div. Date'] <= stocks_end)].sum()['Amount']
dividend_df_sp500_2.loc[:, 'veu4_sum'] = dividend_df_sp500_2[(dividend_df_sp500_2['Ex-Div. Date'] > veu4_start_date) & (dividend_df_sp500_2['Ex-Div. Date'] <= stocks_end)].sum()['Amount']
dividend_df_sp500_2.loc[:, 'vnq5_sum'] = dividend_df_sp500_2[(dividend_df_sp500_2['Ex-Div. Date'] > vnq5_start_date) & (dividend_df_sp500_2['Ex-Div. Date'] <= stocks_end)].sum()['Amount']
dividend_df_sp500_2.loc[:, 'vti6_sum'] = dividend_df_sp500_2[(dividend_df_sp500_2['Ex-Div. Date'] > vti6_start_date) & (dividend_df_sp500_2['Ex-Div. Date'] <= stocks_end)].sum()['Amount']
dividend_df_sp500_2.loc[:, 'vti7_sum'] = dividend_df_sp500_2[(dividend_df_sp500_2['Ex-Div. Date'] > vti7_start_date) & (dividend_df_sp500_2['Ex-Div. Date'] <= stocks_end)].sum()['Amount']

dividend_df_sp500_2.head()

# Subset the above df and re-label the SP500 total dividend amount column.

dividend_df_sp500_2 = dividend_df_sp500_2.iloc[0, 10:]

dividend_df_sp500_2 = dividend_df_sp500_2.to_frame().reset_index()

dividend_df_sp500_2.rename(columns={213: 'SP500 Div Amt'}, inplace=True)

dividend_df_sp500_2

# This function is used to assign the Ticker # column so that this df can be joined with the master df.

def ticker_assigner(df):
    if df['index'] == 'agg0_sum':
        val = 'AGG 0'
    elif df['index'] == 'dbc1_sum':
        val = 'DBC 1'
    elif df['index'] == 'igov3_sum':
        val = 'IGOV 3'
    elif df['index'] == 'veu4_sum':
        val = 'VEU 4'
    elif df['index'] == 'vnq5_sum':
        val = 'VNQ 5'
    elif df['index'] == 'vti6_sum':
        val = 'VTI 6'
    elif df['index'] == 'vti7_sum':
        val = 'VTI 7'
    else:
        val = 0
    return val

```
**The above code is the least elegant and in most need of improvement, but it gets the job done for the time being.**

* In the first code block (line 68), you set a variable for each position based on each position's acquisition date. 
* You then create a new column that sums the dividends paid for the SP500 during an equivalent holding period as each position.
* In the next code block, you grab the first row and column 11 and after, .iloc[0, 10:]. This removes the duplication from the inelegant solution for grabbing the SP500 dividend for each position.
* In the last code block above, you're assigning the sum of the SP500 dividends to each relevant position, in order to calculate TSR for each holding.  For example, agg0_sum tracks the sum of all SP500 dividends since you held your first AGG investment.  You're assigning this to the 'AGG 0' row in your master dataframe.

In line 74, you'll see some familiar calculations, as well as some new ones, in order to create the key metrics we'll compare for each position relative to the SP500.

* SP500 Tot Div - this takes the total SP500 dividend amount and multiplies it by the number of shares you could have purchased in the SP500 for the dollars you instead invested in each position.
* There are total Gain / (Loss) columns added that sum the gain or loss from each position, aka the percent a stock went up or down since purchase, with the total dividends received since you bought the position.  These metrics therefore allow you to calculate TSR for both your individual positions and comparable SP500 holdings.
* As always, your returns are determined by dividing the value of the holding by its original cost basis.
* Similar to that seen in parts 1 and 2, we calculate cumulative returns in order to look at, in addition to individual performance, the performance of our total portfolio return relative to the SP500 benchmark.

### Brief Observations for Dashboard Outputs.
<img src="/assets/robo_advisor_percent allocation.png" alt="Percent Allocation" height="500"  style="width: 100%">
* In the visualization above, you can see your current allocation for each position in this model portfolio relative to your target allocation.
* These positions have all been held since April 2014, and VTI has returned around 70% during that time (thru 4/18/2019).
* Since VTI has returned more than other positions, it now represents nearly 60% of your portfolio -- this is where portfolio re-balancing comes in.  To keep the same amount invested in the portfolio, you would want to sell down some of VTI and use the proceeds to purchase the other positions, in order to get back to your target allocation.
* The benefit of robo-advisors such as Betterment and Wealthfront, is that they'll automatically re-balance for you. The caveat is that there are obviously fees you incur for them to perform this service, while the robo-advisors may save you on transaction costs associated with making these trades. 

<img src="/assets/robo_advisor_tsr by ticker and tsr pct overall.png" alt="Percent Allocation" height="500"  style="width: 100%">


### Conclusion.
[Placeholder]

If you enjoyed this post, it would be awesome if you would click the "claps" icon to let me know and to help increase circulation of my work.

Feel free to also reach out to me on twitter, <a href="https://twitter.com/kevinboller" target="_blank">@kevinboller</a>, and my personal blog can be found <a href="https://kdboller.github.io/" target="_blank">here</a>.  Thanks for reading!

Outline.

1. Intro [**draft complete**] -- this is the third installment of a series on how to leverage ``Python``, ``pandas``, ``Dash`` and financial data APIs in order to automate personal portfolio tracking.

1. Overview Robo Advisor [**draft complete**]; i) passive versus active investing. ii) who are the main Robo Advisors; iii) how you can decently replicate their strategies bsaed on what's provided in this post.

1. Why Implement a Passive Investment Strategy [**draft complete**].  Recent data points:  https://www.cnbc.com/2019/03/15/active-fund-managers-trail-the-sp-500-for-the-ninth-year-in-a-row-in-triumph-for-indexing.html; active fund managers trail; Bogle's recent book and quote on 'top decile returns when you invest in index funds'; Howard Marks book on where we are at in the credit cycle. 

1. Limitations from prior time and how they've been addressed [**draft complete**].; the limitations from prior time included i) not including dividends and total shareholder return (addressed here); ii) not looking at divested positions (to be decided how I'll handle); iii) automate data pipelines to feed a live web dashboard (de-prioritized in order to focus on the right overall investment strategy).

1. Code -- only need to highlight the additions, which are focused on pulling in dividends, allocation comparison, comparing total shareholder return and then rolling up total return versus benchmark.

1. Conclusion -- I've not found a service out there that replicates this type of analysis, which I believe is imperative to make sure you're properly investing your money -- just tells you absolute portfolio return, doesn't effectively compare to benchmarks, and does not show total shareholder return.  A robo-advisor can do this for you, but every dollar you invest is subject to their fee structure, versus your time.  Still have a strategy that focuses on stocks with accelerating revenue growth and are industry leaders in high growth industries; for long-term portfolio strategy, believe a robo advisor / gone fishing is very sensible approach as part of an overall holistic strategy.  


