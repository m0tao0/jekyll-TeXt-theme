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
#### **Step 1: Compute the highs and lows in a window**

Look back a window of days to find out the highest and the lowest prices within the window.

Tools:

- [pandas.DataFrame.rolling](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.rolling.html)

#### **Step 2: Compute long and short signals**

If the close price of one day is lower than the lowest within the window, then generate a short signal (e.g. -1); if higher than the highest, a long signal (e.g. 1); if between the two, generate "nothing" signal (e.g. 0).

#### **Step 3: Filter signals**

Filter out repeated long or short signals within the look-ahead days (e.g. 3 days ahead). If the previous signal was the same, change the signal to 0 (do nothing signal).

#### **Step 4: Look ahead close price and returns and compute signal returns**

With the trading signal done, start working on evaluating how many days to short or long the stocks. Then, based on the close price days ahead in time, compute the log price return between the closing price and the look-ahead price, and generate the signal return.

#### **Step 5: Kolmogorov-Smirnov Test**

> In [statistics](https://en.wikipedia.org/wiki/Statistics), the [**Kolmogorov–Smirnov test** (**K–S test** or **KS test**)](https://en.wikipedia.org/wiki/Kolmogorov%E2%80%93Smirnov_test) is a [nonparametric test](https://en.wikipedia.org/wiki/Nonparametric_statistics) of the equality of continuous, one-dimensional [probability distributions](https://en.wikipedia.org/wiki/Probability_distribution) that can be used to compare a [sample](https://en.wikipedia.org/wiki/Random_sample) with a reference probability distribution (one-sample K–S test), or to compare two samples (two-sample K–S test). It is named after [Andrey Kolmogorov](https://en.wikipedia.org/wiki/Andrey_Kolmogorov) and [Nikolai Smirnov](https://en.wikipedia.org/wiki/Nikolai_Smirnov_(mathematician)).

> The Kolmogorov–Smirnov statistic quantifies a [distance](https://en.wikipedia.org/wiki/Metric_(mathematics)) between the [empirical distribution function](https://en.wikipedia.org/wiki/Empirical_distribution_function) of the sample and the [cumulative distribution function](https://en.wikipedia.org/wiki/Cumulative_distribution_function) of the reference distribution, or between the empirical distribution functions of two samples. The [null distribution](https://en.wikipedia.org/wiki/Null_distribution) of this statistic is calculated under the [null hypothesis](https://en.wikipedia.org/wiki/Null_hypothesis) that the sample is drawn from the reference distribution (in the one-sample case) or that the samples are drawn from the same distribution (in the two-sample case). In each case, the distributions considered under the null hypothesis are continuous distributions but are otherwise unrestricted.

> The two-sample K–S test is one of the most useful and general nonparametric methods for comparing two samples, as it is sensitive to differences in both location and shape of the empirical cumulative distribution functions of the two samples.

Tools:

- [pandas.DataFrame.stack](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.stack.html)
- [scipy.stats.kstest](https://docs.scipy.org/doc/scipy-0.14.0/reference/generated/scipy.stats.kstest.html#scipy-stats-kstest)

#### **Step 6: Find outliers**

Find outliers via symbols:

- Symbols that pass the null hypothesis with a p-value less than the p-value threshold (default = 0.05)
- Symbols that with a KS value above the k-static value threshold (e.g. 0.8)
