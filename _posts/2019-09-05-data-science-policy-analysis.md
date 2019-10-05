---
published: false

layout: post
title: "Learning data science for policy analysis"
date: 2019-09-05
description: Tips and tricks about learning data science for policy analysis problems.
img:
fig-caption:
tags:
---
# Why Python?
Python is a free and powerful scripting language that will be your bread & butter as a data scientist. It's short and intuitive commands make reading the code simple, while its open-source nature means that powerful modules built by others are at your disposal. Because it is popular and widely used, there are many help guides and stack overflow answers to support your questions. Python's capability for policy analysis problems rests largely with its ability to handle huge amounts of data. Policymakers may have large-scale questions about future trends among their constituents and key issues, and python makes it easy to perform powerful tasks to answer their questions. Because python connects well with geospatial tools, database systems, and other applications, it is powerful and easily extendable.



# Data Analysis Fundamentals

### Jitter Plots
When your data is coarse-grained or integer-valued, many of the data points may lie on top of one another on a plot. **Jittering** is a technique where you shift every value by a small random value in order to better visually identify interesting clusters.

### Histograms
The shape of a histogram is likely familiar to you, but it is important to keep in mind that the result of a histogram does not depend only on the dataset, but also on the **bin size** and the **bin alignment**. Appropriate choices of these two key parameters are important to get the right amount of detail in the visualization. There is no hard and fast rule for what these parameters should be set to, so be sure to try out a few different combinations. As a starting point, you may consider using **Scott's Rule** to set the bin width (if your distribution is approximately Gaussian):

$$
  bin width = \frac{3.5 \times \varphi}{\sqrt[3]{n}}
$$

where $$ \varphi $$ is the standard deviation and *n* is the number of samples (points)

For bin alignment, remember to consider where the edges of the bins should be aligned (e.g. centered on the integer intervals or with the edges aligned with the intervals).

Table X: Pros and Cons of the Classical Histogram

| Advantages |  Disadvantages |
| --- | --- |
| Extremely common | Visualization is nonunique (i.e. dependent on parameters such as bin size) |
| --- | --- |
| Intuitive to interpret | Loses information when displaying data as bins rather than as points |
| --- | --- |
| Easy to generate | Does not handle outliers well |
| --- | --- |
| Histograms are useful because they make the most frequent values immediately apparent | But they are not the best choice for comparing two distributions.|


### Kernel Density Estimates (KDEs)
As opposed to classical histograms, you can't easily generate a KDE with a pen and paper - their popularity has risen with the increased availability of computational power.

**Kernel**: a smooth, strongly peaked curve that covers each data point. The most common function used to generate the KDE curve is Gaussian, but valuable alternatives such as Box and Epanechnikov kernels exist.

The most important parameter of a KDE curve is the *bandwidth*, which results in a tradeoff between height and width of the curves. Setting this parameter involves some trial and error - you want the curve to be detailed enough to not hide important information and yet enough smoothness to ensure the curve is not overfitted.

The main reason both histograms and KDEs are so popular is because they are easily interpreted - they give us an intuitive explanation for how likely we are to find a data point of a certain value.

### Cumulative Distribution Functions (CDF)
A **CDF** tells us what fraction of points occur below the value *x*. An advantage of using a CDF instead of (or alongside of) a KDE is that KDEs can be misleading - the human eye automatically senses the largest peak and assumes that "most" points gravitate around this value. CDFs can make it clear when this is not the case - spreading out the total area under the curve in a different way than the KDE (i.e. without binning).

Why use a CDF? They are useful for questions like: *what fraction of points fall between x1 and x2?* because you can simply read the answer off the x-axis. Additionally, CDFs can help you consider the way a distribution is balanced with respect to its tails.

While CDFs are generally less intuitive than the KDE - creating them can be an advantageous supplement to your data analysis process. For instance, CDFs may provide visual information that is less noisy and often more faithfully represented.

## Summary Statistics
The experienced data analyst should have enough familiarity with statistical concepts such as mean, standard deviation, and percentiles to be wary of relying on them. These summary statistics are popular and easy to calculate, however they are based on assumptions that must be clearly understood and articulated if they are to be applied appropriately.

**Important Assumptions**
- Summary statics are only relevant to **unimodal distributions**. When the data contains more than a single peak, concepts like mean and mode will give you results will *seem reasonable* but are actually misleading.
- Summary statistics work well when the data is symmetric, with a central peak, and without any crazy outliers. In reality, most data sets you are likely to encounter will violate one of these assumptions.

When you think your data is not symmetric and/or has significant outliers, it is better to use **median and percentile** instead of **mean and standard deviation**. While mean and variance has historically been more popular because of how simple it is to calculate by hand, the rise in computing availability today means that it is often more practical and useful to work with percentiles.

- *variation* describes the behavior within a variable
  - its usually a bit harder to interpret than standard deviation, because the result of variance is in units squared (e.g. weeks^2, mph^2), which doesn't make a lot of sense. Thus it's not a great summary statistic.
- *covariation* describes the behavior between variables
- *central tendency* when values tend to cluster around a point (use *modes* if there is more than one cluster)
- *spread* how much variability exists
- *tails* do the probabilities drop off
- *outliers* extreme values far away from the mean
- *mean* be careful - this value is misleading when there is no "typical" instance (i.e. a lot of variance or spread)

### Box and Whisker Plots
The popularity of box and whisker plots lies in its ability to convey a lot of statistical information in one compact visualization.

When should you use a box and whisker plot? It's best when you are comparing multiple distributions to one another. If you only have one data set, it is probably better to just quote the summary statistics in tabular or numeric form, rather than making a box plot. On the other hand, when you have several distributions to look at box plots can help compare the structures underlying the different data sets.


# Relationships in Bivariate Data
Often, you'll have a dataset with two variables and you want to know if a relationship exists between them (and what kind it is). So let's begin by plotting the two variables against one another to see if a relationship exists.  

### Start by Smoothing Noisy Data
Before we can characterize a particular relationship, we ought to begin by asking a relationship exists in the first place by smoothing out the noisy data to look for an underlying pattern. There are two common smoothing techniques: **weighted splines** and **locally weighted linear regression (LOESS)**. They both work by constructing local approximations of the behavior and string them together to form a smooth curve.

- **Splines** are made from piecewise (cubic) functions strung together. Each piece should be sufficiently smooth locally, as well as satisfying a globally smooth optimization condition. In general however, splines are better for considering *overall* smoothness while LOESS is more favorable for considering local details.
- **LOESS** works by approximating the data locally through a linear or low-order polynomial function, while incorporating local weighting. LOESS is computationally expensive so splines may be favorable when only an approximation is needed.
  - the difference between LOESS and regular linear regression is the *weight factor*, which emphasizes points close to the location of interest.


### Scatter Plots



### Logarithmic Plots
Rather than graphing raw data, a popular method is to plot the logarithm of the data. This is most useful with data sets that span multiple orders of magnitude.

A main reason why logarithmic plots are valuable is because they help control large variations in data. Additionally, they turn multiplicative behaviors into additive ones through the fundamental behavior of logarithms.

Two types:
1. Single or Semi-Logarithmic Plots
- only one axis is scaled logarithmically (usually the y-axis)

2. Double or Log-Log Plots
- both axes are scaled logarithmically




# Time Series Data Analysis
Let's say you want to track the number of people who get sick over time.


# High Dimensionality/Multivariate Analysis
Many common methods of visualization become impractical after datasets exceed a 2-3 dimensions. Multidimensional visualization is an emerging topic - a great deal of ongoing work is attempting to improve existing methods.  

Things to keep in mind:
- Difficult (but important) to come up with an appropriate palette
    - Tip: use a very simple color palette (e.g. blue - white - red works well)
    - Tip: map low values to cool colors and high values to warm colors to make visualization intuitive

**Scatter Plot Matrices**: construct all possible 2D scatter plots and display them together in matrix format
- the scatter plot matrix is symmetric across the diagonal
- a convenient way to get a quick overview and find pairings that deserve a closer look
- unwieldly (hard to see anything) after about a half dozen variables
- half of the graphs produced are redundant, so you could replace them with something else (e.g. KDE plots, histograms, etc)

**Parallel Coordinate Plots**
- show more variables
- instead of putting coordinate plots perpendicular to one another, have them parallel
- downside is that they are not that intuitive to someone who has never seen one before. After it is explained to the reader, however, they are quite nice.
- main use of these is to find interesting clusters in high-dimensional data sets
- Many times, you'll want to normalize the ranges of the results so that they are all on the same scale (e.g. between 0 and 1 is often useful)
- the appearance of the plot is dependent on the order of the parallel axes. It's a good idea to use an interactive tool (like Plotly) or to manually reshuffle them to see if there is any significant impact.

## Trivariate Plot options
- Surface Plots (3D contour plots)
  - often visually impressive, not that useful practically (hard to read numbers off them)
- False Color Plots
- Contour Plots




**The Four Sampling Distributions**
- *The Gaussian Distribution* - describes the distribution of averages, requiring you to know the variance upfront. It's for the distribution of a sum of "independent, symmetric, random variables"
- *The chi-square Distribution* - describes the sum of squares of Gaussian variables. Is used to describe the distribution of variances. Requires us to know the number of degrees of freedom to evaluate it.
- *Student t distribution* -
- *Fisher's F Distribution* - use this if you want to compare two variances against each other (to see if they are the same)

With all four, you have measurements that are all independent and identically distributed

A **p-value** represents the strength of the evidence in a hypothesis test (and to help soften the hard division between significant and not). It describes the probability of getting a
-  "In other words, the P value is the probability of being wrong when asserting that a difference exists."
- smaller p-values are interpreted to mean higher significance. Meaning that the current (null) hypothesis may not explain the observation. In other words, the null hypothesis is rejected if the probability is below a small (arbitrary) value known as the level of significance (often 0.05 by convention).

### P-value alternatives
(1) **Confidence intervals**: when we want to express how sure we are that our observation (p-hat) is close to the true value of the parameter (p). So we seek an interval around p-hat such that in 95% of samples, the true mean p will lie inside the interval. Again, 95% is arbitrarily chosen, but this method may be better suited to describing the magnitude of an effect.
  - in contrast to hypothesis testing (which relates to a single conclusion of significance vs no significance), confidence intervals provide a range of plausible values for your population
(2) **likelihood relationship**:
(3) **Bayes factors**:



# Bayes
## Probability distributions
### Discrete
When the probability distribution function (Z) is discrete, then the distribution takes the form of P(Z = k), measuring the probability that Z takes on value k.
- Popular **probability mass functions** that consistently appear (e.g. Poisson)

### Continuous
When Z is continuous, use a **probability density function** (e.g. exponential density)

# Probability Mass Functions (PMF)
A **PMF** maps from each value to its probability.
- CON: as the number of values you have goes up, the probability of each value decreases. Thus, the effects of random noise grows stronger

# Cumulative distribution functions (CDFs)
- the *percentile* is the fraction of people who scored the same or lower than you.
- the *cdf* is a function that maps from a value to a percentile rank. This function is the fraction of that is less than or equal to x
  - PRO: especially good for comparing distributions

# Analytic distributions
### The exponential distribution
- occurs when we look at interarrival times (the time between events)

### the Gaussian (normal) distribution
- characterized by the mean and SD
