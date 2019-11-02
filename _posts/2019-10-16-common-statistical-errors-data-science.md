---
published: false

layout: post
title: Problems with common statistical methods used in data science
date: 2019-10-16
description:
img:  # Add image post (optional)
fig-caption:
tags: []
---
# Overview
- A. The trouble with Standard Deviation
- B. Using Least Squares methods
- C. P-values and Z-scores
- D. What to know about the main distributions
- E.


# A. Standard Deviation
Everybody knows that 1SD contains 68% of data, 2SD contains 95% of the data, and 99.7% within 3SD. The SD is easy to calculate and use for a discussion about the spread of data.
- Just because it is easy though, does not mean the SD is always a good metric for discussing spread around the mean.
- PROBLEMS W SD:
  - ONLY works if the distribution is Gaussian
  - if the distribution is strongly asymmetrical, then mean and SD are no longer appropriate (you can calculate them, but they wont give you very meaningful insight)
    - for distributions that are very asymmetrical/weird you may want to use the inter-quartile range instead

When you think your data is not symmetric and/or has significant outliers, it is better to use **median and percentile** instead of **mean and standard deviation**. While mean and variance has historically been more popular because of how simple it is to calculate by hand, the rise in computing availability today means that it is often more practical and useful to work with percentiles.

# B. Least Squares
#### Statistical Parameter Estimation
- we have input (x) and a response (y). The response is related to the input by some function y = f(x, {a,b,c} + e). Where a,b,c are a set of some parameters and e reflects the idea what the actual measurements are affected by some ransom noise. Thus, the response we measure is a combination of the actual values and a noise term. So how to choose the right a,b,c to achieve a "good fit"? The usual answer is to choose them so that the noise term is minimized i.e. lowest total mean square error.
- Keep in mind: you are able to find not only estimates of {a, b, c}, but also *confidence intervals*
- estimating the points on their own is really not that useful. How sure are you that a = 8.26? Do you think you could by off by a couple decimal points or a couple orders of magnitude?
- Problem: in most applications, people try to use least-squares to "fit" a formula to a bunch of data points (e.g. because they seem to fall along a line). In this use however, there is no random noise component, thus we cannot apply statistical arguments it. We can't say something about our confidence in the fit, since the errors are not randomly generated. Statistical goodness-of-fit is inappropriate
- Problem is that the least-squares method forces us to state the form of the function we are trying to fit. If we guess this wrong, then the results will be bad.
- Alternatives:
  - Nonparametric approaches such as splines or LOESS. Useful because you can find a smooth curve without specifying a certain functional form of the data.
  - Local interpolation is good if you don't need a global expression, but just want to approximate based on a few nearby points.

# C. P-values and Z-scores
## P-Values
Look at the tail of the normal distribution. The p-value is the probability that if you randomly pick a value from the population, that it will be greater than that level.
- when a p-value is less than alpha, it means that the outcome is statistically significant
- the alpha is just some threshold p-value (set at 0.05 for unknown reasons). If the area under the curve of a certain p-value is less than the alpha value, this is considered to be so rare an event that we call it 'statistically significant'.
- when the p-value is greater than the alpha, we 'fail to reject the null hypothesis'. In other words, the boring finding is more likely.
[ASA warning on Pvalues](https://www.nature.com/news/statisticians-issue-warning-over-misuse-of-p-values-1.19503?WT.mc_id=TWT_NatureNews&error=cookies_not_supported&code=2edb6732-0d05-48bb-a104-8c5e1e9ebf88)
A **p-value** represents the strength of the evidence in a hypothesis test (and to help soften the hard division between significant and not). It describes the probability of getting a
-  "In other words, the P value is the probability of being wrong when asserting that a difference exists."
- smaller p-values are interpreted to mean higher significance. Meaning that the current (null) hypothesis may not explain the observation. In other words, the null hypothesis is rejected if the probability is below a small (arbitrary) value known as the level of significance (often 0.05 by convention).

### P-value alternatives
(1) **Confidence intervals**: when we want to express how sure we are that our observation (p-hat) is close to the true value of the parameter (p). So we seek an interval around p-hat such that in 95% of samples, the true mean p will lie inside the interval. Again, 95% is arbitrarily chosen, but this method may be better suited to describing the magnitude of an effect.
  - in contrast to hypothesis testing (which relates to a single conclusion of significance vs no significance), confidence intervals provide a range of plausible values for your population
(2) **likelihood relationship**:
(3) **Bayes factors**:

## Z-Test (Similarity Test)
Is a sample similar to a population or not? Using classical statistics, the approach would be as follows:
1. generate a null and alternate hypothesis
2. calculate the z-score
3. determine the p-value
4. compare p and alpha
5. interpret the outcomes


# D. What to know about the main distributions

**The Four Sampling Distributions**
- *The Gaussian Distribution* - describes the distribution of averages, requiring you to know the variance upfront. It's for the distribution of a sum of "independent, symmetric, random variables"
- *The chi-square Distribution* - describes the sum of squares of Gaussian variables. Is used to describe the distribution of variances. Requires us to know the number of degrees of freedom to evaluate it.
- *Student t distribution* -
- *Fisher's F Distribution* - use this if you want to compare two variances against each other (to see if they are the same)

With all four, you have measurements that are all independent and identically distributed

## Probability distributions
### Discrete
When the probability distribution function (Z) is discrete, then the distribution takes the form of P(Z = k), measuring the probability that Z takes on value k.
- Popular **probability mass functions** that consistently appear (e.g. Poisson)

### Continuous
When Z is continuous, use a **probability density function** (e.g. exponential density)

#### Probability Mass Functions (PMF)
A **PMF** maps from each value to its probability.
- CON: as the number of values you have goes up, the probability of each value decreases. Thus, the effects of random noise grows stronger

#### Cumulative distribution functions (CDFs)
- the *percentile* is the fraction of people who scored the same or lower than you.
- the *cdf* is a function that maps from a value to a percentile rank. This function is the fraction of that is less than or equal to x
  - PRO: especially good for comparing distributions
