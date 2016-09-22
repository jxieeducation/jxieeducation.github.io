---
layout: post
category : tutorial
tags: ANOVA
tagline: "Anova F Ratio"
excerpt: Anova F Ratio

---

### The F-Ratio

I have always known the F-score in classification as the harmonic mean between precision and recall. However, I recently also learned that there is another F-score, which I will denote as the F-ratio, widely used in ANOVA analysis. This post will attempt to explain how the F-ratio works.

### F-Ratio Formula

For a feature i, the F-ratio is calculated as follows:

$
F(i) = \dfrac{ (\bar{x_i}^{+} - \bar{x_i})^2 + (\bar{x_i}^{-} - \bar{x_i})^2 }
{ 
	\dfrac{1}{n_{+} - 1} \sum_{k=1}^{n_{+}} (x_{k,i}^{+} - \bar{x_i}^{+})^2
	+ 
	\dfrac{1}{n_{-} - 1} \sum_{k=1}^{n_{-}} (x_{k,i}^{-} - \bar{x_i}^{-})^2
}
$

Here $x^{+}$ and $x^{-}$ denote positive and negative labelled examples respectively. 

### How to Interpret the F-Ratio

The numerator is called F1 (variability between groups), and the denominator is called F2 (variability within groups). 

$ 
F = \dfrac{F1}{F2} 
= \dfrac{\text{Between-group Variance}}{\text{Within-group Variance}}
= \dfrac{\text{Effect Variance}}{\text{Error Variance}}
$

A simple and effective feature would have a high F-Ratio and vise-versa. In order to understand it futher, let's break it down into F1 and F2 scores, since the F-Ratio is a combined metric.

---

#### Case 1: Low F1, High F2 

This combination results in the lowest F-Ratio. As shown below, it's practically impossible to separate the pos and neg classes base on the feature.

<img src="{{site.imgrepo}}/fscore_low_f1_high_f2.png" alt="low f1 high f2" style="width:400px;height:300px; margin-left:10%">

*pos ~ N(4.8, 1), neg ~ N(5.2, 1)*

---

#### Case 2: Low F1, Low F2

Although $\bar{x_i}^{+}$ and $\bar{x_i}^{-}$ are fairly close together, the within-group variance is also fairly low, which makes it an improvement over case 1.

<img src="{{site.imgrepo}}/fscore_low_f1_low_f2.png" alt="low f1 low f2" style="width:400px;height:300px; margin-left:10%">

*pos ~ N(4.8, 0.1), neg ~ N(5.2, 0.1)*

---

#### Case 3: High F1, High F2

This is the exact opposite of case 2. Although the within-group variance is considerable, the distance between the 2 gaussians are far apart.

<img src="{{site.imgrepo}}/fscore_high_f1_high_f2.png" alt="high f1 high f2" style="width:400px;height:300px; margin-left:10%">

*pos ~ N(2, 1), neg ~ N(8, 1)*

---

#### Case 4: High F1, Low F2

This is the best case scenario, also with the highest F-Ratio. The decision boundary between the positive and negative is clear and precise.

<img src="{{site.imgrepo}}/fscore_high_f1_low_f2.png" alt="high f1 low f2" style="width:400px;height:300px; margin-left:10%">

*pos ~ N(2, 0.1), neg ~ N(8, 0.1)*

It should be apparent that the F-Ratio is a measure of how effective one (and only one) variable is at for the task of constructing the decision boundary.

### Weakness

The main weakness of the F-Ratio lies in how one-dimensional it is. (Literally. Cue laughter). 

<img src="http://i.stack.imgur.com/EYTKH.png" alt="weakness" style="width:300px;height:300px; margin-left:10%">

In the above example, neither x1 nor x2 have a high F-Ratio. In fact, judging blindly by the F-Ratio, you'd guess that x1 and x2 have little statistical power. However, the mutual information between x1 and x2 can easily discern the binary classes.

### Conclusion

Sadly, this post does not cover much in regards to ANOVA. The F-Ratio described here only covers a fraction of one-way ANOVA. However, hopefully I was able to provide some statistical intuition in regards to what the F-Ratio tries to measure.
