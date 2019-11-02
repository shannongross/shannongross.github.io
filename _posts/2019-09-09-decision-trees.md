---
published: false

layout: post
title: Decision Tress notes
date: 2019-09-08
description:
fig-cation:
img: #books.jpg
tags: []
---
- TOC
{:toc}

# What are "Decision Trees"?
- leaf nodes represent the classification (decision)
- can work with categorical or numerical data
- Steps to building a decision tree
  - Split: partition the data into sets (e.g. by gender, by wealth status)
  - Prune: where the tree is too complex, make it simpler. This helps the algorithm do a better job of classifying new values.
  - Selection: select the shortest tree that fits the data.
- constructing a good one is al about trying to make a balanced tree
- in building a decision tree, our main task is to find the best set of rules to classify things. We judge how good our rules were by looking at the accuracy of things correctly classified.

- Decision trees are extremely intuitive ways to classify or label objects: you simply ask a series of questions designed to zero in on the classification.
- The trick, of course, comes in deciding which questions to ask at each step.
- Such overfitting turns out to be a general property of decision trees; it is very easy to go too deep in the tree, and thus to fit details of the particular data rather than the overall properties of the distributions they are drawn from.
- This notion—that multiple overfitting estimators can be combined to reduce the effect of this overfitting—is what underlies an ensemble method called bagging. Bagging makes use of an ensemble (a grab bag, perhaps) of parallel estimators, each of which overfits the data, and averages the results to find a better classification. An ensemble of randomized decision trees is known as a random forest.
- In this example, we have randomized the data by fitting each estimator with a random subset of 80% of the training points. In practice, decision trees are more effectively randomized when some stochasticity is injected in how the splits are chosen; this way, all the data contributes to the fit each time, but the results of the fit still have the desired randomness.


# common approaches
-  ID3, C4.5, CART

# What are their advantages?
- easy to interpret results
- computationally inexpensive
- can't use linear or logistic regression in situations where features interact with each other

# What are their disadvantages?
- prone to overfitting (combat this by pruning - combining the adjacent nodes that have low information gain)
- finding the best set of rules for splitting can be hard
- a single decision tree isn't very useful because its poor at generalizing. However, an ensemble (random forest) minimizes this weakness.

# Random forests
- a random forest is an optimized ensemble of decision trees

# Bagging, Bootstrapping, and Boosting
- Bootstrapping: sampling with replacement
    - some data is left out each time
- Bagging: creating a bunch of decision trees each trained on a different bootstrap sample of the dataset
  - guards against overfitting
  - making ensembles of decision trees in this way helps to bring down total error
- Boosting: combining trees to form a stronger predictive model. Built over time by adding trees that reduce error.
