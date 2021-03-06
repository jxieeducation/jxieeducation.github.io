---
layout: post
category : ml
tags: word2vec, wordembedding
tagline: "Translation between Word Embeddings"
excerpt: Translation between Word Embeddings

---

### The Problem With Word Embeddings

Refreshing Word2Vec embeddings is a pain. Say that you'd like to change the dimensions of your embeddings or to use a better trained model, you'd need to recalculate almost everything that you have used embeddings for, because the new embeddings are totally different. This applies to any modeling, unsupervised learning or visualizations. 

### The Solution

It turns out that maybe you don't need to recalculate everything. Word2Vec embeddings can be translated from one to another as long as the relationship between words are the same.

I trained 2 different w2v models on the IMDB reviews. The vocabulary and corpus stayed the same. However, the embeddings for the words are totally different. 

```
model1 - "one" : 3.52521874e-02, 4.00067866e-03, 2.30610892e-02
```

```
model2 - "one" : -5.90761974e-02, -3.17945816e-02, 1.26407698e-01
```

### Geometric Similarity

Fortunately, since the words still have the same relationships, they share a similar geometric structure. I applied PCA on the words "zero", "one", "two", "three", "four" from both models and visualized the relationships between the words.

<center><img src="https://raw.githubusercontent.com/PragmaticLab/EmbeddingMapper/master/pca_visualization/left.png" alt="Drawing" style="width: 400px;"/><img src="https://raw.githubusercontent.com/PragmaticLab/EmbeddingMapper/master/pca_visualization/right.png" alt="Drawing" style="width: 400px;"/></center>

We can see that the geometry is very similar, but not quite the same. Hint: The angle between 0 and 1 are different between the first and second model. 

Here is the illustration that Mikolov's PCA visualization from his [paper](http://arxiv.org/pdf/1309.4168.pdf), where the numbers' embeddings came from an English model and a Spanish model. 

<center><img src="{{site.imgrepo}}/word_translation_visualization.png" alt="Drawing" style="width: 1000px;"/></center>

This geometric similarity in the PCA visualization suggests that there is a fairly decent linear mapping between models of the same word relationships. 

### Training the Translation Mechanism

The next step is to learn a translation matrix to connect the two models. 

We can extract the training set by getting a small number embeddings from the source model and the target model. For my experiment, I used 2000 words. Mikolov trained on 5000 English words and their spanish counterparts via Google Translate. As a general rule, it's better to use the highest occuring or most common vocabuary to establish the mapping, because their embeddings are the most well defined. 

The actual training can be done easily through [Scikit-Learn's Linear Regression](http://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html).

The mapping is quite simple. 

```
[Original embeddings] dot [translation matrix] = [New embeddings]
```

If I am translating a 2000 500xdimensional embeddings to a 200 one.

```
[2000 x 500] dot [500 x 200] = [2000 x 200]
```

### Evaluating the Translation 

To evaluate the quality of the embeddings, we can use words that we didn't use for training. I recommend measuring how often the map of the old embedding can be mapped to the same word. 

For instance, if "one" is mapped to "one", "a" and "an" in the new space, it is a hit. However, if "one" is mapped to "time", "star" and "tree", it is a miss. 

### Applications

#### The method can be applied in many ways:
* Introducing new vocabulary to your model
* Translating between languages (e.g. English - French, Android - iOS)
* Increasing or decreasing the dimensionality of your embeddings
