---
published: false

layout: post
title: "Learning data science for policy analysis"
date: 2019-09-05
description: Learning data science for policy analysis
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
- *covariation* describes the behavior between variables

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

# Linear Regression
Use this when you have a set of input values and want to measure the output (response) value. You are trying to determine a linear function that describes the control variable with the least amount of error. The purpose of this is to try and predict the value of the response variable, given some input.

In order to minimize the overall error of a linear regression function, you try to minimize the error of each of the individual points (since the overall error is the aggregate of these).

As with all summary statistics, it is important to properly understand and apply the assumptions behind linear regression. See [Anscombe's quartet](https://medium.com/datadriveninvestor/anscombes-quartet-12649db7eac0) for a particularly infamous example of the improper application of Linear Regression.

No matter the chosen method for data analysis, plotting the data you are trying to analyze is a critical part of the process. Scripting languages such as Python and especially R are useful for generating statistical plots.

See: [Intro to R](/intro-to-R/)



# Time Series Data Analysis
Let's say you want to track the number of people who get sick over time.


# High Dimensionality/Multivariate Analysis
Many common methods of visualization become impractical after datasets exceed a 2-3 dimensions. Multidimensional visualization is an emerging topic - a great deal of ongoing work is attempting to improve existing methods.  

Things to keep in mind:
- Difficult (but important) to come up with an appropriate palette
    - Tip: use a very simple color palette (e.g. blue - white - red works well)
    - Tip: map low values to cool colors and high values to warm colors to make visualization intuitive

## Trivariate Plot options
- Surface Plots (3D contour plots)
  - often visually impressive, not that useful practically (hard to read numbers off them)
- False Color Plots
- Contour Plots




# Hypothesis Testing
Whenever we are doing statistics, we have the following:
- a **population**, or the set of all possible outcomes
- a **sample** of the entire population, because it is easier to work with a subset than the entire (very large) full set.
- **statistical inference** inferring characteristics of the entire population based on results from the sample set

Classical statistics is primarily interested in the following two procedures:
1. Estimation
 - assume that the population is described by some distribution (e.g. Gaussian) and try to estimate parameters (e.g. mean, standard deviation) based on the sample set
  - *point estimation* yields a specific value for a single parameter
  - *interval estimation* yields a range of values that the parameter is supposed to lie within
2. Hypothesis testing
- the purpose of hypothesis testing is to help us reach a conclusion about the universe by testing a sample of that universe.
- does not try to measure the size of an effect, it *merely tries to determine whether an effect exists*
- helps us decide if a relationship is **statistically significant**
- suppose we have a new drug to treat a particular illness and we want to know if it is effective. We divide the population in two and give the treatment to one half of the population. Is the application of the new drug statistically significant or just the result of random noise?
- the **null hypothesis** (Boring finding) in this case would be that the drug has no effect - there is no difference between the two populations. If the drug has no effect, then we "fail to reject the null hypothesis". This double negative statement is important because we can never truly *prove* that the treatment worked, only to show that *it is not true that a relationship does not exist*.
- the **alternate hypothesis** (interesting finding) is that there is a difference between the two populations that is statistically significant. In this scenario, we have enough information to "reject the null hypothesis".
  - one of the shortcomings of hypothesis testing is that interpreting the results requires this non-intuitive line of reasoning.
  - a second drawback is that that *the resulting statement has almost no practical meaning!*  Dividing the choice into either "significant" or "not significant" is not true to reality, where results do not usually fall into a dichotomy but lie along a continuum.

### Flaws and Classical Traps of Hypothesis Testing
(1) A result lies *just* outside the level of statistical significance. Thus, the outcome is categorized in a misleading manner. This problem is enhanced by the **arbitrariness of the statistical significance level**, which is commonly set at 5 percent (but why not 3 percent or 4.999 percent?). Thus, the process is fundamentally troubling - on the one hand we introduce a strict cutoff to divide between significant or not, and yet that very cutoff is arbitrarily chosen.
(2) **Data dredging** refers to the case where you run enough tests to draw whatever conclusion you want to.
(3) In real applications, the size of a statistical significance relationship is so much more valuable than a description of whether it exists or not.

Because of these flaws, hypothesis testing may often be better suited to theoretical and academic studies, for instance when trying to highlight the existence of some phenomenon. In many real world applications, seeking out the confidence interval to determine the size of some statistical relationship may be more insightful than hypothesis testing.

### P-Value Controversy
Increasingly, more and more statisticians are becoming uneasy with the routine use of such statistical tests, especially in [medicine](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3016704/).

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
