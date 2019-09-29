---
layout: post
title: "Exploratory Policy Modeling for Flood Management"
date: 2019-01-15 #2018-05-05
description: This project uses advanced exploratory modeling techniques to provide policy support on a water management case study.
img:  ijssel.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [water management, python, policy analysis, decision support]
---

To supplement the limitations of human cognition in non-linear and uncertain situations, quantitative modelling can be a useful aid. Models may help policymakers to compare, contrast, and visualize the potential policy performance of different options. Such computational testing not only helps to understand the behavior of the system, but also to make likely tradeoffs between different objectives clear to the decision maker.

<!-- However, recent studies suggest that the **success of models to influence policy debates has been rather limited** (Saltelli & Giampietro, 2015). Critics have argued that models often exclude, ignore, or simplify precisely those aspects that make public policy problems so formidable. Furthermore, models often fail to answer many of the key questions asked by policymakers (Victora, Habicht, & Bryce, 2004). Therefore, why do we continue to use models for supporting policy decisions? -->

<br>

# Decision Support on River IJssel Flood Management
The [River IJssel Flood Management case](https://www.mdpi.com/2076-3263/8/6/224/htm) is an example study of the conflicts that frequently arise between scientists and policymakers, especially for deeply uncertain problems. The following features are notable:
* There are a variety of plausible models of the flood system
* There is no single "correct" way to frame the problem. A combination of perspectives and scenarios is needed.
* Exploratory modeling approaches can help decisionmakers to explore and adapt. The goal is to **identify differences that make a difference**. Then, help policymakers to design plans that are relatively insensitive to these differences (i.e. exogenous uncertainties).

## Applying exploratory modeling to deeply uncertain policy problems
No model can completely replicate the real world. It is unavoidable that any model will contain assumptions that simplify reality, especially in situations where the system contains many unknowns. In some cases, this uncertainty can be reduced through further laboratory experimentation or data collection. In other cases, the uncertain parameter is so unknown that it is irreducible *even if additional data is collected*. When gathering more data fails to reduce uncertainty, the choice of how to model a parameter becomes a subjective one. In multi-actor situations, policymakers may disagree about what values or structures best represent unknown parameters, leading to a situation of “deep uncertainty.”

[Deep uncertainty](https://www.sciencedirect.com/science/article/pii/S1364815212003131) refers to a situation where the various parties to a decision do not know or cannot agree on how the system works; how likely various possible future states of the world are; and how important the various outcomes of interest are. Accordingly, deep uncertainty problems are often contentious. From a [modeler’s perspective](https://ascelibrary.org/doi/full/10.1061/%28ASCE%29WR.1943-5452.0000626), this means that there are many plausible model structures that could be used; a variety of perspectives on how to formulate the main objectives; and different ideas about what the optimal solution sets are.

In situations of deep uncertainty, **traditional decision analysis methods may be insufficient** to assist decision makers in coming up with strategies to achieve their objectives. Thus, rather than falsely trying to reduce an irreducible uncertainty – or avoiding creating a model about the topic at all – modelling techniques that are able to systematically *explore*  deep uncertainty values are needed.

## Example exploratory model for the River IJssel case study
View the full code here: [Decision Support on River IJssel Flood Management](https://github.com/shannongross/Model-Based-Decision-Making)

<br>
## References
Lempert, R. J., & Groves, D. G. (2010). Identifying and evaluating robust adaptive policy responses to climate change for water management agencies in the American west. Technological Forecasting and Social Change, 77(6), 960-974.

Kwakkel, J. H., Walker, W. E., & Haasnoot, M. (2016). Coping with the wickedness of public policy problems: approaches for decision making under deep uncertainty.
