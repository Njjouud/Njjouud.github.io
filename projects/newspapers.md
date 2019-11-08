---
layout: page
title: News Papers’ Articles Aggregator and Recommender
---


### Purpose
To develop a real-time news aggregator and recommender system.

### Why aggregating/clustering news? 
Today we are awash in too much news so it can be hard to get quality information. The goal is to develop a system that automatically determines topics from multiple news sources. 

### Work Stages

#### Data Acquisition

I collected articles in two ways:
1. By using RSS (Rich Site Summary) and parse it into json using rss2json API.
2. If a RSS-feed link is not provided, I used python newspaper library to extract articles.
This is an example of RSS-feed:
![rss]({{ site.url }}/images/rss_feed.png)

#### Data Sources

Data has been collected from the following sources:
![sources]({{ site.url }}/images/news_sources.png)


##### Data Preprocessing

I started by removing duplicates articles and then converting text to lower-case, excluding escape characters, html tags, punctuation and symbols and digits, excluding stop words and non-English words.
After that I started tokenizing data (splitting the article into list of words) to stemmed out the words

##### Text Similarity Measure

Using Count Vectorizer 

##### Dimensionality Reduction

I tried three techniques to reduce the dimensionality Latent Dirichlet Allocation (LDA), Latent Semantic Analysis (LSA), and Non-negative Matrix Factorization (NMF), but I found that NMF works better for my data so I sticked to it.
Here is a sample of topics:
![bf_trump]({{ site.url }}/images/topic_bf_trump.png)

And since many topics were dominated by **Trump**, So I made the design decision to remove his presence from the news aggregation and clustering process in an attempt to get cleaner news topic clusters. 
![trump]({{ site.url }}/images/trump.png)
Here is a sample topics after removing the presence of **Trump**.
 ![af_trump]({{ site.url }}/images/topic_af_trump.png)

##### Clustering

Before I started clustering data I normalized it to standardize the similarity distance between articles. After that I used Elbow technique to find the optimum number of clusters. 
![elbow]({{ site.url }}/images/elbow.png)
Then I clustered the articles using K-Means Model with 6 clusters. And here are the wordclouds for each cluster:
Cluster #1 which is obviously about Baking:
![wc1]({{ site.url }}/images/wc_1.png)

Cluster #2 which is about Business:
![wc2]({{ site.url }}/images/wc_2.png)

Cluster #3 which is about Military:
![wc3]({{ site.url }}/images/wc_3.png)
 
Cluster #4 which is clearly about Movies and TV Shows:
![wc4]({{ site.url }}/images/wc_4.png)

Cluster #5 which is basically a collection of Spanish words and you may be wondering how come there are spanish words and I already said that I excluded any non-English words but since some Spanish words are written in English letters:
![wc5]({{ site.url }}/images/wc_5.png)
 
Cluster # 6 which is about Business too:
![wc6]({{ site.url }}/images/wc_6.png)
 
 
##### Recommender System

I began generating unique id for each article and then I built a function that returns the top topic for read article:
![top_topic]({{ site.url }}/images/news_top_topic.png)*Topic 42: bar, audio, sound, get, one*
And then I built a recommender system that recommends articles in two ways:
* Either by getting the top article about a specific topic.
![top_topic]({{ site.url }}/images/top_article.png)*Topic 42: bar, audio, sound, get, one*

* Or recommending an article based on a read article.
![top_topic]({{ site.url }}/images/top_art_top_topic.png)*Topic 42: bar, audio, sound, get, one*


### Conclusion and Future Work

- Apply more advanced clustering models.
- Build a flask application.



Have questions or suggestions? Feel free to [email me](mailto:njoud.algifari@gmail.com).

Thanks for reading!
