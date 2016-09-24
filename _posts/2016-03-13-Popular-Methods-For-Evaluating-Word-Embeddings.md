---
layout: post
category : tutorial
tags: word2vec, wordembedding
tagline: "Evaluating word embeddings"
excerpt: Evaluating word embeddings

---

## Evaluating Word Embeddings

### Methods

* word-pair similarities
	* Get human tagged similarity scores for any 2 words
	* Get the correlation between the model generated and human tagged scores
* word relatedness classification
	* Have a 50/50 split of word-pairs that are related and unrelated
	* Use the model generated scores to predict relatedness
* rare word similarities
	* Sample words from different frequency bins to construct word-pairs
	* Focused on testing embeddings with low frequencies
* cross domain similarities
	* Construct word-pairs from different domains (e.g. nouns and verbs)
* analogies
	* Mikolov introduced analogy-based word pairs
	* (e.g. man + king - woman => queen)
* sentence completion
	* Correctly predict missing word from given list of 5 other words
	* Average the embeddings for the given words to calculate the closest cosine similarity
* sentiment analysis
	* Train a logistic regression classifier on the average of word vectors
* TOEFL synonyms
	* Takes inspiration from standardized tests such as TOEFL
	* A given word needs to be matched to its closest synonym from 4 given options


### Visualization

* t-SNE
	* pick seed words (e.g. eye, cough, surgery, tumor)
	* get n words that are most similar to the seed words
	* visualize in 2d using t-SNE
* antonyms and synonyms

### Resources

* [WordVectors.org](http://wordvectors.org/) is a CMU based service that provides quick online testing of embeddings against 10+ datasets
