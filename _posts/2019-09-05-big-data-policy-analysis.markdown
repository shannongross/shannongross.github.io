---
published: true

layout: post
title: "The Politicization of Big Data"
date: 2019-09-05
description: "How subjective preferences and subtle politics influences the success of a big data analysis project."
img: divide2.webp
fig-caption: Big data in policy analysis
tags: [big data problems, policy analysis, uncertainty, data analytics]
categories: [Policy]
---
- TOC
{:toc}

## Data, data everywhere
We live in an age of data. **Datafication** refers to the increasing number of activities conducted in a semi-digital environment, where sensors, devices, and apps collect information about our activities.

With these seemingly endless data streams being collected, the choice surrounding *which* data sets to use in *what way* are increasingly contested. Even when a data analysis question appears straightforward, a closer look at the implicit assumptions associated with it can reveal hidden complexities.

Today, there are more and different datasets one can use to (partially) answer the same question. Scientific questions that seem simple enough to quantify at face value become "politicized" based on the techniques or datasets used to calculate them. For instance:
* How much have global surface temperatures risen in recent years? <br> (*[Taking Politics Out of Climate Change](https://www.pbs.org/wgbh/nova/article/depoliticizing-climate-change/)*)
* What is the current unemployment rate? <br>
(*[The Politics Surrounding Jobless Data](https://amstat.tandfonline.com/doi/full/10.1080/2330443X.2016.1241061)*)
* How old is the human race? <br>
(*[Kitzmiller v. Dover Area School District](https://berkleycenter.georgetown.edu/cases/kitzmiller-v-dover-area-school-district)*)

These questions seem to lie squarely in the domain of scientific study, yet because of their political or social ramifications they become highly contested. Each side argues that their opponent is using a flawed techniques, definitions, or datasets in order to generate favorable results. In such highly-charged environments, big data analysts must be careful and transparent in their modeling choices and assumptions.

<br>
![using big data](../assets/img/cartoon-using-big-data.jpg){:.post-img-smallest}
<div class ="post-img-caption">
https://timoelliott.com/blog/cartoons/analytics-cartoons
</div>
<br>

## What do we mean by "Big Data"?
The term "Big Data" is relatively new but increasingly becoming an everyday term. It encompasses the idea that many of today's datasets do not fit comfortably on a single disk, let alone on main memory. A common definition of Big Data is based on multiple "V's" that each denote a characteristic of big data: **variety**, **velocity** and **volume**.

However, the multiple V definition presents an operational problem because there isn't a meaningful threshold for any of these characteristics (i.e. what is a "big" volume?). Instead, it may be more useful to think of **Big Data Analysis** as the:
> Combination of multiple, large datasets from various sources (unstructured and structured, internal and external) and the application of advanced analytic techniques to gain new insights beyond the applications that the data were originally collected for.

<!-- Large datasets can be extremely useful to inform and guide strategy development. Yet, policymaking occurred long before the advent of big data. So how have decisions been guided historically? Perhaps with less evidence behind them than we would like there to be. There is a growing body of research to support the idea that policy decisions are often not based on evidence, but instead made by "gut feeling" or by following precedent. -->

Big data can be tremendously useful for solving policy problems. A major problem, however, occurs when users are unaware of the **assumptions** behind their data. Quantifiable information is often assumed to be objective, however, we must understand that no analysis is truly "objective" and all data collection and modelling captures just part of the picture. For instance, failing to fully understand the context of information can lead to **big data discrimination**, where models are trained on historical data which codifies patterns of discrimination.

# The role of big data analysts in policymaking
Analysts provide computational skills that can support politicians in gaining insight from big data. However, big data analysis frequently involves more "political" decisions to be made during the analysis compared to "normal" data. The way that assumptions are quantified and relationships are structured may already inject political subjectivity into the analysis.

As an analyst working on policy-relevant concerns, it is important to consider the shortcomings behind big data. Analysts must take care not to take data only at their face value, but to interrogate the assumptions and methods used to create them. This is especially the case for contentious political issues. If you (as the analyst) do not question the characteristics behind your assumptions, then your policy opponent is sure to!

## Convincing policymakers of big data evidence
In the world of big data, it is easier to criticize data, bring up alternative data, and argue system boundaries. Therefore, in order to provide policy support in this increasingly complex and data-driven world, data analysts are recommended to keep in mind the following:

- Evolve from being a solely "objective/scientific" external expert toward a policy facilitator role. Try to construct the facts *along with* the stakeholders in order to make it more likely that consensus surrounding the results will be attained.
- Be sensitive to concerns about open data privacy and management.
- Rather than prescribing a single or narrowly defined strategy, present a variety of potentially strong options or solutions that have wiggle room. Make work more attractive to policymakers by showing strategies that can help solve stalemates. By redefining and broadening the problem, you may create new options for decision makers.
- Big data is potentially powerful but not necessarily better than a smaller, well-chosen sample set. Don't forget the basics!

<br>
![problems with big data](../assets/img/its_not_you.jpg){:.post-img-smaller}
<div class ="post-img-caption">
https://timoelliott.com/blog/cartoons/analytics-cartoons
</div>
