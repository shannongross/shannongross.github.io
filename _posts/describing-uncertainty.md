---
published: false

layout: post
title:
date:
description:
img:  
fig-caption:
tags: []
categories: [Tutorial]
---



1. TOC
{:toc}
{:.toc-styling}

# Reporting uncertainty
The average time a woman in some African country spends walking to collect water from a well is estimated to be 30 minutes/day. How reliable is this statement?
The concentration of Arsenic in a tubewater well is measured to be 50.5mg/L, which is above the "safe" level declared by the Government of Bangladesh.

- a preferable alternative to giving a single estimate is to provide a range/interval

- for small samples where the data is not distributed normally, the mean will not be a good approx.
- But as you increase the number of data points, the mean can effectively be approximated using a normal distribution. This is  the Central Limit Theorem, which states that for data that have finite variance (lots of environmental problems!) the sample mean will approach the normal distribution with large same sizes. If the data is really skewed to one side or has extreme outliers, it may take a lot more data points until you see the distribution become symmetric.
- When you only have a small number of data points (which is common!) the means may not follow the pattern of normality, esp if the data are skewed
- another option for finding means and confidence intervals is *log transformation*. By taking the natural logarithm of each data point and assuming the data are relatively symmetric, you may achieve an estimate of the mean with less variance.

- "Data must be assumed nonnormal unless shown otherwise. It is difficult to disprove normality using hypothesis tests (Chapter 4) due to the small sample sizes common to environmental data sets. It is also difficult to see non-normality with graphs unless the departures are strong (Chapter 10). It is unfortunate that though most water resources data sets are asymmetric and small, symmetric intervals are commonly used."
- "An outlier is an observation which appears to differ in its characteristics from the bulk of the data set to which it is assigned. It is a subjective concept -- different people may define specific points as either outliers, or not. Outliers are sometimes deleted from a data set in order to use procedures based on the normal distribution. One of the central themes of this book is that this is a dangerous and unwarranted practice. It is dangerous because these data may well be totally valid. There is no law stating that observed data must follow some specific distribution, such as the normal. Outlying observations are often the most important data collected, providing insight into extreme conditions or important causative relationships. Deleting outliers is unwarranted because procedures not requiring an assumption of normality are both available and powerful."


- if you perform tests on your data while assuming it has some particular distribution (e.g. normal), you are performing **parametric testing**. If your data really does follow this particular distribution, then you have many shortcuts available to you that make your life a lot easier.
- Alternatively, there is **nonparametric testing**, which does not assume any distribution. You gain information from the data by comparing each data point with every other data point. This process is good at getting information about the relative magnitudes of the values without boiling it down to just a couple stats.
- Historically, statistics applications have predominately used parametric methods because they are much more "elegant".

### Hypothesis Tests
- When we collect data, we generally have with some notion of how that data might behave (called a hypothesis!). A reason for gathering data, therefore, is to test the validity of our hypothesis by supporting it with this evidence.
- hypotheses are often used to compare and contrast two datasets. For instance, if you go to a city in Bangladesh and measure the arsenic concentration in different wells over time, you might make a statement like "our remediation efforts have decreased arsenic concentration in these wells". But in order to support his statement with evidence, you may want to back it up with statistics provided by hypothesis tests. This makes sure you conclusions are reproducible/clear to other experts. They also measure how *strong* your conclusion is

- "The primary reason to test whether data follow a normal distribution is to determine if parametric test procedures may be employed. "


#Correlation
- "The primary reason to test whether data follow a normal distribution is to determine if parametric test procedures may be employed."
- "The above situations require a measure of the strength of association between two continuous variables, such as between two chemical concentrations, or between amount of precipitation and time. How do they co-vary? One class of measures are called correlation coefficients, three of which are discussed in this chapter. Also discussed is how the significance of that association can be tested for, to determine whether the observed pattern differs from what is expected due entirely to chance. "
- "Whenever a correlation coefficient is calculated, the data should be plotted on a scatterplot. No single numerical measure can substitute for the visual insight gained from a plot. Many different patterns can produce the same correlation coefficient, and similar strengths of relationships can produce differing coefficients"
- "Correlation coefficients measure of the strength of association between two continuous variables. Of interest is whether one variable generally increases as the second increases, whether it decreases as the second increases, or whether their patterns of variation are totally unrelated. Correlation measures observed co-variation. It does not provide evidence for causal relationship between the two variables. One may cause the other, as precipitation causes runoff. They may also be correlated because both share the same cause, such as two solutes measured at a variety of times or a variety of locations. (Both are caused by variations in the source of the water). Evidence for causation must come from outside the statistical analysis -- from the knowledge of the processes involved. "
