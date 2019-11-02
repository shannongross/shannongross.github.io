---
published: false

layout: post
title: "Learning data science for policy analysis"
date: 2019-09-05
description: Tips and tricks about learning data science for policy analysis problems.
img: numbers.jpg
fig-caption: Data and Policy
tags: [policy analysis, data science, statistics, python, visualizations]
---
# Outline
- TOC
{:toc}

# A. How can data science help with policy analysis?
Policy analysis is an endeavor to understand the process through which governments develop different policies, and what impact those policy choices ultimately have. With ever-increasing data availability, data science provides a powerful aid to supporting the aims of policy analysis.

It's common knowledge that there's more data collected today than any other time in history. Policymakers would like to use available datasets (e.g. electricity use trends, patterns in police arrests, text on social media, weather sensors, and so forth) about their communities and constituents to gain some sort of insight. Sometimes, what insight they are looking for is more of a vague feeling than a clear set of instructions, which can present challenges for the data scientist charged with generating those insights.

In order to be sure that data are used appropriately to support policy analysis, a strong background in mathematics and statistics is necessary. Even where a data scientist is capable of

What are some basic statistical and programming foundations that a data scientist should have in order to properly support policy concerns?

# B. Basic Statistics for Data Science
## Summary Statistics
The experienced analyst should have enough familiarity with statistical concepts such as mean, standard deviation, and percentiles to be wary of relying on them. These summary statistics are popular and easy to calculate, however they are based on assumptions that must be clearly understood and articulated if they are to be applied appropriately.

**Important Assumptions**
- Summary statistics work well when the data is symmetric, with a central peak, and without any crazy outliers. In reality, most real world data sets violate one of these assumptions.
- Summary statics are only relevant to **unimodal distributions**. When the data contains more than a single peak, concepts like mean and mode will give you results will *seem reasonable* but are actually misleading.




- *variation* describes the behavior within a variable
  - its usually a bit harder to interpret than standard deviation, because the result of variance is in units squared (e.g. weeks^2, mph^2), which doesn't make a lot of sense. Thus it's not a great summary statistic.
- *covariation* describes the behavior between variables
- *central tendency* when values tend to cluster around a point (use *modes* if there is more than one cluster)
- *spread* how much variability exists
- *tails* do the probabilities drop off
- *outliers* extreme values far away from the mean
- *mean* be careful - this value is misleading when there is no "typical" instance (i.e. a lot of variance or spread)

### Start by Smoothing Noisy Data
Before we can characterize a particular relationship, we ought to begin by asking a relationship exists in the first place by smoothing out the noisy data to look for an underlying pattern. There are two common smoothing techniques: **weighted splines** and **locally weighted linear regression (LOESS)**. They both work by constructing local approximations of the behavior and string them together to form a smooth curve.

- **Splines** are made from piecewise (cubic) functions strung together. Each piece should be sufficiently smooth locally, as well as satisfying a globally smooth optimization condition. In general however, splines are better for considering *overall* smoothness while LOESS is more favorable for considering local details.
- **LOESS** works by approximating the data locally through a linear or low-order polynomial function, while incorporating local weighting. LOESS is computationally expensive so splines may be favorable when only an approximation is needed.
  - the difference between LOESS and regular linear regression is the *weight factor*, which emphasizes points close to the location of interest.

Relationships in Bivariate Data:
Often, you'll have a dataset with two variables and you want to know if a relationship exists between them (and what kind it is). So let's begin by plotting the two variables against one another to see if a relationship exists.  

# C. Fundamental Visualizations for Data Analysis
## 1. Histograms
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

## 2. Kernel Density Estimates (KDEs)
As opposed to classical histograms, you can't easily generate a KDE with a pen and paper - their popularity has risen with the increased availability of computational power.

**Kernel**: a smooth, strongly peaked curve that covers each data point. The most common function used to generate the KDE curve is Gaussian, but valuable alternatives such as Box and Epanechnikov kernels exist.

The most important parameter of a KDE curve is the *bandwidth*, which results in a tradeoff between height and width of the curves. Setting this parameter involves some trial and error - you want the curve to be detailed enough to not hide important information and yet enough smoothness to ensure the curve is not overfitted.

The main reason both histograms and KDEs are so popular is because they are easily interpreted - they give us an intuitive explanation for how likely we are to find a data point of a certain value.

## 3. Cumulative Distribution Functions (CDF)
A **CDF** tells us what fraction of points occur below the value *x*. An advantage of using a CDF instead of (or alongside of) a KDE is that KDEs can be misleading - the human eye automatically senses the largest peak and assumes that "most" points gravitate around this value. CDFs can make it clear when this is not the case - spreading out the total area under the curve in a different way than the KDE (i.e. without binning).

Why use a CDF? They are useful for questions like: *what fraction of points fall between x1 and x2?* because you can simply read the answer off the x-axis. Additionally, CDFs can help you consider the way a distribution is balanced with respect to its tails.

While CDFs are generally less intuitive than the KDE - creating them can be an advantageous supplement to your data analysis process. For instance, CDFs may provide visual information that is less noisy and often more faithfully represented.

## 4. Scatter Plots

### Jitter Plots
When your data is coarse-grained or integer-valued, many of the data points may lie on top of one another on a plot. **Jittering** is a technique where you shift every value by a small random value in order to better visually identify interesting clusters.

## 5. Box and Whisker Plots
The popularity of box and whisker plots lies in its ability to convey a lot of statistical information in one compact visualization.

When should you use a box and whisker plot? It's best when you are comparing multiple distributions to one another. If you only have one data set, it is probably better to just quote the summary statistics in tabular or numeric form, rather than making a box plot. On the other hand, when you have several distributions to look at box plots can help compare the structures underlying the different data sets.


## 6. Logarithmic Plots
Rather than graphing raw data, a popular method is to plot the logarithm of the data. This is most useful with data sets that span multiple orders of magnitude.

A main reason why logarithmic plots are valuable is because they help control large variations in data. Additionally, they turn multiplicative behaviors into additive ones through the fundamental behavior of logarithms.

Two types:
1. Single or Semi-Logarithmic Plots
- only one axis is scaled logarithmically (usually the y-axis)

2. Double or Log-Log Plots
- both axes are scaled logarithmically

## 7. Time Series Data Analysis
Let's say you want to track the number of people who get sick over time.



## 8. High Dimensionality/Multivariate Analysis
When you have 3 variables (Trivariate Plot options)
- Surface Plots (3D contour plots)
  - often visually impressive, not that useful practically (hard to read numbers off them)
- False Color Plots
- Contour Plots

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







# Tools for Data Science in Policy Analysis
## Why Python?
Python is a free and powerful scripting language that will be your bread & butter as a data scientist. It's short and intuitive commands make reading the code simple, while its open-source nature means that powerful modules built by others are at your disposal. Because it is popular and widely used, there are many help guides and stack overflow answers to support your questions. Python's capability for policy analysis problems rests largely with its ability to handle huge amounts of data. Policymakers may have large-scale questions about future trends among their constituents and key issues, and python makes it easy to perform powerful tasks to answer their questions. Because python connects well with geospatial tools, database systems, and other applications, it is powerful and easily extendable.

## Why R?

## WHy SQL?
