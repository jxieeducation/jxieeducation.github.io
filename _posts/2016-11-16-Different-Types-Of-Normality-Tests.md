---
layout: post
category : tutorial
tags: statistics
tagline: "Different Types of Normality Tests"
excerpt: Different Types of Normality Tests

---

### Normality Tests

This is a short post focused on the intuition behind the various normality statistical tests out there. 

I will be talking about the Kolmogorov–Smirnov test for historical reasons, the Anderson-Darling test for its popularity and the Ryan-Joiner test for its similarity to regression.

### Kolmogorov-Smirnov 

The KS and AD tests are both based on the emperical CDF function. For those  familiar with nonparametric density estimation, it's very very similar. 

$
F_n(X) = \dfrac{1}{n} \sum_{i=i}^n I_{\left| -\infty, X \right|}(X_i)
$

![eCDF](https://upload.wikimedia.org/wikipedia/commons/thumb/1/17/Empirical_CDF.png/300px-Empirical_CDF.png)

In the diagram above, the emperical CDF is the blue line. The theoretical CDF is the black line. 

The KS score is defined as the maximum difference between the emperical and theoretical CDF for any X (Z-value). This sounds great theoretically. 

#### However, the KS test has several disadvantages in reality:
* Most sensitive when the EDFs differ near the center of the distribution (Z = 0)
* The test cannot be applied to multivariate data

### Anderson-Darling

Anderson-Darling is an improvement directly from the KS test, by taking account of the first weakness.

The CDF function by design converges to 0 and 1 at the beginning and end of the distributions respectively. The AD test counters this by using a weighted emperical CDF that puts more emphasis on the tails. 

$
A = n \int^{-\infty}_{\infty} \dfrac{(F_n(x) - F(x))^2}{F(x) (1 - F(x))} dF(X)
$ 

In the formula above, the denominator is the weighting factor that puts emphasis on the tails. 

### Ryan-Joiner

The Ryan-Joiner test has its roots in the pearson correlation. It simply measures the linearity of data points on the qqplot. The qqplot is simply the percentiles of the values versus the z-values of the $x_i$. 

![qqplot example](https://upload.wikimedia.org/wikipedia/commons/thumb/0/08/Normal_normal_qq.svg/300px-Normal_normal_qq.svg.png)

The above is an example of a normal distribution.

### Conclusion

In any software package, there are many normality tests. I generally tend to look at a few of them at the same time when I don't have time to analyze the implications and assumptions behind the tests. (like an ensemble of normality tests)
