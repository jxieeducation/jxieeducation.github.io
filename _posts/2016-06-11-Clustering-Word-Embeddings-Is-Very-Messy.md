---
layout: post
category : paper
tags: word2vec, wordembedding
tagline: "Clustering Word Embeddings"
excerpt: Clustering Word Embeddings

---

### Clustering Word Embeddings

Clustering word embeddings is pretty tricky. A good cluster contains all the members of a group with a distinct property. On the other hand, a bad cluster has nothing different from everything else. This post is going to be about what I learned while running some experiments.  

### Distance Metric

Most clustering packages support Euclidean distance and not cosine distance. However, in word embeddings, the intuitive measurement is cosine distance (``` 1 - cosine similarity ```). 

Cosine similarity measures the angular similarity, while Euclidean distance measures geometric differences. Your intuition tells you that Euclidean distance is not viable. However, I do think that Euclidean distance is actually more viable than cosine similarity. 

#### Some reasons why: 
* All embeddings are normalized, so there wouldn't exist embeddings of  the same angle but different scalars. 
* Euclidean distance (l2) punishes large differences
* There are some experimental results on Euclidean distance performing better than Cosine Similarity - [paper](http://arxiv.org/pdf/1512.00765v1.pdf), [blog](http://sujitpal.blogspot.com/2015/09/sentence-similarity-using-word2vec-and.html)

### Size of Clusters

I always get terrible results when my cluster sizes are large. 

Here is an example of my results via Hierarchical clustering on the IMDB reviews. [Full cluster results](https://github.com/PragmaticLab/w2v_to_d2v/blob/master/results/result_hierarchical_clustering_average.txt)


| Cluster  | Count | Word descriptors              |
| :------: |:-----:| :----------------------------:|
| 0        | 11    | ogre, demons, nightmare, omen |
| 2        | 3905  | but, that, and, the           |
| 4        | 14    | cheesy, bad, fun, cheesiness  |

The average of docs that don't belong together results in nothing-ness. In word embeddings, this "nothing-ness" is the usual NLP stopwords, e.g. but, this, an...etc. I am now a lot more skeptical of large cluster sizes, because they typically introduces zero insight. 


### The Right Clustering Technique

* KMeans ([my results](https://github.com/PragmaticLab/w2v_to_d2v/blob/master/results/result_kmeans_clustering.txt)) produces some atrocious results, because without knowing a good k value, the clusters then to be large and useless
* Hierarchical ([my results](https://github.com/PragmaticLab/w2v_to_d2v/blob/master/results/result_hierarchical_clustering_average.txt)) tend to be better than KMeans in that at least there tend to be a good number of small and unique clusters. However, because of how it is bottom up, there tends to be a large cluster of nothing-ness. 
* SOM ([my results](https://github.com/PragmaticLab/w2v_to_d2v/blob/master/results/result_self_organizing_map.txt)) seems like a better version of KMeaens but also needs a lot of manual tuning to get reasonable results

I have yet to find a particularly good technique for clustering. Maybe my distance metric is off (this [paper](http://jmlr.org/proceedings/papers/v37/kusnerb15.pdf) seems to offer a good alternative). Or maybe the techniques are completely off and that I should start incorporating topic modeling as part of the process like LDA2VEC. Will follow up on this when I have more insight.



