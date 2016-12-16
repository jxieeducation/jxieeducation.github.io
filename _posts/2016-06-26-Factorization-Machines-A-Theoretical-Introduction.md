---
layout: post
category : ml
tags: factorizationmachines
tagline: "What is Factorization Machines?"
excerpt: What is Factorization Machines?

---

## Factorization Machines

This post is going to focus on explaining what factorization machines are and why they are important. The future posts will provide practical modeling examples and a numpy clone implementation of factorization machines.

### What problem do Factorization Machines solve?

TL;DR: FMs are a combination of linear regression and matrix factorization that models sparse feature interactions but in linear time.

Normally when we think of linear regression, we think of this formula. 

$$ y = w_0 + \sum_{i=1}^n w_i x_i $$

In the formula above, the run time is $$ O(n) $$ where $$n$$ is the number of features. When we consider quadratic feature interactions, the complexity increases to $$ O(n^2) $$, in the formula below. 

$$ y = w_0 + \sum_{i=1}^n w_i x_i + \sum_{i=1}^n \sum_{j=i+1}^n w_{ij} x_i x_j $$

Now consider a very sparse set of features, the runtime blows up. In most cases, we instead model a very limited set of feature interactions to manage the complexity. 

### How do Factorization Machines solve the problem?

In the recommendation problem space, we have historically dealt with the sparsity problem with a well documented technique called (non-negative) matrix factorization. 

![matrix factorization diagram](http://data-artisans.com/img/blog/factorization.svg)

We factorize sparse user item matrix (r) $$ \in R^{UxI}$$ into a user matrix (u) $$ \in R^{UxK} $$ and an item matrix (i) $$ \in R^{IxK} $$, where $$ K << U $$ and $$ K << I $$. 

User ($$ u_i $$)'s preference for item $$ i_j $$ can be approximated by $$ u_i \cdot i_j $$. 

Factorization Machines takes inspiration from matrix factorization, and models the feature iteractions like using latent vectors of size $$ K $$. As a result, every sparse feature $$ f_i $$ has a corresponding latent vector $$ v_i $$. And two feature's interactions are modelled as $$ v_i \cdot v_j $$.  

### Factorization Machines Math

$$ y = w_0 + \sum_{i=1}^n w_i x_i + \sum_{i=1}^n \sum_{j=i+1}^n <v_i, v_j> x_i x_j $$

Instead of modeling feature interactions explicitly, factorization machines uses the dot product of features' interactions. The model learns $$ v_i $$ implicitly during training via techniques like gradient descent. 

The intuition is that each feature will learn a dense encoding, with the property that high positive correlation between two features have a high dot product value and vise versa. 

Of course, the latent vectors can only encode so much. There is an expected hit on accuracy compared to using conventional quadratic interactions. The benefit is that this model will run in linear time.

### FM complexity

For the full proof, see lemma 3.1 in Rendle's [paper](http://www.csie.ntu.edu.tw/~b97053/paper/Rendle2010FM.pdf).

$$ \sum_{i=1}^n \sum_{j=i+1}^n <v_i, v_j> x_i x_j $$

$$ = \frac{1}{2} \sum_{i=1}^n \sum_{j=1}^n <v_i, v_j> x_i x_j 
-  \frac{1}{2} \sum_{i=1}^n <v_i, v_i> x_i x_i $$

$$ = \frac{1}{2} \sum_{f=1}^k ((\sum_{i=1}^n v_{i,f} x_i )^2 - \sum_{i=1}^n v_{i,f}^2 x_i^2 ) $$

Since $$ \sum_{i=1}^n v_{i,f} x_i $$ can be precomputed, the complexity is reduced to $$ O(KN) $$. 

*Now that we have a theoretical understanding, in the next post, we will discuss practical use cases for factorization machines.*

### Benchmark (added Sep 24, 2016)

On the standard recommendation dataset, MovieLens-100k, using Vowpal Wabbit, normal linear regression achieved a MSE of 0.9652, while a FM achieved a MSE of 0.9140. 

For a guide on how to do Factorization Machines via Vowpal Wabbit, [see here](https://github.com/JohnLangford/vowpal_wabbit/wiki/Matrix-factorization-example).
