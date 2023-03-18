---
layout: post
title: Clustering Big Data
date: 2022-12-04 14:12:39
tags: [Machine Learning, Big Data, Data Science]
---
## Clustering Big Data

*Unsupervised learning* refers to a class of machine learning algorithms which study unlabeled data to identify patterns. Uniquely, there is no data containing labels or class information nor the intervention of a human operator to provide instructions on the nature of the data. Instead, the machine identifies any underlying correlations or causal relationships by analyzing the provided data.

In an unsupervised learning process, the machine learning algorithm is left to interpret large data sets and address that data accordingly. The algorithm tries to organize that data in a manner that describes its structure. This could be through attempted grouping based on similarity or arrangement into a more organized structure. As more data is assessed, its ability to make decisions based on given data grows more refined.

*Clustering*<sup>[[1]](https://www.amazon.com/Elements-Statistical-Learning-Prediction-Statistics/dp/0387848576)</sup> involves grouping observational data exhibiting similarities across defined criteria into sets or clusters. Observations pertaining to a particular cluster are defined as bearing a stronger similarity within the cluster as opposed to outside members of a different cluster for the predetermined criteria. Clustering is useful for segmenting and filtering data into several groups before performing additional analysis to extract other interesting patterns.

The power of clustering emerges from the fact that with big data and multidimensional feature spaces, it grows exceedingly difficult for humans to visually discern patterns in unlabeled data without machine assistance. The algorithmic approach is efficient and eschews human intervention and thereby human limitations in processing multidimensional data where patterns are not immediately noticeable or comprehensible to the eye. It also avoids the imposition of human biases in the process, where generally pattern-seeking with preconceived expectations by human operators may lead to incorrect cluster identification.


### K-Means
**Figure 1.** *K-Means identifying (3) clusters*

K-Means clustering is one such algorithmic implementation which works by finding groups within the data. It then works iteratively to assign each observational data point to said groups in feature space.

Given a user-specified integer K, observational data points in n-dimensional feature space are organized into K unique clusters based on similarity. This similarity metric is usually generally calculated based on Euclidean distance.

K-Means categorizes unlabeled data by randomly placing K centroids in n-dimensional feature space. The distances between all points are calculated to each centroid’s position. Observations closest to a centroid are assigned to the cluster belonging to that centroid. The mean position of all points in each cluster is calculated, and the positions of each centroid is set to the mean position of all points in the cluster to which it belongs.

Cluster reassignment, mean calculation, and updating of centroid position ends with convergence to a specific position, where the position of the K centroids no longer change and the points are not newly reassigned to any clusters., i.e. data without defined categories or groups. 

Clustered observations exhibit unique associations which are understandable by humans through analysis post-clustering, as it becomes evident which range of features and realized values observational data have been segmented upon. Armed with this knowledge and insight, one can then begin to develop catered strategies and engage in decision-making targeting these segments.

### Reference

[[1] Hastie, Trevor, Robert, Tibshirani and J. H. Friedman, *The Elements of Statistical Learning: Data Mining, Inference, and Prediction*. New York: Springer, 2009.](https://www.amazon.com/Elements-Statistical-Learning-Prediction-Statistics/dp/0387848576)
