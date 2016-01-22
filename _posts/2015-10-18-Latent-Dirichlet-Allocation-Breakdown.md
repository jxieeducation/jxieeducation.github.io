---
layout: post
category : paper
tags: LDA TopicModeling
tagline: "A Breakdown of Latent Dirichlet Allocation"
excerpt: Topic Modeling is a type of natural language processing technique to identify patterns within the text. Latent Dirichlet Allocation is a topic modeling algorithm that tries to identify topics within a corpus. In this post, I share some of my results from the Enron corpus and tips on how to interpret the model.
---

##Latent Dirichlet Allocation & Topic Modeling  
  
Topic Modeling is a type of natural language processing technique to identify patterns within the text.  

Latent Dirichlet Allocation is a topic modeling algorithm that tries to identify topics within a corpus.

---

###Example
Here's an experiment that I ran a while ago on the [Enron corpus](https://archive.ics.uci.edu/ml/datasets/Bag+of+Words).

Identified Topics:
* corporation
`(company, business, firm, market, services, investment, investor)`
* online retail
`(click, page, free, offer, travel, database, final)`
* energy business 
`(power, energy, california, electricity, market, bill)`
* organization
`(meeting, attached, contract, review, customer, group, report)`
* sports sponsorship
`(game, texas, team, play, think, going, against)`

*The beauty of LDA lies in how it figures out the relationship (topics) between words in documents*

--- 

###Algorithm

- The only parameter for LDA is how many topics you think is in the corpus. For the Enron dataset, the optimal number is 5.
- We initialize every single word in the documents (each email is a document) with a topic according to the Dirichlet distribution (it's similar to just assigning topics randomly)
- For every word in every document, we try to reassign topics by looking at several things
  * how is this word distributed across all the topics? 
  * how are all the topics distributed across this document? 
  * we multiply the previous two distributions to get a distribution for how to reassign the topic
- repeat the previous step many many times

---

###Intuition

After running the algorithm many times, eventually each word is assigned to a single topic. And documents are assigned topics (e.g. 40% fruits, 60% sports).

Words that often appear in the same documents end up in the same topic. 

Some notations: 
* $D, W, Z$ are the document, word and topic respectively
* $\Pr(Z|D,W) = \dfrac{number\,of\,words\,in\,topic\,Z}{total\,number\,of\,words\,in\,Z} * number\,of\,words\,in\,D\,that\,belong\,to\,Z$ 

This equation works because after each iteration 1) words slowly become more common in topics where they are already common 2) topics become more common in docments where they are already common.

This graph shows that the log likelihood decreases through iterations.

![lda_log_iteration]({{site.imgrepo}}/lda_log_iteration.png)

Although the algorithm knows nothing about what words mean, it groups words together smartly by looking at the distribution of words across documents. 


###Choosing the best number of topics

The LDA algorithm has a loss function that punishes entropy in the topic assignments. By iterating through the number of topics, we simply choose the best score. 

![lda_log_N]({{site.imgrepo}}/lda_log_N.png)

I chose 5 for the Enron dataset.

For more information on the application of LDA, [here](https://www.quora.com/What-is-a-good-practical-usecase-for-Topic-Modeling-and-LDA)
