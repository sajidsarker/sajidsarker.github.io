---
layout: post
title: Recommender Systems
date: 2022-10-10 23:59:59
tags: [Machine Learning, Artificial Intelligence]
---
## Recommender Systems

A **recommender system** or engine, is a class of information filtering algorithms which predicts preferences users have for a specific item<sup>[[1]](https://www.amazon.com/Elements-Statistical-Learning-Prediction-Statistics/dp/0387848576)</sup>. These algorithms are popular in search engines and in e-commerce platforms offering product recommendations. The heterogeneity in filtering methods illustrates the variations in goals with which preferences are determined for users.

Recommender systems initially suffer from the ‘cold start’ problem, where in a system containing information on items and users and the matrix of their preferences for said items, much of the data of ratings will not have been gathered from users beforehand in order to make accurate and relevant predictions. This is usually alleviated when a new user joining a system is asked to initially rate a series of products (frequently comparatively), or provide a broad set of categories in which they exhibit personal interest and from which they would like to receive recommendations.

![recommender-system](/docs/assets/images/[...].png)

**Figure 1.** *User-item ratings matrix*

As users participate within the system and offer more information on their preferences for items, the better the filtering system becomes in accurately predicting user ratings based on events such as the introduction of new products to the system or arrival of new users to the system.
A similarity metric is derived between users or between products to analyse how close different users are in terms of their taste or how close different products are in terms of their characteristics.

### Collaborative Filtering
**Collaborative filtering** operates on the assumption that users who tend to have rated products similarly in the past, are likely to share similar preferences. Accordingly, when a user A has high ‘similarity’ to another user B with a pre-existing rating for a product, then it is expected that user A will share the same preference for the product as user B and give the product a similar rating. The system then recommends products to a user based on high ratings given by other similar users sharing the same preferences.

### Content-based Filtering
**Content-based filtering** adds the caveat that more information is known of the product’s characteristics, attributes, function, and/or utility within the system, and the similarity metric is calculated between different products on these dimensions. A user’s preferences exist in the form of ratings for products (and their attributes), and products with high ‘similarity’ are given similar ratings for that user for more frequent recommendation.

### Session-based Filtering
**Session-based filtering** arose as a counter to collaborative and content-based filtering, due to the assumptions with which the latter algorithms were developed. In both the prior algorithms, the underlying assumption is that the entire history of user preference is critical for determining future recommendations. The impact of time-sensitivity and recency is thereby underestimated. It is often more important that a user’s short term preferences be weighted more when the algorithm makes recommendations. Furthermore, another assumption is that users will always provide their ratings for products over time, when it is much likelier that within a system, this critical data may not always be reliably collected.

For example, what a user has recently viewed or recently purchased can be critical in curating better recommendations relevant to a user’s present interest. Additionally, being offered better and more time-relevant recommendations would yield an improved user experience.

In session-based filtering, a recent set of unique user interaction, browsing, and search activity is categorised as a singular session. The activity data collected during a session is used as the generating set of products weighted for importance on which recommendations are to be predicted and made.

### Hybrid Recommender Systems
**Hybrid recommender systems** are unique in that they are built as a composite of collaborative, content-based, and other filtering algorithms. Both collaborative filtering and content-based filtering have strengths and weaknesses, some of which are identified and rectified through session-based filtering. Collaborative filtering needs significant feedback from users to function optimally, while content-based filtering requires proper cataloguing of product attributes and descriptions. Often recommendations are produced as a mix of the output from the various filtering algorithms along with other types of input, such as user location or time of day.

Recommendation sets of various algorithms may be weighted through scoring prior to being presented to the user. A mix of different recommender systems and their results are provided together to users all at once. Sometimes results from one algorithm are used as the input for another algorithm before being presented to the user. These constitute just some of the unique hybrid strategies in current use.

There are various different similarity metrics which can be used to calculate how close users or products are in characteristics. Some similarity metrics which can easily be calculated include *Euclidean Distance*, *Jacard Similarity*, *Pearson Similarity*, *Cosine Similarity*, and *Dot Product*.

### Reference

[[1] Hastie, Trevor, Robert, Tibshirani and J. H. Friedman, *The Elements of Statistical Learning: Data Mining, Inference, and Prediction*. New York: Springer, 2009.](https://www.amazon.com/Elements-Statistical-Learning-Prediction-Statistics/dp/0387848576)
