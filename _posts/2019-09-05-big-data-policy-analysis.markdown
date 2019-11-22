---
published: true

layout: post
title: "The Politicization of Big Data"
date: 2019-09-05
description: "How subjective preferences and subtle politics influences the success of a big data analysis project."
img: divide2.webp
fig-caption: Big data in policy analysis
tags: [big data problems, policy analysis, uncertainty, data analytics, decisionmaking]
categories: [Policy]
---
Innovative new tech opportunities such as machine learning, big data analysis, and cloud computing are already disrupting a wide variety of global issues. To be a part of the cool shift towards advanced computing though, you'll have to master a lot of old-school things like [classical statistics](/hypothesis-testing/) and [probability distributions](/probability-distributions/), which is why I've included several tutorials in this blog. But you'll find no examples of coin flips and dice-rolling here, because you can find that in plenty of other textbooks and websites. Instead, my focus is on the messy and uncertain situations that surround real-world policymakers. While the political decisionmakers who craft our environmental regulations, disaster budgets, and health insurance policies certainly rely on mathematical and statistical information, there is (hopefully) more to their decision making than measuring and coin-flipping.

* TOC
{:toc}


# How do policymakers use scientific evidence?
The process of policymaking is probably never linear, although you'll find a number of decision analysis texts that seem to portray it as if it were. More likely, policies are made through interactions between multiple stakeholders (or "actors") and over a series of compromises, tangents, and revisions. Also, many policy ideas "sit on a shelf" until the right window of opportunity presents itself - perhaps through a shift in public opinion or financial opportunity - that makes the idea suddenly become favorable. Any multi-actor problem is bound to grapple with diverging interests, culture differences, miscommunication and differing information sources. And of course, the jaded among us will hark of corruption, partisanship, and hidden agendas. However, this is the nature of the world we live in and which really big and important decisions are made.
<!-- To be useful, scientific analysis must be conducted in the world as it really is, not how we wish it was. -->

Those of us who are technically-inclined serve an important role in supporting those who are appointed to create large-scale policies. Whether you are:

* an engineer advising on the safety of a new infrastructure project;
* a data scientist making projections from census data;
* an epidemiologist giving input on how government money should be spent against a novel disease;
* an economists providing forecasts about a proposed tax incentive; or
* an IT expert weighing in on a program to combat a cybersecurity threat.

All of these technocrats play a role in the ability of policymakers to make evidence-informed decisions. However, it is misleading to think of the analyst's role merely as the "neutral advisor". Data is assumed to be objective because we have institutionalized its use, however, we must understand that no analysis is truly "objective" and all data collection and modelling captures just part of the story.

The standard scientific model assumes that if there is not a consensus about some fact, then more research should be done and then the truth will be revealed. However, applying this standard model to problems in the policy sphere - where all facts seem up for debate - means that conducting *more* research is unlikely to resolve the problem. This is a major frustration to scientists, who may implicitly assume the following linear trajectory exists:

<p style="text-align: center;">"more science"  &rarr; "less uncertainty"  &rarr; "correct course of action"  &rarr; "political action"</p>

Therefore, to the scientifically-inclined, the only excuse for a lack of policy action can be if there is uncertainty around what the best course of action is. However, the politically-minded are well aware that supposing there is only *one* way to define the "best" option is far removed from reality.

<br>
![science-policy interface](../assets/img/climate-change-science-v-politics-cartoon.jpg){:.post-img-smaller}

## Data, data everywhere
We live in an age of data. "Datafication" refers to the increasing number of activities conducted in a semi-digital environment, where sensors, devices, and apps collect information about our activities. With these seemingly endless data streams being collected, the choice surrounding *which* data sets to use in *what way* are increasingly contested.

The problem with having endless data is that there is now *more* and *different* datasets one can use to (partially) answer the same question. Even when a data analysis question appears straightforward, a closer look at the implicit assumptions associated with it can reveal hidden complexities. Scientific questions that seem simple enough to quantify at face value become "politicized" based on the techniques or datasets used to calculate them. For instance:
* How much have global surface temperatures risen in recent years? <br> (*[Taking Politics Out of Climate Change](https://www.pbs.org/wgbh/nova/article/depoliticizing-climate-change/)*)
* What is the current unemployment rate? <br>
(*[The Politics Surrounding Jobless Data](https://amstat.tandfonline.com/doi/full/10.1080/2330443X.2016.1241061)*)
* How old is the human race? <br>
(*[Kitzmiller v. Dover Area School District](https://berkleycenter.georgetown.edu/cases/kitzmiller-v-dover-area-school-district)*)

These questions seem to lie squarely in the domain of scientific study, yet because of their political or social ramifications they become highly contested. Each side argues that their opponent is using a flawed techniques, definitions, or datasets in order to generate favorable results. In such highly-charged environments, big data analysts must be careful and transparent in their modeling choices and assumptions.



## What do we mean by "Big Data"?
The term "Big Data" is relatively new but increasingly becoming an everyday term. It encompasses the idea that many of today's datasets do not fit comfortably on a single disk, let alone on main memory. A common definition of Big Data is based on multiple "V's" that each denote a characteristic of big data: **variety**, **velocity** and **volume**.

However, the multiple V definition presents an operational problem because there isn't a meaningful threshold for any of these characteristics (i.e. what is a "big" volume?). Instead, it may be more useful to think of **Big Data Analysis** as the:
> Combination of multiple, large datasets from various sources (unstructured and structured, internal and external) and the application of advanced analytic techniques to gain new insights beyond the applications that the data were originally collected for.

<!-- Large datasets can be extremely useful to inform and guide strategy development. Yet, policymaking occurred long before the advent of big data. So how have decisions been guided historically? Perhaps with less evidence behind them than we would like there to be. There is a growing body of research to support the idea that policy decisions are often not based on evidence, but instead made by "gut feeling" or by following precedent. -->

Big data can be tremendously useful for solving policy problems. A major problem, however, occurs when users are unaware of the assumptions behind their data. Quantifiable information is often assumed to be objective, however, we must understand that no analysis is truly "objective" and all data collection and modelling captures just part of the picture. For instance, failing to fully understand the context of information can lead to big data discrimination, where models are trained on historical data which codifies patterns of discrimination.

# The role of big data analysts in policymaking
In the world of big data, it is easier to criticize data, bring up alternative data, and argue system boundaries. Therefore, in order to provide policy support in this increasingly complex and data-driven world, data analysts are recommended to keep in mind the following:

- Evolve from being a solely "objective/scientific" external expert toward a policy facilitator role. Try to construct the facts *along with* the stakeholders in order to make it more likely that consensus surrounding the results will be attained.
- Be sensitive to concerns about open data privacy and management.
- Rather than prescribing a single or narrowly defined strategy, present a variety of potentially strong options or solutions that have wiggle room. Make work more attractive to policymakers by showing strategies that can help solve stalemates. By redefining and broadening the problem, you may create new options for decision makers.
- Big data is potentially powerful but not necessarily better than a smaller, well-chosen sample set. Don't forget the basics!


## The Politicization of Big Data - Closing Remarks
<!-- Convincing policymakers of big data evidence -->
Analysts provide computational skills that can support politicians in gaining insight from big data. However, big data analysis frequently involves more "political" decisions to be made during the analysis compared to "normal" data. The way that assumptions are quantified and relationships are structured may already inject political subjectivity into the analysis.

As an analyst working on policy-relevant concerns, it is important to consider the shortcomings behind big data. Analysts must take care not to take data only at their face value, but to interrogate the assumptions and methods used to create them. This is especially the case for contentious political issues. If you (as the analyst) do not question the characteristics behind your assumptions, then your policy opponent is sure to!

<br>

## References
Hoppe, Robert. (1999). Policy analysis, science and politics: From 'speaking truth to power' to 'making sense together'. Science & Public Policy - SCI PUBLIC POLICY. 26. 201-210. 10.3152/147154399781782482.

<!-- <br>
![problems with big data](../assets/img/its_not_you.jpg){:.post-img-smaller}
<div class ="post-img-caption">
https://timoelliott.com/blog/cartoons/analytics-cartoons
</div> -->

<!-- <br>
![using big data](../assets/img/cartoon-using-big-data.jpg){:.post-img-smallest}
<div class ="post-img-caption">
https://timoelliott.com/blog/cartoons/analytics-cartoons
</div>
<br> -->
