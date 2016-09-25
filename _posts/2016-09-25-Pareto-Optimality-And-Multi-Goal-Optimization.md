---
layout: post
category : tutorial
tags: optimization, pareto
tagline: "Pareto Optimality and Multi-Goal Optimization"
excerpt: Pareto Optimality and Multi-Goal Optimization

---

### Multiple Goals

Often times, we judge things by more than one metric. In classification, we care about precision and recall. In fitness, we care about strength and flexibility. And in life, we care about short-term and long-term happiness.

Unfortunately, often times, we cannot maximize multiple goals at the same time. In classification, higher precision usually means lower recall. In fitness, benching 300lbs usually mean that you have trouble scratching your back. And in life, spending all of your youth playing video games means that you won't be as smart and knowledgeable in the future.

<img src="http://newlifehouse.com/wp-content/uploads/2014/05/shorttermlongterm.jpg" alt="short term vs long term" style="width:400px;height:300px; margin-left:10%">

As said by some old and wise person (I hope), "life is all about the tradeoffs." And this post touches on the math behind maximizing multiple goals and understanding the trade offs.

### Pareto Optimality 

The Pareto Optimality means "Take from Peter to pay Paul." Let me explain what this means.

In Pareto Optimality, there are two classes of points: dominated and non-dominated. A dominated point is one where you can improve on one of the goals without lowering the others. For example, {goal 1: 20, goal 2: 20} is dominated by {goal 1: 20, goal 2: 21}. A non-dominated point on the other hand means that if you want to improve on any goal, some other goal(s) will suffer. 

<img src="{{site.imgrepo}}/pareto_front.png" alt="pareto front" style="width:400px;height:300px; margin-left:10%">

In this diagram, all of the dominated points in the objective space is colored  grey, and the non-dominated points is shaded in black. The pareto frontier (aka the non-dominated points, or the black line) shows us the best that we can do for either without consequences in the other. 

### How to determine dominance? 

Given two points each representing multiple objectives, we simply need to see if one point is greater or equal to the other in all objectives. 

$x_1 = \begin{bmatrix}9.5 & 7.5\end{bmatrix}$

$x_2 = \begin{bmatrix}8.5 & 7.5\end{bmatrix}$

$ [x_1 >= x_2] = \begin{bmatrix}1 & 1\end{bmatrix}$

Since $ [x_1 >= x_2] $ is all $1$s, we can say that $x_2$ is dominated.

And if for all points {1, 2, 3..., N}, $ x_1 $ is not dominated by $ x_n $, we can say that $x_1$ is non-dominated.

### Why is this useful?

Understanding the pareto front let us know what's possible. 

<img src="http://pubs.rsc.org/services/images/RSCpubs.ePlatform.Service.FreeContent.ImageService.svc/ImageService/Articleimage/2010/CP/b914552d/b914552d-f4.gif" alt="pareto optimality graph" style="width:400px;height:300px; margin-left:10%">

#### With this graph, you can answer some really important questions: 

* What cache size do I need for a 5ms response time? (RAM limits vs response time)
* How do I achieve a $14 vCPM for this ad? (CPM vs viewability)
* What do I buy to get the most out of my lunch? ($ vs tastiness)

### How to figure out the Pareto Front?

If the objectives are deterministic and can be represented mathematically, there are efficient methods like the Normal Boundary Intersection (NBI) and the Adaptive Weighted Sum (AWS). Feel free to read about them [here](https://ocw.mit.edu/courses/engineering-systems-division/esd-77-multidisciplinary-system-design-optimization-spring-2010/lecture-notes/MITESD_77S10_lec15.pdf). 

There are a lot that can be said about the math behind solutions such as the Weighted Sum approach. However, most of them are very intuitive, so I won't be covering the details in this post.

Then there is also the other case, where our objective functions are blackboxes that can't be calculated. In these situations, we fallback to search functions to generate data points in order to generate the pareto front, some methods are:

1. random search / uniform search
2. genetic algorihtms / particle swarms / any heurestic based ones

### Conclusion

There is a lot of value in understanding the pareto front of multi-objective optimization problems. For more resources, checkout the [Multidisciplinary System Deisgn Optimization course](https://ocw.mit.edu/courses/engineering-systems-division/esd-77-multidisciplinary-system-design-optimization-spring-2010/lecture-notes/) from MIT Open Courseware.
