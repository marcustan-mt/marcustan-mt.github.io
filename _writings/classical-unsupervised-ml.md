---
title: "Classical Unsupervised ML — Dimensionality Reduction and Clustering"
subtitle: "Exploring clustering and dimensionality reduction on Wine and Apple Quality datasets"
category: Machine Learning
tags: [machine-learning, unsupervised, clustering, pca, ica, k-means, em]
order: 7
---

An exploration of unsupervised learning techniques, focusing on clustering and dimensionality reduction using the same Wine Quality and Apple Quality datasets from the supervised learning analysis.

## Clustering Methods

### K-Means Clustering

K-Means partitions a dataset into K clusters by iteratively assigning points to nearest centroids. This hard clustering approach is simple and fast but sensitive to centroid initialization — run it multiple times and pick the best result.

### Expectation Maximization (EM)

EM takes a probabilistic approach using soft clustering with Gaussian Mixture Models. It employs iterative Expectation and Maximization steps for parameter optimization. Unlike K-Means, each point gets a probability of belonging to each cluster rather than a hard assignment.

## Dimensionality Reduction Techniques

### Principal Component Analysis (PCA)

PCA identifies directions of maximum variance to reduce dimensionality while preserving data structure. It's the go-to first step — fast, interpretable, and enables reconstruction of the original data.

### Independent Component Analysis (ICA)

Best understood through the "cocktail party" analogy: multiple microphones record overlapping conversations, and ICA separates them into independent source signals. Unlike PCA's variance focus, ICA targets statistical independence.

### Random Projection

A faster but less precise technique using random matrices for projection. It prioritizes computational speed over accuracy — useful for very large datasets where PCA becomes expensive.

## Critical Findings

EM clustering proved sensitive to outliers, effectively functioning as an anomaly detection tool. An important interaction effect: combining ICA with EM clustering on the Apple Quality dataset actually **degraded** performance because EM requires Gaussian-distributed features — which ICA explicitly removes.

**Recommendation:** Proactively manage collinearity and outliers during preprocessing. And be mindful of how your pipeline stages interact — a technique that works well in isolation can hurt when combined with incompatible downstream methods.
