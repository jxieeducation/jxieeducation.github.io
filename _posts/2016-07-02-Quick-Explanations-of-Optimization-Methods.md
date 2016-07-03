---
layout: post
category : paper
tags: optimization
tagline: "Quick Explanations of Optimization Methods"
excerpt: Quick Explanation of Optimization Methods

---

## Optimization methods

One of the biggest mysteries for beginners in neural networks is figuring out when to use which optimization method. This post focuses on describing popular first-order methods: SGD, Momentum, Nesterov Momentum, Adagrad, RMSProp and Adam. 

*Second order methods are not included largely because inverting the Hessian takes too much computation power, and most deep learning researchers find it impractical to use second order methods.*

### Stochastic Gradient Descent

Using stochastic gradient descent, we simply follow the gradient. The gradient is controlled by a learning rate, which typically tends to be a linearly decreasing number. 

$$ \theta = \theta - \alpha \cdot \nabla J(\theta) $$ 

The problem with SGD is that chosing a proper learning rate is difficult and it's easy to get trapped in a saddle point when optimizing a highly non-convex loss function.


### Momentum 

Stochastic Gradient Descent can oscillate and have trouble converging. Momentum tries to improve on SGD by dampening the oscillation and emphasizing the optimal direction. 

If we call the update $$ v $$, the SGD equation becomes $$ \theta = \theta - v $$. Momentum combines the past update along with the current update, in order to stablize the updates. 

$$ v_t = \mu \cdot v_{t-1} + \alpha \cdot \nabla J(\theta) $$

The value of $$ \mu $$ is usually close to 1 e.g. 0.9, 0.95. 

### Nesterov Momentum

Momentum is an improvement on SGD because $$ v_t $$ is combined with $$ t_{t-1} $$. However, because $$ v_t $$ is very dependent on $$ v_{t-1} $$, momentum by itself is slow to adapt and change directions. 

Nesterov momentum builds on raw momentum. Instead of calculating $$ v_t $$ via $$ \nabla J(\theta_t) $$, Nesterov tries to calculate $$ \nabla J(\theta_{t + 1}) $$. But how can we calculate the gradient of the parameters in the future? We can't. However, we can approximate the future parameter by assuming that $$ v_t = \mu \cdot v_{t-1} $$, which is largely true. 

![nesterov pic](http://cs231n.github.io/assets/nn3/nesterov.jpeg)

$$ v_t = \mu \cdot v_{t-1} + \alpha \cdot \nabla J(\theta - \mu \cdot v_{t-1}) $$

### Adagrad 

Adagrad, RMSProp and Adam take a different approach on how to improve SGD. SGD, Momentum and Nesterov Momentum all have a single learning rate for all parameters. The following 3 methods instead adaptively tune the learning rates for each parameter.

Adagrad normalizes the update for each parameter. Parameters that had large gradients will have smaller updates; small or infrequent gradients will be bumped to take larger steps. 

$$ v = \dfrac{ \alpha \cdot \nabla J(\theta) }{ \sqrt{ cache } } $$


$$ cache = \sum_{t=1}^n { \nabla J(\theta_{t}) }^2 $$

Adagrad will eventually be unable to make any updates, because the size of cache becomes infinity. 


### RMSProp

RMSProp improves on adagrad by decaying the size of the cache. The cache is "leaky" and prevents the updates from becoming 0. Hinton recommends setting $$ \gamma $$ to 0.99 and $$ \alpha $$ to 0.01. 

$$ cache_t = \gamma \cdot cache_{t-1} + (1 - \gamma) \cdot {\nabla J(\theta_{t})}^2 $$

### Adam

Adam is a variation of RMSProp.

$$ m_t = \beta_1 \cdot m_{t-1} + (1 - \beta_1) \cdot \nabla J(\theta_{t}) $$

$$ v_t = \beta_2 \cdot v_{t-1} + (1 - \beta_2) \cdot {\nabla J(\theta_{t})}^2 $$ 

$$ \theta_t = \theta_{t-1} - \dfrac{ \alpha \cdot m_t }{ \sqrt( v_t ) } $$

### When to use what?

There is no concensus which optimization methods are the best. In my experience, adagrad based methods are a lot safer but slower than momentum based methods. I usually stick to RMSProp for the first cut of the model and test other methods afterwards. 



