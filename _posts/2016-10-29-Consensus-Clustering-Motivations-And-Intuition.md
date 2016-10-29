---
layout: post
category : tutorial
tags: clustering
tagline: "Consensus Cluster Motivations and Intuition"
excerpt: Consensus Cluster Motivations and Intuition

---

### Unsupervised Clustering Is Hard

It's pretty much universal knowledge that clustering algorithms have some major shortcomings. Having spent the past week doing a lot of topic modeling with NMF, I have quite a lot of complaints.

![nmf vis](http://www.nature.com/nature/journal/v401/n6755/images/401788ab.eps.0.gif)

#### Here are some usual complaints about clustering algorithms:
* Choosing the number of clusters
	* e.g. NMF is pretty dependent on the number of latent factors k
* Sensitivity to initialization
	* e.g. K-means Lloyd's algorithm is a serious offender
* Stuck in local minima
	* e.g. Any EM based clustering algorithm like GMM needs random restarts

Consensus clustering is an ensemble technique that tries to solve these problems.

### Consensus Clustering

Consensus clustering for unsupervised learning is analogous to ensemble learning in supervised learning.

Consensus Clustering (CC) is a meta-algorithm that combines multiple runs of a clustering algorithm. It takes in the item cluster labels or factorizations and outputs an aggregated item-item similarity matrix. 

<img src="{{site.imgrepo}}/consensus_embeddings.png" alt="input example" style="width:300px;height:100px; margin-left:10%">

<img src="{{site.imgrepo}}/consensus_item_item.png" alt="output example" style="width:300px;height:120px; margin-left:10%">

After running the above multiple times, we can aggregate the item-item similarities to create an aggregate similarity matrix.

*Note: In a way, consensus clustering is a resampling-based method, like a bootstrap for the clustering algorithm*

<img src="{{site.imgrepo}}/consensus_agg_matrix.png" alt="aggregate matrix" style="width:400px;height:200px; margin-left:10%">

We can think of the aggregated item-item similarity matrix as a stablized output of the clustering algorithm. This consensus matrix is useful in many ways and I will be outlining them in the sections below.

### Choosing Number of Clusters

If we obtain a consensus matrix for every number of cluster K, we can analyze the matrices to understand the appropriate number of clusters.

Looking at the sum of the values for each k, we can see where the values level out.

<img src="{{site.imgrepo}}/consensus_k_values.png" alt="aggregate matrix" style="width:400px;height:300px; margin-left:10%">

This plot can be interpreted similarly to a scree plot for PCA. The elbow of the graph is important and should warrant further investigation for the last meaningful decrease in entropy. 

### Measuring the Stability of Clustering

The consensus matrix also provides us with a summary statistic for the "consensus" of the clusters. This statistic can rank clusters in term of their stability. 

Say after running k-means, we are given a cluster $$ c_i $$. Let $$ M(j,k) $$ be the normalized entry in the consensus matrix for items $$ e_j $$ and $$ e_k $$. We can define the stability of a cluster as the average normalized consensus between every pair of items in the cluster.

$$ s_{c_i} = \frac{\sum_{j, k \in c_i} M(j, k)}{| j, k \in c_i |} $$

The statistic $$ s_{c_i} $$ can be used to describe how stable a cluster is.

### Conclusion

Consensus cluster provides perspective on the stability of clustering algorithms. [ConsensusClusterPlus](http://www.bioconductor.org/packages/release/bioc/vignettes/ConsensusClusterPlus/inst/doc/ConsensusClusterPlus.pdf) is a great R package if you want to try it out.

*Thank you [Chuck Wessel](http://meyer.math.ncsu.edu/Meyer/Talks/Consensus%20Clustering.pdf) for the visualizations*
