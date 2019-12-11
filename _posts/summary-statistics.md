---
published: false

layout: post
title: Problems with common statistical methods used in data science
date: 2019-10-16
description:
img:  
fig-caption:
tags: []
categories: [Tutorial]
---



1. TOC
{:toc}
{:.toc-styling}

# Summary Statistics
- your analysis is not going to give you meaningful results if you start by assuming that the data possesses characteristics that it doesn't have (such as being normally-distributed).
- some summary statistics are more robust than others, meaning that they are resilient against outliers in the data. This can help you answer the question, should I use the median instead of the mean?
  - the **median** is less affected by single outliers, which is often a useful characteristic. If you have an analysis where you don't want your results to be skewed by a single outlier, then using the median may be preferable over the **mean**.
  - because the **standard deviation** uses the square of the mean in its calculation, it's even more affected by outliers. A single, weird data point can cause you to think that the data is much more spread out than most of the points actually are. A more robust alterative is the **interquartile range**, which measures the spread in the middle 50% of the data, so it is not skewed by very high and low outliers.
  - when data are skewed to one side or the other (having a leading/trailing tail), using the mean and standard deviation are of much less value, inflating the role of outliers and unlikely to paint a fair picture of the data. If you have skewed data, having summary tables that include median and interquartile range are more appropriate.
  - Skewed data also means that your data is not normally-distributed and thus you should not use other statistical methods which require this distribution, such as hypothesis/parametric tests. There are many real-world cases where you are unlikely to obtain normal (or even symmetric) data distributions.

## Outliers
- don't be too scared of your outliers, or too quick to throw them away so that you can perform a hypothesis test
- these are important data points
- don't discard them simply because they're weird
- first, you need to verify that it was not some kind of data-entry error
- graphical/visualization methods are highly useful for recognizing outliers
- let the data lead you to the correct statistical method to use, rather than throwing away some values to force it to fit e.g. the normal distribution

## Sampling
The **population** is the entire set of things that you're making a statement about. For instance, this could be all the people in a country who lie below the designated poverty level. Or, the concentrations of a toxic pollutant in the blood of animals living in a catchment area. It is exceptionally rare for the analyst to have a data point for every single person/animal/etc. in the entire population, since it would be crazy expensive, invasive and time-consuming to collect. Instead, scientists work with a **sample** of the population, which is a subset that represents the whole population and is easier to work with.

### Transformations
- some believe that by transforming data, you're tweaking it to match your own preconceived notions. But transformation can be useful to get a dataset to yield symmetry and linearity.  

> "One unit of measurement is no more valid a priori than any other. For example, the negative logarithm of hydrogen ion concentration, pH, is as valid a measurement system as hydrogen ion concentration itself. Transformations like the square root of depth to water at a well, or cube root of precipitation volume, should bear no more stigma than does pH. These measurement scales may be more appropriate for data analysis than are the original units." ~USGS

- if you want to make a symmetric distribution out of an asymmetric one, you can transform or re-express values in different units. Different units can change the distances between how the values look when plotted.
- The logarithm is a commonly used transformation. "Logs of water discharge, hydraulic conductivity, or concentration are often taken before statistical analyses are performed."


## Point vs Interval Estimates
- point estimate: mean and median. on their own, don't give you any indication of how reliable they are.
- interval estimate: range that has a stated probability of containing the true population value. They give you the following information:
  - confidence intervals: the likelihood that the interval contains the true value (aka its reliability)
  - prediction intervals: "A statement of the likelihood that a single data point with specified magnitude comes from the population under study. "

Confidence and prediction intervals are not the same thing, even though they are related, and you can't use them for the same purposes. How to interpret a 90% confidence interval: "The true mean will be inside of this interval an average of 90% of the time"
- confidence level: probability that the interval contains the true value
- alpha level: probability that the interval will **not** contain the true value (alpha = 1- CI)


#### Confidence Intervals For The Mean
"For large sample sizes a symmetric interval adequately describes the variation of the mean, regardless of the shape of the data distribution. This is because the distribution of the sample mean will be closely approximated by a normal distribution as sample sizes get larger, even though the data may not be normally distributed. For smaller sample sizes, however, the mean will not be normally distributed unless the data themselves are normally distributed. As data increase in skewness, more data are required before the distribution of the mean can be adequately approximated by a normal distribution. For highly skewed distributions or data containing outliers, it may take more than 100 observations before the mean will be sufficiently unaffected by the largest values to assume that its distribution will be symmetric. 

- This property is called the Central Limit Theorem (Conover, 1980). It holds for data which follow a distribution
having finite variance, and so includes most distributions of interest in water resources."

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


<!--
Since a distribution represents a range of possible outcomes, the simulation is run many different times. With each replication, a different possible value is drawn at random from the probability distribution. After a large number of replications, the result is another distribution representing the set of possible outcomes.



### Lognormal
- not symmetric
- only positive values
- values can't be negative but can extend infinitely in the positive direction
- EX: real estate property values, stock prices, oil reserves



### Triangular
- define the minimum, maximum, and most likely value.
- EX: past Christmas sales, inventory levels

### Discrete
- define the likelihood of different values
- EX: 10% chance of getting an A, %25 chance of getting a B, %45 chance of getting a C, %20 chance of other grade.

### The exponential distribution
- occurs when we look at interarrival times (the time between events)

- *The Gaussian Distribution* - describes the distribution of averages, requiring you to know the variance upfront. It's for the distribution of a sum of "independent, symmetric, random variables"
- you have measurements that are all independent and identically distributed

 -->


 <!-- ## Probability distributions
 ### Discrete
     When the probability distribution function (Z) is discrete, then the distribution takes the form of P(Z = k), measuring the probability that Z takes on value k.
     - Popular **probability mass functions**  (e.g. Poisson)
     Note: A weakness of the probability mass function is that as the number of values you have goes up, the probability of each value decreases. Thus, the effects of random noise grows stronger
     -Probability Mass Functions (PMF) A **PMF** maps from each value to its probability.

 ### Continuous
     When Z is continuous, use a **probability density function** (e.g. exponential density)
     - if the variable can assume an infinite number of values between the max and min
     - "distribution parameters are values that apply to entire populations. Unfortunately, its generally impossible to measure an entire population. So you can use random samples to calculate estimates of these parameters"

 #### Cumulative distribution functions (CDFs)
     - the *percentile* is the fraction of people who scored the same or lower than you.
     - the *cdf* is a function that maps from a value to a percentile rank. This function is the fraction of that is less than or equal to x
       - PRO: especially good for comparing distributions -->
