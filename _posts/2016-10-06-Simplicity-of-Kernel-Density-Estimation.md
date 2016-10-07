---
layout: post
category : tutorial
tags: probability_theory
tagline: "Simplicity of kernel density estimation"
excerpt: Simplicity of kernel density estimation

---

### Smoothed Histograms

I recently picked up Seaborn for data visualization. I love the package because it makes me feel pro. 

One of my favorite plots is the KDE plot. And this post is about how the KDE is calculated.

![kde plot](http://pandas.pydata.org/pandas-docs/version/0.17.0/_images/rplot-seaborn-example2.png)

### Probability Density Estimation

There are 2 general approaches to estimating the PDF of a distribution. 

The first group is parametric. We have some prior assumption that the data follows a certain distribution (e.g. gaussian, student t, gamma) and try to fit parameters around these distributions.

The second is nonparametric. They make no prior assumptions on the distribution of the data by modeling the data instead of the parameters. I will go into more details the Parzen Window approach.

### The General Approach

The PDF of x can be modeled as the following:

$ 
p(x) = \frac{ \frac{k}{n} }{v} = \frac{k}{nv}
$

Here v stands for the volume. First, we specify a bin size (or volume), like we do with histograms. 

Then we get k (the number of samples in the bin) and n (the total number of samples) to calculate the density of the bin. 

![hist](http://matplotlib.org/1.3.0/_images/histogram_demo_extended_01.png) 

Overall, the formula works exact like a histogram, but converted (via division over the volume / bin size) to make it behave like density.


### Parzen Window

The Parzen Window is a very simplistic kernel that is best explained pictorially. 

![parzen]({{site.imgrepo}}/kde_parzen_window.png)

[Source](http://www.csd.uwo.ca/~olga/Courses/CS434a_541a/Lecture6.pdf)

Here the 7 points are colored. The density estimation is: 

$ p(x) = \frac{ \sum_i^n (\| x - p_i \| <= \frac{3}{2})}{21} $

Here the denom is $ 21 = nv = 7 * 3 $ 

This way of calculating density is nonparametric because we need to remember every single sample in $ D $. 

### Smoothed Parzen Window

Instead of a kernel that returns 0 or 1, we can use a gaussian instead $
\frac{ 1 }{ \sqrt{2 \pi } } e^{ \frac{-d^2}{2} }
$. 

As a result, the generated density estimation is smoothed. 

![kde gaussian](https://upload.wikimedia.org/wikipedia/en/thumb/4/41/Comparison_of_1D_histogram_and_KDE.png/500px-Comparison_of_1D_histogram_and_KDE.png)

### Choosing the Right Window Size

The window size h is the only parameter that we need to decide for the KDE. 

![kde h diff]({{site.imgrepo}}/kde_h_window_values.png)

Generally, if h is too big (left) or h is too small (right), then the quality of the density estimation will suffer. 

In a classification context, we can systematically choose h by fitting KDEs to each category, classify test points under the maximum posterier, and varying h to get the best accuracy. 

### Conclusion

Check out the kdeplot function in Seaborn. Hopefully this post explained the basics of how the density estimation really works. 
