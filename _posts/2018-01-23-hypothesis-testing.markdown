---
published: true

layout: post
title: "Hypothesis Testing in Policy Analysis"
date: 2018-01-23
description: "A discussion of the appropriateness of classical statistics including hypothesis testing in complex policy analysis problems."
img: hypoth_testing_cover.webp
fig-caption: Classic uses of hypothesis testing
tags: [frequentist statistics, hypothesis testing in policymaking, data analytics, decisionmaking, tutorials]
categories: [Tutorial]
---

- TOC
{:toc}


## Using Classical Statistics
In statistics, we have the following:
- A **population**, or the set of all possible outcomes.
- A **sample** of the entire population, because it is easier to work with a subset than the whole (very large) set.

Whenever we are performing hypothesis testing, we are concerned with the question: *is the effect we observe in the sample likely to occur in the population?*  In other words, we use hypothesis testing to help reach a conclusion about the universe by testing a sample of that universe. Doing this is known as **statistical inference**, where we infer characteristics of the entire population based on results from the sample set.

Hypothesis testing is a central technique of classical statistics. Most often it is used to decide if a relationship is statistically significant. Importantly however, it does not try to measure the size of an effect, it merely tries to determine whether an effect *exists*.


## Why Use Hypothesis Testing in the Real World?
Suppose that the mayor of a small community has come up with a new policy for policing crime in his district. After putting the policing policy into effect for awhile, the mayor feels like the new method has worked pretty well to reduce crime in the area. But is the reduction in crime statistically significant, or just the result of random noise? To test this, the mayor differentiates between:

1. The **null hypothesis** - that there is no difference between the new policy and the old one (i.e. the null hypothesis is the boring finding). If the new policy makes no different, then we "fail to reject the null hypothesis". This double negative statement is important because we can never truly *prove* that the new policy was the reason crime went down, only to show that *it is not true that a relationship does not exist*.

2. On the other hand, there is the **alternate hypothesis** (or as I like to think of it- the interesting finding). If the alternate hypothesis is true, it means that there is a difference between the new policy and the new policy that is statistically significant. When this happens, we say that we have enough information to "reject the null hypothesis".

If you're scratching your head about the weird logic we use when describing the results of these hypotheses, you're not alone! One of the biggest drawbacks of hypothesis testing is that interpreting the results requires some seriously non-intuitive line of reasoning.

A second shortcoming is that the resulting statement has almost no *practical* meaning. In the real world, the effects of a new policing policy cannot easily be divided strictly into either "significant" or "not significant". Instead, the effects of the policy probably lie somewhere along a continuum instead of completely in one bucket or the other. This opens up the discussion to some of the classical traps of hypothesis testing.

<br>
![hypothesis testing pitfalls](../assets/img/hypoth_testing_cartoon.png){:.post-img-smallest}

<div class ="post-img-caption">
https://xkcd.com/archive/
</div>
<br>


# Flaws and Classical Traps of Hypothesis Testing
Let's say that to make things simple, the mayor wants to be able to use classical statistics to distinguish between a "significant" or a "not significant" policy. This will make things a lot easier for him when we has to defend his new policy to the community or against his political opponent. As is often done in statistics, he creates the division between "significant" and "not" by setting the **statistical significance level** at 5 percent. The level 0.05 is commonly chosen out of convention, tradition, or laziness - however you want to look at it - but take a moment to think of how arbitrary that barrier really is (i.e. why not 3 percent or 4.999 percent?). In fact, our mayor is dismayed to find that when the numbers are crunched the result lies just *barely* outside the level of statistical significance. If the police had just caught one or two more bad guys, it would have been enough for him to confidently declare that the results of his new crime policy made the streets **significantly** safer. Instead, his own experimental design - which centers around an arbitrarily chosen threshold and a strict, dichotomous classification system - forces him to say that the new crime policy did not have a "significant" effect (even if many more criminals were caught then before).

Perhaps the mayor notices this and decides to hold off on publishing the results. Instead, they will collect data for a few more months and then crunch the numbers again. This time, after many more samples are collected, the major finds that the results are in his favor - the results meet the level of statistical significance! We can reject the null hypothesis at last. However, this behavior is known as **data dredging** and is widely discouraged in the statistics community. It refers to the practice where you run enough tests to draw whatever conclusion you want to.

However, let's assume that the mayor used a well-designed experimental setup and his staff of experienced statisticians agree that a statistically significant relationship does exist. The major gets behind his podium and jubilantly tells the citizens that the policy has had an effect. But one citizen - who has always been skeptical of our mayor - is not convinced. He complains to the mayor that the new policy was very expensive - taxes had to be raised enormously on all of the citizens to fund it. Just because the major used a hypothesis test to show that the policy had a significant effect does not tell them *how significant* the new policy is. Our concerned citizens wants to know if it was worth it.

This concern gets to the heart of the practical limitation of hypothesis tests. In real applications, the *size* of a statistical significance relationship may often be so much more valuable than a description of whether it *exists* or not. Increasingly, more and more statisticians are becoming uneasy with the routine use of such statistical tests, especially in [medicine](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3016704/) and in [science](https://www.npr.org/sections/health-shots/2019/03/20/705191851/statisticians-call-to-arms-reject-significance-and-embrace-uncertainty). Because of these flaws, hypothesis testing may often be better suited to theoretical and academic studies, for instance when trying to highlight the existence of some phenomenon. In many real world applications, focusing on graphical analyses or confidence intervals may potentially be more insightful than relying on hypothesis tests alone.
