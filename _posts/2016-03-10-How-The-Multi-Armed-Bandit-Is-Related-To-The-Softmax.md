---
layout: post
category : tutorial
tags: softmax, bandit
tagline: "Intuition of softmax"
excerpt: Evolution stages of how the softmax algorithm came to be.

---

## Evolution of Softmax
Let's say that we are doing A/B testing. We know that $\mu_A = 0.5$ and $\mu_B = 0.2$ for algorithms A and B. And we are interested in picking between algorithms A and B based on their performance.

### Weighted Percentage
A simple answer would be choose the algorithm directly proportionally to its performance.

In this case, we would use A, $\dfrac{\mu_A}{\sum_{i=0}^n \mu_i}$ % of the time. 

### Weighted Exponential
In realty, our naive algorithm isn't adopted. Instead, people choose to scale the rewards exponentially.

After exponentiating, we'd use A, $\dfrac{e^{\mu_A}}{\sum_{i=0}^n e^{\mu_i}}$ % of the time.

### Regularized Exponential
In order to make the weighted exponential more stable, we should scale $\mu_i$.

Then the percentage becomes $\dfrac{e^ \dfrac{\mu_A}{\tau} }{\sum_{i=0}^n e^ \dfrac{\mu_i}{\tau} }$.

$\tau$ here is used to trade off 2 extremes. When $\tau -> \infty$, we will choose the arms at random regardless of $\mu$. However, when $\tau -> 0$, we will always choose the arm with the highest individual value.

### Simulated Annealing
The annealing algorithm takes inspiration from blacksmithing, where the iron is hot and maleable in the beginning, but slowly becomes colder and more permanent.

We want the annealing effect for our softmax algorithm as well, where we want to explore a lot of A and B at first, then slowly converge on one of the two.

We can simulate $\tau$ as $\dfrac{1}{\ln{t}}$, where t is how many sample points we have already.

###Summary
$Pr(k) = \dfrac{e^ \dfrac{\mu_k}{\tau} }{\sum_{i=0}^n e^ \dfrac{\mu_i}{\tau} }$, where $\tau = \dfrac{1}{\ln{t}}$
