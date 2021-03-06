---
layout: post
category : ml
tags: SGD
tagline: "Hogwild Stochastic Gradient Descent"
excerpt: Stochastic gradient descent differs from batch gradient descent in that the weights are updated using a single sample as opposed to the whole dataset. Because the weights are updated after every single sample is computed, the weight variable is updated very frequently.
---

## Parallelizing SGD

Stochastic gradient descent differs from batch gradient descent in that the weights are updated using a single sample as opposed to the whole dataset. Because the weights are updated after every single sample is computed, the weight variable is updated very frequently.

---

### How SGD works

Repeat until convergence: 
1. pick a random element in the training set
2. update the weights with the example
$$\theta \leftarrow (\theta - \alpha \nabla L(f(x_i), y_i)) $$

Because of the fast updates, SGD has the following properties:
1. Unlike GD, each update in SGD can improve or enlarge the loss
2. SGD converges faster than GD because we update the weights much more frequently
3. SGD takes much longer to get to the most "optimal" solution, making it less likely to overfit

![SGD vs GD]({{site.imgrepo}}/sgdvsgd.png )

---

### Parallelizing SGD

Looking at the SGD formula, it appears to be hard to parallelize, because all the weight updates are sequential. This means that we need to finish the current small and quick update before going forward.

When multithreading, a single thread generally takes only a few microsecond to calculate the new weight, but may need to wait several miliseconds to obtain permission (the lock) to update the weight. It's like in life, when it takes you a few seconds to fill out a document, but a months for the document to be processed.

Fortunately, scientists at the University of Wisconsin-Madison discovered that [SGD doesn't need to be synchronous](https://www.eecs.berkeley.edu/~brecht/papers/hogwildTR.pdf).

Because although weight updates would inevitably overwrite each other, the absense of locks enables SGD to perform many times more updates overall. Going back to the 3 properties of SGD listed earlier, (2) and (3) allow the asynchronous SGD to yield good results in a fraction of the time. 

---

### Experimental Results on the [Connect 4 Dataset](https://archive.ics.uci.edu/ml/datasets/Connect-4)

The dataset's features are the states of each square on the board. Each column can be either B(lank), X or O. And the target variables are (w)in, (d)raw or (l)oss. The features and target are normalized and put through a logistic regression classifier via SGD.

I was able to consistently achieve 90-92% accuracy with the [raw](https://github.com/jxieeducation/HogwildSGD/blob/master/connect4/sync.py), [lock-threaded](https://github.com/jxieeducation/HogwildSGD/blob/master/connect4/async_lock.py) and [nolock-threaded](https://github.com/jxieeducation/HogwildSGD/blob/master/connect4/async_nolock.py) implementations. 

Even though the performance did not improve, the speed of the lock-threaded proved to be much faster compared to the nolock-threaded implementation. 

![SGD lock vs nolock]({{site.imgrepo}}/sgd-no-lock.png )

### Caveat

I expected the nolock-threaded speed to plateau while the number of threads are small, because given the unsynchronous nature of weight updates, the time should not increase linearly. However, this hypothesis need to be tested on a really powerful computer before anything is conclusive. 
