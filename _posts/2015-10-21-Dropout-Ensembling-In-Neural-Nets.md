---
layout: post
category : ml
tags: neuronetwork overfitting
tagline: "Dropout As Prevention For Co-Adoption In Feedforward Neural Net"
excerpt: As the size of our neuro nets get larger, it becomes especially easy to overfit. Pretend that we have 20,000 neurons across 20 layers, with only 500 training examples, it's very easy for the net to memorize the shape of the data and come up with some crazy, super high dimension model only to fit the data. Here I present some visualizations of the effects of dropout.
---

## Dropout in Neuro Nets 
  
As the size of our neuro nets get larger, it becomes especially easy to overfit. Pretend that we have 20,000 neurons across 20 layers, with only 500 training examples, it's very easy for the net to memorize the shape of the data and come up with some crazy, super high dimension model only to fit the data.

Another way to think about it is: pretend that we are studying for a big physics exam. However, the professor provided only 1 practice problem. Because we only have 1 practice problem, we spent a very long time to make sure that we would get the practice problem correct. However, we do poorly on the exam, because we tunneled on the specific problem.

---

### How does dropout work? 

Normally, the input for a neuron is this:

$$y=W\^T X$$

However, the dropout says that we should randomly shut off some weights, effectively turning off some neurons. The dropout equation works like this: 

$$y=W R\^T X$$

$$
y = 
\begin{bmatrix}w1 \\\ w2 \\\ w3 \end{bmatrix}
\begin{bmatrix}1 & 0 & 1 \end{bmatrix}
\begin{bmatrix}x1 \\\ x2 \\\ x3 \end{bmatrix}
$$

Here R is a combination of ```0```s and ```1```s. If we want 30% dropout, then there would be 30% ```0```s and 70% ```1```s. And 30% of the input neurons would be turned off.

--- 

### Experiment on the Titanic dataset

Here is the topology of my net.
![dropout diagram]({{site.imgrepo}}/dropout-net-diagram.png )

Then to understand dropouts, I did a grid search on the loss function for the training and test set.

![dropout res]({{site.imgrepo}}/dropout-grid.png )

Here we see that we are overfitting like crazy when the dropout is small, because the training loss is much smaller than the test loss. However, as the dropout percentage increases, the training loss and test loss converge. 

---

### Intuition

When the size of the neuro net is large, it's easy for neurons to co-adapt, meaning that they work together to fit the model as well as possible. This leads to overfitting, making the net lose much of its predictive power.

When we applied dropout, we see that the training loss increased. This is because we are preventing the features from overfitting with crazy formulas. Instead, the neuro network is forced to learn multiple independent representations of the data. (You can't co-adapt when you are not there randomly)

We can pretty much think of the dropout layer as a regularization mechanism that punishes overfitting. 

