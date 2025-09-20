---
title: "K-means by another means"
excerpt: "Success! There is machine learning happening on my Apple ]\[+."
tags:
  - K-means
  - machine learning
date: 2025-09-20
---

Wait. Does k-means count as machine learning? Yes. It does.

[CS229](https://cs229.stanford.edu/){:target="_blank"} is the graduate-level machine learning course I took at Stanford as part of the [Graduate Certificate in AI](https://www.linkedin.com/pulse/graduate-certificate-ai-achievement-unlocked-mark-cramer/){:target="_blank"} that I received back in 2021. While k-means is my choice as the easiest to understand algorithm in machine learning, it was taught as the introductory clustering algorithm for unsupervised learning. As a TA (technically a 'course facilitator') for [XCS229](https://online.stanford.edu/courses/xcs229-machine-learning){:target="_blank"}, which I have been doing since 2022 and most recently did this Spring, I know that it is still being taught as part of this seminal course in AI.

## We have liftoff!

Unlike [previously](/apple-2-blog/synthesizing-data/) where I saved the result for the end, let's start by taking a look at the algorithm in action!

[![Video of Apple][+ running k-means](https://img.youtube.com/vi/xi876Gqt4jk/0.jpg)](https://youtube.com/shorts/Cy0wMMLObVA "Video of Apple]\[+ running k-means"){:target="_blank"}

For debugging purposes, to speed up execution, I reduced the number of samples in each class to 5. That's obviously pretty small but you can see the algorithm iterating. At the end of each loop I draw a line between the latest estimates of cluster centroids. The perpendicular bisector of these segments are the decision boundaries between the classes, so I draw that, too. Some of the code was written to handle more than two classes but here there are only two which makes this relatively easy.

## K-means explained

[K-means clustering](https://en.wikipedia.org/wiki/K-means_clustering){:target="_blank"} aims to partition \\(n\\) observations into \\(k\\) clusters in which each observation belongs to the cluster with the nearest mean, called the cluster centroid. In pseudo-code it looks like this:

|Step|Description|
|--|--|
|Initialize|Produce and initial set of k cluster centroids. This can be done by randomly choosing k observations from the dataset.|
|Step 1 - Assignment| Using Euclidean distance to the centroids, assign each observation to a cluster.|
|Step 2 - Update| For each cluster, recompute the centroid using the newly assigned observations. If the centroids change (outside of a certain tolerance), go back to step 1 and repeat.|

Ezpz.

The math is also very easy. In step 1 the distance between two points, \\(x\\) and \\(y\\), is simply \\(\sqrt{(x_0 - y_0)^2 + (x_1 - y_1)^2 + \cdots + (x_d - y_d)^2}\\). Since we're just comparing distances it's not even necessary to take the square root. In step 2, the centroid is simply the sum of all the points divided by the number of points.

## Implementation

{to be written...}