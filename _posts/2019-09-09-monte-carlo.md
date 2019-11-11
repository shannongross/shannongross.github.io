---
published: false

layout: post
title: Monte Carlo notes
date: 2019-09-08
description:
fig-cation:
img:
tags: []
categories: [Modeling]
---
- TOC
{:toc}

# What is "Monte Carlo" simulation/method?
- it is a computational method for assessing risk/uncertainty to support decision-making
- gives the decision-maker a range of possible options and the probability that they will occur
- gives you a better understanding of the risk involved with a particular decision
- gives you the extreme options (going "all in" or "playing it safe"), along with middle-ground options
- You build a Monte Carlo simulation the same as any other model, except for any parameter where you are unsure of its value, you substitute a *probability distribution* instead. Since a distribution represents a range of possible outcomes, the simulation is run many different times. With each replication, a different possible value is drawn at random from the probability distribution. After a large number of replications, the result is another distribution representing the set of possible outcomes.

## Common probability distributions
### The Gaussian (Normal) distribution
- characterized by the mean and SD
- just give the mean and standard deviation to create this bell-shaped curve.
- examples include: people's heights, energy prices?
- *The Gaussian Distribution* - describes the distribution of averages, requiring you to know the variance upfront. It's for the distribution of a sum of "independent, symmetric, random variables"
- you have measurements that are all independent and identically distributed

### Lognormal
- not symmetric
- only positive values
- values can't be negative but can extend infinitely in the positive direction
- EX: real estate property values, stock prices, oil reserves

### Uniform
- all values have an equal chance of occurring
- simply give the max and min
- EX:

### Triangular
- define the minimum, maximum, and most likely value.
- EX: past Christmas sales, inventory levels

### Discrete
- define the likelihood of different values
- EX: 10% chance of getting an A, %25 chance of getting a B, %45 chance of getting a C, %20 chance of other grade.

### The exponential distribution
- occurs when we look at interarrival times (the time between events)

### Poisson
- good for *count* data

### Bernoulli Trials and The Binomial Distribution
When a random trial can only end in one of two outcomes (success or failure), it is a **Bernoulli Trial**.
- Probability of success = p
- Probability of failure = 1 - p






# Why do we use it?
- rather than running a simulation and getting a single point-value outcome, Monte Carlo allows us to obtain a range of outcomes and the likelihood that they will occur. This is important for when we are dealing with uncertainty, since obtaining a single point-value estimate would present false certainty about the answer.
- while obtaining a solution in the form of a distribution might seem like it would complicate matters, an advantage of this is that it is easy to create graphs that display a range of outcomes and their probabilities.
- Monte Carlo simulation makes it easier to perform **Sensitivity Analysis**, so that we can see which parameters impact the outcome the most.

## Extensions to the Monte Carlo method
- rather than sampling randomly, we could use a technique such as **Latin Hypercube Sampling (LHS)** to sample from the distribution. LHS is useful for ensuring that a better coverage is achieved during the sampling process.
- In some cases, a parameter may be so unknown, that it is not even possible to use a probability distribution to characterize it. For instance, say there is an outbreak of a brand new disease in a remote country. A team of international doctors fly in to assist, but they are uncertain about many characteristics of the disease and rumors are spreading that the disease is a Western conspiracy. What proportion of the infected people will go to the hospital for treatment? The truth is, we really don't know. We could guess half of people, but it would just be a guess. We could try different probability distributions, but it could be difficult without enough information or previous experience to conclude which distribution is the "right" one. Even more confusing, what if local leaders insist that there is no outbreak occurring? Not only are you unsure of the appropriate probability distribution but you're now put into a position of a mediator - having to discuss with local and international leaders whether the relationship even *exists*. This is a case of **deep uncertainty**, and may require different methods to analyze.

#### Standard Probability Models - Conclusion
How should uncertainty be handled when a system has some kind of randomness? There may be a range of outcomes that fall under some probability distribution. What you'd like to do is reduce the uncertainty band around some output to its "typical" value.

NOTE: Using a standard probability model may not work for all types of uncertainty, especially [deep uncertainty].
