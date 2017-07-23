---
layout: post
title:  "Scaling Business and Operational Insights with Python"
date:   2017-07-09 12:00:00 -0500
categories: 
---

<!-- <img src="/assets/4_OKC_players_in_2011.jpg" alt="Kevin Durant with OKC Teammates" height="500"  style="width: 100%"> -->

<h1><strong>Please note that this post is still under development but a significant amount has now been completed.</strong></h1>

<p>
    In recent months, I’ve written about some of the critical undertakings and initiatives which I oversee as VP of Product at FloSports.  
  These have included my efforts to build a data informed culture, through product experimentation, our overall approach to our analytics tech stack, 
  and our approach to building and reviewing our rolling financial forecasts.
</p>

<p>
    I’ve also mentioned that the implementation of our data warehouse and the use of data analytics software, including Periscope Data, Segment, 
  and Mode Analytics have been fairly transformative across the company.  And, as business intelligence and data analysis requests and 
  feedback grow within an organization, it is critical to put processes and analytical procedures in place that reduce the queuing of data requests
  -- fast-paced and efficient approaches significantly reduce the time gathering the data and increase the level of insight derived from the data.
</p>

<p><i>In other words, spend less time calculating your LTV and more time focusing on efforts to grow your LTV. </i></p>

<p>
<strong><u>What I will cover in this post:</u></strong>
<ul>
  <li>Cohort retention analysis; I found this over a year ago on Greg Reda’s blog, and it was remarkably helpful</li>
    <ul><li>Taking this one step further and calculating weighted average retention</li>
    <li>This can be a single series fed directly into a model</li></ul>
  <li>The power of Mode Analytics, which combined SQL and Python in a single web application</li>
    <ul>
      <li>I use Jupyter Notebook for all analysis in Python</li>
      <li>Mode Analytics has a powerful offering for Python, which all exists within their overall reporting tool</li>
    </ul> 
  <li>The use of Python, in place of Excel, to conduct large scale analysis, which can ultimately live in a financial model</li>
      <ul><li>The best resource I’ve found for this to-date is Chris Moffit’s Practical Business Python blog</li>
      </ul>
</ul>
</p>

<strong><u>Cohort Retention Analysis with Python</u></strong>
<p>
Rather than reconstruct Greg Reda’s remarkably helpful post, I will simply continue from where he leaves off by showing how to calculate
M1, M2, etc. weighted average retention.

As mentioned in this guest post on Andrew Chen’s blog, Christoph Janz has written some of the most helpful posts on SaaS metrics and cohort analyses.
In the referenced post, one of the screenshots in Christoph’s post, from his model, shows the calculated weighted average retention by cohort month.
</p>

<p>
Here’s a screenshot of what this looks like:
<img src="/assets/ChristophJanz_CohortAnalysisNotes.png" alt="Illustrative Inputs Worksheet" height="500"  style="width: 100%">

</p>

<p>
If you would like to follow along with this explanation in Jupyter notebook, you will just need to use Greg Reda’s code from the post to
arrive at my starting point -- I’m starting after his last code snippet, which uses Seaborn and generates a heat map.
</p>


```python
# Unstack the TotalUsers
unstacked = cohorts['TotalUsers'].unstack(0)
unstacked.reset_index()
```
<p>This is a placeholder</p>

```python
# Create a weighted data frame with a reset index
weighted = unstacked.reset_index()

# Drop the Cohort Period from the dataframe to calculate the sums
weighted = weighted.drop('CohortPeriod', 1)

# Sum the users across all of the rows
total_users = weighted.sum(axis=1)

# Calculate percents by dividing each row by the row at index 0
pcts = total_users / total_users[0]

# Calculate weighted averge by creating a dataframe using a sum + percents dictionary key:value pairing.
weighted_average = pd.DataFrame(dict(total_users = total_users, pcts = pcts)).reset_index()

# Drop the index column out of the weighted average dataframe
weighted_average = weighted_average.drop('index', 1)

# Transpose the weighted average dataframe
weighted_average_transpose = weighted_average.transpose()
```

<p>The table attempt goes below.</p>

Header | Header | Header
-------|--------|-------
Cell   | Cell   | Cell
Cell   | Cell   | Cell


