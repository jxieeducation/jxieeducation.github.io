---
layout: post
category : paper
tags: visualization, timeseries
tagline: "Autocorrelation Quick Explanation"
excerpt: Autocorrelation Quick Explanation

---

### Autocorrelation Quick Explanation

A few months ago, I wrote a post on [time series decomposition]({{ site.url }}//time-series-decomposition/). I just want to follow up on how to learn more about the periodicity of the periodic / seasonal portion of the time series.

*I have a short R script [here](https://github.com/jxieeducation/Quick-Data-Science-Experiments-2016/blob/master/autocorrelation_test/explore.R) if you want to follow along.*

### Demo

Autocorrelation tells us about how a time series relates to itself. 

Here is a dataset of the length of English kings' lives.

![king ages](https://raw.githubusercontent.com/jxieeducation/Quick-Data-Science-Experiments-2016/master/autocorrelation_test/king_ages.png)

Autocorrelation tells us King's life spans are strongly related within 2 to 3 generations. However, this relationship becomes weak after 4 generations. After 15 generations, the King's life spans are inversely related likely due to the improvement in health care over many centuries.

![king ages acf](https://raw.githubusercontent.com/jxieeducation/Quick-Data-Science-Experiments-2016/master/autocorrelation_test/king_ages_cf.png)

### How It Works

Autocorrelation gets the correlation between a time series and itself with a lag of step N. 

$$ autocorr(X, N) = corr(X, X(t-N)) $$

Here the correlation is calculated as

$$ corr(X, X(t-N)) = \dfrac{ cov(X, X(t - N)) }{ std(X) * std(X(t - N)) } $$

The covariance between two series is positive when ```series A``` and ```series B``` move in the same direction, and negative when they are changing in different directions. 

So back to the King's example, lag 0 has an autocorrelation of 1 because the two series are the same. Lag 1 has an autocorrelation of 0.4 (a relatively high value) because of similarity in the two immediate king's time period as well as genetics. Lag 20 has a -0.25 score because 20 generations have past and health care has improved drastically. 

### Partial Autocorrelation

Partial autocorrelation removes dependencies between lag 0 and lag k by explicitly getting rid of interactions between lag 1 and lag k - 1. This is a sanitized and independent and arguably better performing version of autocorrelation.

![king ages partial acf](https://raw.githubusercontent.com/jxieeducation/Quick-Data-Science-Experiments-2016/master/autocorrelation_test/king_ages_pacf.png)
