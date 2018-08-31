---
layout: post
title: Breakout strategy
tags: 
  - Quantitative Trading
lang: en
mathjax: true
mathjax_autoNumber: true
chart: true
---
Smart beta has a broad meaning, but we can say in practice that when we use the universe of stocks from an index, and then apply some weighting scheme other than market cap weighting, it can be considered a type of smart beta fund. A Smart Beta portfolio generally gives investors exposure or "beta" to one or more types of market characteristics (or factors) that are believed to predict prices while giving investors a diversified broad exposure to a particular market. Smart Beta portfolios generally target momentum, earnings quality, low volatility, and dividends or some combination. Smart Beta Portfolios are generally rebalanced infrequently and follow relatively simple rules or algorithms that are passively managed. Model changes to these types of funds are also rare requiring prospectus filings with US Security and Exchange Commission in the case of US focused mutual funds or ETFs.. Smart Beta portfolios are generally long-only, they do not short stocks.

In contrast, a purely alpha-focused quantitative fund may use multiple models or algorithms to create a portfolio. The portfolio manager retains discretion in upgrading or changing the types of models and how often to rebalance the portfolio in attempt to maximize performance in comparison to a stock benchmark. Managers may have discretion to short stocks in portfolios.

Imagine you're a portfolio manager, and wish to try out some different portfolio weighting methods.

One way to design portfolio is to look at certain accounting measures (fundamentals) that, based on past trends, indicate stocks that produce better results.

The other way is design a portfolio that can then be made into an ETF. 

Smart Beta ETFs can be designed with both of these two general methods (among others): alternative weighting and minimum volatility ETF.

### **Part 1 Smart beta portfolio**

#### **Step 1: Compute weighted returns**

$$Weighted\ Returns = Returns \times Weights$$

#### **Step 2: Compute cumulative returns**

To compare performance between the ETF and Index, we're going to calculate the tracking error. Before we do that, we first need to calculate the index and ETF cumulative returns.

$$Cumulative\ Returns = (r_1 + 1)(r_2 + 1)...(r_t + 1) - 1$$

Tools:

- [pandas.DataFrame.cumprod](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.cumprod.html)

#### **Step 3: Tracking error**

In order to check the performance of the smart beta portfolio, we can calculate the annualized tracking error against the index.

$$Tracking\ Error = \sqrt{252} \times Sample\ Stdev(r_p - r_b)$$,

where $r_p$is the portfolio/ETF returns and $r_b$ is the benchmark returns.

*Note: When calculating the sample standard deviation, make sure to set the delta degrees of freedom to 0.*

### **Part 2 Portfolio optimization**

We want to both minimize the portfolio variance and also want to closely track a market cap weighted index. In other words, we're trying to **minimize the distance between the weights of our portfolio and the weights of the index**.

**Minimize** [$$\sigma_p 2 + \lambda\sqrt{\sum_1^m(Weight_i - index\ Weight_i)^2}$$]

where $m$ is the number of stocks in the portfolio, and $\lambda$ is a scaling factor that you can choose.

Why are we doing this? One way that investors evaluate a fund is by how well it tracks its index. The fund is still expected to deviate from the index within a certain range in order to improve fund performance. A way for a fund to track the performance of its benchmark is by keeping its asset weights similar to the weights of the index. We’d expect that if the fund has the same stocks as the benchmark, and also the same weights for each stock as the benchmark, the fund would yield about the same returns as the benchmark. By minimizing a linear combination of both the portfolio risk and distance between portfolio and benchmark weights, we attempt to balance the desire to minimize portfolio variance with the goal of tracking the index.

#### **Step 4: Compute covariance matrix of returns**

If we have mm stock series, the covariance matrix is an $m \times m$ matrix containing the covariance between each pair of stocks.

The covariance matrix = $$\left [\begin{matrix} \sigma_{1, 1} 2 & ... & \sigma_{1, m} 2 \\ ...  & ... & ...\\ \sigma_{m, 1} 2 & ... & \sigma_{m, m} 2\end{matrix}\right]$$

Tools:

- [numpy.cov](https://docs.scipy.org/doc/numpy/reference/generated/numpy.cov.html)
- [pandas.DataFrame.fillna](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.fillna.html)

#### **Step 5: Optimize portfolio**

The portfolio variance is $\sigma_p 2 = x^TPx$.

Recall that the $x^TPx$ is called the quadratic form. We can use the cvxpy function `quad_form(x,P)` to get the quadratic form.

So, the objective function is: $$x^TPx + \lambda\Vert{x - index}\Vert_2$$

Tools:

- [cvxpy](http://www.cvxpy.org/)

#### **Step 6: Rebalance portfolio over time**

The single optimized ETF portfolio used the same weights for the entire history. This might not be the optimal weights for the entire period. Let's rebalance the portfolio over the same period instead of using the same weights.

Rebalance the portfolio every n number of days. When rebalancing, you should look back a certain number of days of data in the past.

#### **Step 7: Compute portfolio turnover**

With the portfolio rebalanced, we need to use a metric to measure the cost of rebalancing the portfolio by calculating the annual portfolio turnover.

$$Annualized\ Turnover = \frac{Sum\ Total\ Turnover}{Number\ of\ Rebalance\ Events} \times Number\ of\ Rebalance\ Events\ Per\ Year$$

$$Sum\ Total\ Turnover = \sum_{t, n}|x_{t, n} - x_{t+1, n}|$$, where $x_{t, n}$ are the weights at the time $t$ for equity $n$.
