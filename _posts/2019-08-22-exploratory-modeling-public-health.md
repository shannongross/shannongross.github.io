---
layout: post
title: Using Exploratory Modeling to Support Public Health Policy
date: 2019-08-22
description: Justification for greater use of exploratory modeling in public health policymaking.
img:  exp.webp #public-health.jpg
fig-caption: Evidence-based public health policymaking.
tags: [public health, systems thinking, deep uncertainty, exploratory modeling, multi-disease modeling]
categories: [Modeling]
---

Evidence-based public health policymaking is difficult. One reason for this difficulty is because the “evidence” presented to decision makers is often too specialized to address broad policy concerns. This is especially the case in low-income countries, where evidence to support health policymaking is often lacking or inappropriate (e.g. suggesting overly-technical solutions). Quantitative modelling is useful for simulating the effects of different disease interventions, particularly when testing them in real life would be impractical or unethical. The vast majority of quantitative models, however, are used by researchers to design a control strategy against a single pathogen of interest. Unfortunately, looking at one pathogen in isolation is much less useful from a policy standpoint than it is in a laboratory setting.

Policymakers are rarely interested in a single pathogen under narrowly-defined conditions, being charged more broadly with the general health and welfare of their communities. In the real world, isolating one disease from another is difficult because any decision to invest in a particular intervention is also an implicit decision to not invest in a different strategy. In order to understand which intervention out of many is most worth investing in, policymakers would need to refer to a large number of different disease models. To meet policy concerns, there is a need for models that evaluate across a [wider landscape](https://github.com/shannongross/multi_disease_model/blob/master/report/Evaluating%20multi-disease%20interventions%20report.pdf) of public health issues.

1. TOC
{:toc}
{:.toc-styling}


## Looking at the whole system
Infectious diseases do not spread in isolation. Instead, pathogens are transmitted through complex mechanisms involving human behaviors and external conditions in the environment. This is one reason for incorporating a range of expertise in policy discussions. Additionally, not all decisions related to public health are performed by those with medical expertise. For instance, financial institutions, donor agencies, or water and sanitation engineers are all examples of influential actors on community health who may not have epidemiological backgrounds. Models that incorporate non-medical domains (or at least, are interpretable by those lacking clinical experience) may be useful in multi-actor policy situations.

<br>
![systems thinking in medicine](../assets/img/scopes.webp){:.post-img-smaller}
<br>

To account for complexity and interdisciplinarity, a growing number of researchers are advocating for the application of **systems thinking** to public health issues. Systems approaches account for the complex interrelationships between connected sub-systems and encourage the integration of cross-disciplinary knowledge. Such methods move beyond the traditional methods used in disease epidemiology because they work to account for factors such as: economic mechanisms, community effects, social interactions, ecological factors, and other interdependent elements.

## Models to support policy decisions
Models may help policymakers to compare, contrast, and visualize the potential performance of various options. Such computational testing not only helps to understand the behavior of the system, but can also clarify tradeoffs between different decision objectives. Quantitative models including compartmental and agent-based models have thrived over the past several decades, making great contributions in our knowledge of infectious diseases. However, recent studies suggest that the success of models to [influence policy](https://arxiv.org/abs/1607.07398) debates has been rather limited. Critics have argued that models often exclude, ignore, or simplify precisely those aspects that make public policy problems so formidable. Furthermore, models often fail to answer many of the key questions asked by policymakers.

A critical instance of models failing to support policy decisions occurs when the model itself is difficult for policymakers to understand, not only due to the use of technical jargon but due to simplifying assumptions used to create the model. It is unavoidable that any model will contain assumptions that simplify reality, but while the assumptions chosen may be obvious and rational to the modeler, to the policymaker the simplifications may appear to be biased and misguided. Ideally, the modeler and policymaker would build the model together, ensuring that the parameter assumptions are fully understood and agreed upon. However, public health policies are rarely decided by a single actor. In multi-actor policymaking processes – especially where the actors have wildly different worldviews – it may be impossible to achieve consensus on modelling assumptions.

## Deeply uncertain policy situations
Modelling assumptions are necessary in cases of uncertainty. Uncertain parameters – such as how often people come into contact with infectious material and what proportion of infected individuals are likely to die – cannot be known exactly, but the modeler may use literature estimates and probability distributions to make an acceptable approximation. In some cases, the uncertainty can be reduced through further laboratory experimentation or data collection. In other cases, the uncertain parameter is so unknown that it is irreducible even if additional data is collected – greatly increasing the difficulty for modelers and decision makers alike. In multi-actor situations, policymakers may disagree about what values or structures best represent these parameters, leading to a situation of “deep uncertainty.”

[Deep uncertainty](https://www.sciencedirect.com/science/article/pii/S1364815212003131) refers to a situation where the various parties to a decision do not know or cannot agree on how the system works; how likely various possible future states of the world are; and how important the various outcomes of interest are. Accordingly, deep uncertainty problems are often contentious. From a  modeler’s perspective, this means that there are many plausible model structures that could be used; a variety of perspectives on how to formulate the main objectives; and different ideas about what the optimal solution sets are. In situations of deep uncertainty, traditional decision analysis methods may be insufficient to assist decision makers in coming up with strategies to achieve their objectives.

<br>
![exploratory versus predictive modeling](../assets/img/public-health.webp){:.post-img-smaller}
<br>

The classic use of modelling to support decision making tries to predict future outcomes with computational simulation, but such approaches are ill-equipped to handle [deep uncertainty](https://www.sciencedirect.com/science/article/pii/S1364815217301251). If even forming a “best-guess” probability distribution of a particular uncertainty is unsuitable or impossible, then traditional models may be unable to support decision-making. Thus, rather than falsely trying to reduce an irreducible uncertainty – or avoiding creating a model about the topic at all – modelling techniques that are able to systematically explore deep uncertainty values are needed.

Predictive modelling tools applied to the public health sector are often unsuitable when transmission parameters are highly uncertain or data are scarce. In light of this, exploratory (rather than predictive) modelling techniques can be used for learning about the behavior of the public health system. **Exploratory modelling** entails investigating the behavior of highly complex and uncertain systems through computational experiments (Bankes, 1993; Bankes et al., 2013). Each model run is an experiment to test how a particular decision would perform if that plausible situation came to pass (J. Kwakkel & Haasnoot, 2018). Exploratory modelling can be a powerful tool for helping public health policymakers gain insights that are important for decision-making, even when the situation is highly complex and deeply uncertain.


## References
Saltelli, A., & Giampietro, M. (2015). The fallacy of evidence based policy. arXiv preprint arXiv:1607.07398.

Kwakkel, J. H. (2017). The Exploratory Modeling Workbench: An open source toolkit for exploratory modeling, scenario discovery, and (multi-objective) robust decision making. Environmental modelling & software, 96, 239-250.

Kasprzyk, J. R., Nataraj, S., Reed, P. M., & Lempert, R. J. (2013). Many objective robust decision making for complex environmental systems undergoing change. Environmental Modelling & Software, 42, 55-71.
