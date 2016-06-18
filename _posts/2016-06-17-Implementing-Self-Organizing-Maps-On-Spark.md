---
layout: post
category : paper
tags: som, visualization
tagline: "Implementing Self Organizing Map On Spark"
excerpt: Implementing Self Organizing Map On Spark

---

### Implementing Self Organizing Map on Spark

Self Organizing Maps is probably the most popular visualization method in computational biology. While SOMs never achieved the same adoption rate in other areas, it's still a very versatile tool. Code for everything in this post can be found [here](https://github.com/PragmaticLab/spark-som).

![som init]({{site.imgrepo}}/som_spark_init.png)

Initializations of SOM on colors

![som finished]({{site.imgrepo}}/som_spark_result.png)

Finished SOM color visualizations

### Initialization

#### There a few straight forward ways to initialize SOMs:
* Generating random numbers between 0 and 1
* Picking random members of the training dataset
* Divide up the training dataset via the first N principal components via PCA

The better the SOM codebooks are initialized, the faster the training convergence.

### Training

The SOM training process has two steps: 1) finding a winner 2) adapt the winner and cells around the winner to be closer to the data point. 

The adaption or update formula is $C(i) = C(i) + \alpha * \omega * (X_i - C(i))$, where $\alpha$ is the learning rate and $\omega$ is the field multiplier that is stronger near the winner (e.g. Gaussian around the winner). 

Training can be distributed via data partitioning. For each partition of the data, an independent codebook is trained. At the end of an epoch, the different codebooks are averaged as the new codebook. 

I ran experiments on gigabytes of color vector and word embedding data. The Spark speed up is slightly less than linear as the number of executors increase, which makes SOM training very scalable.

### Error

SOM's success can be measured by the quantization error, which is just the average error between the cell and the datapoints that are quantized to the cell. 

### Variations of SOM

I also implemented 2 variations of SOM, which try to dynamically grow a SOM. Both are also compatible with Spark.  

#### *Self Organizing Tree Algorithm*: [paper here](http://bioinformatics.oxfordjournals.org/content/17/2/126.long)
* SOTA starts out with a simple node that's the mean of all the data points
* After each cycle, the cell that has the highest quantization error reproduces two identical children
* The growth can be stopped via different criteria (e.g. depth, number of leaf..etc.)

![som init]({{site.imgrepo}}/som_growing_grid.png)

#### *Growing Grid*: [paper here](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.54.8183&rep=rep1&type=pdf)
* Growing Grid starts out with 4 cells and expands
* It adds an additional row or column between the cell with the highest quantization error and its most different neighbor
* The idea is to figure out how to reduce the quantization error of the cell with the highest variance 
* The new cells are initialized as the average of their surrounding

### To do

I definitely need to run more profiling to improve the implementation of the Spark training code. Please feel free to contribute [here](https://github.com/PragmaticLab/spark-som).

