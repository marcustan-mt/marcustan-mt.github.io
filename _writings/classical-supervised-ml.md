---
title: "Classical Supervised ML (Classification) — Decision Trees, Boosting, Neural Networks, KNN, SVM"
subtitle: "Comparative analysis of five classical algorithms on Wine and Apple Quality datasets"
category: Machine Learning
tags: [machine-learning, classification, decision-trees, adaboost, neural-networks, knn, svm]
order: 6
---

A comprehensive comparison of five classical machine learning algorithms using two datasets: Wine Quality and Apple Quality (~4,000 rows, 8-11 features each).

## Datasets

- **Wine Quality** — Multi-class classification with significant imbalance (92% concentrated in quality levels 5-7)
- **Apple Quality** — Binary, balanced classification

The contrast between these two datasets is deliberate: one stresses class imbalance handling, the other provides a cleaner baseline.

## Algorithm Analysis

### Decision Trees

Use greedy optimization approaches that struggle with complex relationships. Performance plateaus at higher depths — increasing `max_depth` and `max_nodes` yields diminishing returns beyond a certain point. Simple to interpret but limited in expressiveness.

### AdaBoost

Demonstrates resilience to overfitting through exponential loss functions. Wine quality required approximately 600 trees before error stabilization, while apple quality converged much faster. The sequential learning approach means each new tree focuses on previously misclassified samples.

### Neural Networks

Achieved the **highest recall scores** (0.76 for wine, 0.97 for apple) by effectively handling imbalanced classes, collinear features, and outliers. The advantage comes from three mechanisms:

1. Effective imbalanced class handling via gradient consideration
2. Collinear feature tolerance through regularization
3. Outlier resilience when outliers comprise less than 15% of training data

### KNN

Sensitive to outliers. Wine quality required 25 neighbors versus just 4 for apple quality to buffer outlier effects. This sensitivity makes K selection critical — and dataset-dependent.

### SVM

RBF kernels outperformed polynomial kernels through distance-weighted approaches. Higher polynomial degrees caused overfitting — a reminder that kernel choice and degree are not "set and forget" hyperparameters.

## Key Findings

Neural Networks proved superior across both datasets, primarily because of their ability to handle the messy realities of real data: class imbalance, collinearity, and outliers. The gap was especially pronounced on the Wine Quality dataset where these challenges compound.
