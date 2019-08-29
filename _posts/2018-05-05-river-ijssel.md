---
layout: post
title: "Exploratory Policy Modeling for Flood Management"
date: 2018-05-05
description: This project uses advanced exploratory modeling techniques to provide policy support on a water management case study.
img:  ijssel.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [water management, python, policy analysis, decision support]
---

To supplement the limitations of human cognition in non-linear and uncertain situations, quantitative modelling can be a useful aid (J. Kwakkel & Haasnoot, 2018). Models may help policymakers to compare, contrast, and visualize the potential policy performance of different options. Such computational testing not only helps to understand the behavior of the system, but also to make likely tradeoffs between different objectives clear to the decision maker. However, recent studies suggest that the *success of models to influence policy debates has been rather limited* (Saltelli & Giampietro, 2015). Critics have argued that models often exclude, ignore, or simplify precisely those aspects that make public policy problems so formidable. Furthermore, models often fail to answer many of the key questions asked by policymakers (Victora, Habicht, & Bryce, 2004).

## Applying exploratory modeling to deeply uncertain policy problems
It is unavoidable that any model will contain assumptions that simplify reality, but while the assumptions chosen may be obvious and rational to the modeler, to the policymaker the simplifications may appear to be biased and misguided. In some cases, the uncertainty can be reduced through further laboratory experimentation or data collection. In other cases, the uncertain parameter is so unknown that it is irreducible even if additional data is collected – greatly increasing the difficulty for modelers and decision makers alike. In multi-actor situations, policymakers may disagree about what values or structures best represent these parameters, leading to a situation of “deep uncertainty.”

**Deep uncertainty** refers to a situation where the various parties to a decision do not know or cannot agree on how the system works; how likely various possible future states of the world are; and how important the various outcomes of interest are (Lempert et al., 2003). Accordingly, deep uncertainty problems are often contentious. From a  modeler’s perspective, this means that there are many plausible model structures that could be used; a variety of perspectives on how to formulate the main objectives; and different ideas about what the optimal solution sets are (J. H. Kwakkel, Walker, & Haasnoot, 2016). In situations of deep uncertainty, **traditional decision analysis methods may be insufficient** to assist decision makers in coming up with strategies to achieve their objectives. Thus, rather than falsely trying to reduce an irreducible uncertainty – or avoiding creating a model about the topic at all – modelling techniques that are able to systematically explore deep uncertainty values are needed.

## Decision Support on River IJssel Flood Management
The River IJssel Flood Management case is an example study of the conflicts that frequently arise between scientists and policymakers, especially for deeply uncertain problems. The following features are notable:
* There are a variety of plausible models of the flood system
* There is no single "correct" way to frame the problem. A combination of perspectives and scenarios is needed.
* Exploratory modeling approaches can help decisionmakers to explore and adapt. The goal is to *identify differences that make a difference*. Then, help policymakers to design plans that are relatively insensitive to these differences (i.e. exogenous uncertainties).

## Example exploratory model for the River IJssel case study
View the full code here: [Decision Support on River IJssel Flood Management](https://github.com/shannongross/Model-Based-Decision-Making)
