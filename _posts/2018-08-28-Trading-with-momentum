---
layout: post
title: Classic Machine Learning Algorithm
tags: 
  - Quantitative Trading
lang: en
mathjax: true
mathjax_autoNumber: true
chart: true
---
# Trading with momentum

#### **Step 1: Resample data according to sampling frequency (e.g. daily, monthly, yearly)**

E.g. the raw data is provided on daily basis for each ticker (i.e. stock) and date (i.e. trading day), so to conduct analysis on monthly basis, the data should be resample to use month-end prices.

Tools:

- [pandas.DataFrame.resample](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.resample.html)

#### **Step 2: Compute log returns**

$$R_t = \log_e (P_t) - \log_e (P_{t-1})$$

**Why log returns**
1. Log returns can be interpreted as continuously compounded returns (i.e. compounding infinitely).
2. Log returns are time-additive.The multi-period log return is simply the sum of single period log returns.
3. The use of log returns prevents security prices from becoming negative in models of security returns.
4. For many purposes, log returns of a security can be reasonably modeled as distributed according to a normal distribution.
5. When returns and log returns are small (their absolute values are much less than 1), their values are approximately equal.
6. Logarithms can help make an algorithm more numerically stable.

**Distribution of log returns**

So long-term prices and cumulative returns can be modeled as approximately log-normally distributed because they are *products* of independently, identically distributed (IID) random variables. On the other hand, log returns sum over time. Therefore, if $R_1 = \ln\left(\frac{p_1}{p_0}\right)$ and $R_2 = \ln\left(\frac{p_2}{p_1}\right)$ are normal, their sum, the two-period log return, is also normal. Even if they are not normal, as long as they are IID, their long-term sum will be approximately normal, thanks to the Central Limit Theorem. This is one reason why using log returns can be convenient for modeling purposes.

Tools:

- [numpy.log](https://docs.scipy.org/doc/numpy/reference/generated/numpy.log.html)
- [pandas.DataFrame.shift](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.shift.html)

#### **Step 3: Shift the computed log returns**

Shift the log returns to the previous or future returns in the time series

#### **Step 4: Generate trading signal**

For each period, rank all the stocks by previous returns in descending order. Then, "long" (i.e. buy) the top performers and "short" (i.e. sell) the bottom performers in portfolio. 

Tools:

- [pandas.DataFrame.iterrows](https://pandas.pydata.org/pandas-docs/version/0.21/generated/pandas.DataFrame.iterrows.html)
- [pandas.Series.nlargest](https://pandas.pydata.org/pandas-docs/version/0.21/generated/pandas.Series.nlargest.html)

#### **Step 5: Check projected returns**

Compute the potential net returns for each stock in the portfolio:

$$Net\ returns  = Long\ Equity\ Returns - Short\ Equity\ Returns$$

[**Long-short strategy** ](https://www.barclayhedge.com/research/educational-articles/hedge-fund-strategy-definition/hedge-fund-strategy-equity-long-short.html)

> An equity long-short strategy is an investing strategy, used primarily by hedge funds, that involves taking long positions in stocks that are expected to increase in value and short positions in stocks that are expected to decrease in value.

> You may know that taking a long position in a stock simply means buying it: If the stock increases in value, you will make money. On the other hand, taking a short position in a stock means borrowing a stock you don’t own (usually from your broker), selling it, then hoping it declines in value, at which time you can buy it back at a lower price than you paid for it and return the borrowed shares.

#### **Step 6: Statistical test (t-test) for annualized rate of returns (of the portfolio)**

Firstly, sum the log returns for each date; secondly, compute the mean and the unbiased standard error for log returns of each date; finally, perform a t-test with the null hypothesis being that the expected mean return is zero.

Tools:

- [panda.DataFrame.sem](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.sem.html)
- [scipy.stats.ttest_1samp](https://docs.scipy.org/doc/scipy-1.0.0/reference/generated/scipy.stats.ttest_1samp.html)
