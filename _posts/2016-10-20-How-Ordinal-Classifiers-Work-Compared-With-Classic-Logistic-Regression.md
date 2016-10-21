---
layout: post
category : tutorial
tags: ordinal
tagline: "How Ordinal Classifiers Work Compared With Classic Logistic Regression"
excerpt: How Ordinal Classifiers Work Compared With Classic Logistic Regression

---

### Ordinal Data

I recently started working a lot more with survey data. So I got a lot more opportunities to play with ordered categorical data (e.g. cold -> warm -> hot). 

Standard regression assumes that the variables are measured based on a metric (e.g. meters, # thousand likes). However, with ordinal data, we don't know how to quantify the distance between the categories (e.g. cold to warm vs warm to hot).

![pepper img](http://www.statisticshowto.com/wp-content/uploads/2013/09/hotscale.jpg)

### Techniques with Ordinal Data

It's possible to have ordinal predictors (X), response variables (y) or both. In this post, I only talk about oridnal response variables, if you are interested in ordinal predictors, [this](http://www.norusis.com/pdf/ASPC_v13.pdf) is a great starting point. 

Two popular Ordinal Logistic Regression techniques are the Immediate-Threshold and All-Threshold methods. I will be referencing quite a lot of [Jason Rennie's summary](http://qwone.com/~jason/writing/olr.pdf). 

### Immediate Threshold LR

Let's think back to the classic logistic regression.

$
J = \sum_i^n log(1 + e^{-y_i * x_i^T w})
$

This formula is very intuitive for binary logistic regression. However, what happens if we want to model ordinal responses instead? 

![thresholds](https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcTYG9_ZWMhiND_UifGUxU3NqJdD4IphVT5CXxlxiZpq8KiLNIkb2A)

A simple method would be introduce thresholds $\theta_{yi}$ and calculate $\theta_{yi} - x_i^T w$ instead of $ x_i^T w$. 

This leads to the following loss function known as the immediate threshold method.

$
J_{im} = \sum_i^n h(\theta_{yi - 1} - x_i^T w) + h(x_i^T w - \theta_{yi})
$

The first term tries to maximize the distance between the predicted category with the left immediate category; and the second term tries to maximize the distance with the right immediate category. 

In a way, we can almost interpret it as a maximum margin classifer. Below is a diagram typically used to explain SVMs. 

![svm diagram](http://users.sussex.ac.uk/~christ/crs/ml/copied-pics/max-margin-classification.png)

### Problems with the Immediate Threshold and the All Threshold

With immediate threshold, there is no guarantee that the the thresholds are ordered. 

Imagine an imbalanced dataset, by the virtue of maximizing the margins, the dominant classes can overshadow the less frequent ones. 

In order to solve this problem, we want to construct a loss function that takes account of all the categories instead. 

$
J_{all} = \sum_i^n [ \sum_{k=1}^{y_i-1}  h(\theta_k - x_i^T w) + \sum_{k=y_i}^{l-1} h(x_i^T w - \theta_k) ] 
$

The All Threshold loss is very similar to the Immediate Threshold, except that it tries to maximize the margin of a category from all the others. 

### Conclusion

I will update when I have more practical experience using these methods. I hope that this post provides some basic intuition on how the threshold-based ordinal classifications work!
