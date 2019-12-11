---
published: false

layout: post
title: "Multi-Disease Modeling"
date: 2019-09-09
description: ""
img:
fig-caption:
tags: [multi-disease model, modeling multiple pathogens, transmission pathways, exploratory model, deep uncertainty]
categories: [Writing]
---

While infectious disease models have thrived in recent decades for their ability to provide a great deal of insight into pathogen behavior, they have been less successful in supporting public health policymaking where concerns go beyond the properties of a single pathogen. This research gap is crucial because many infectious diseases share similar control strategies. From a public health policy perspective, how does the consideration of multiple pathogens in a single model change the formulation of an “optimal” control strategy? Here, a multi-disease model highlights how strategic investments in different public health interventions translate to higher-level policy objectives. The hypothesis driving this model is that the recommended policy will change depending on whether decisionmakers are presented with a single-disease or multi-disease problem formulation.

1. TOC
{:toc}
{:.toc-styling}

# WASH-Related Disease in Uganda
Uganda is a low-income country that has struggled for decades against widespread prevalence of many infectious diseases. According to the Ugandan Ministry of Health, diseases related to hygiene and sanitation currently contribute over 70% of the overall disease burden 1. Inadequacies in local water, sanitation, and hygiene (WASH) conditions are significant risk factors that cause fecal pathogens to be passed on to susceptible hosts. WASH-related diseases are an appropriate test case for the multi-disease model because there is a relatively limited set of interventions which are effective at stopping a large variety of different pathogens.
To reduce the burden of WASH-related disease, policymakers may consider options such as: improving drinking water quality, increasing water supply, increasing latrine access, and promoting hygiene education. These are promising strategies for alleviating the associated disease burdens, although the exact extent of the effectiveness depends on pathogen-specific characteristics. While there is a great deal of overlap in the strategies to prevent or control fecal-oral pathogens, it is unlikely that policymakers have the resources to implement all interventions at once. Yet, no guide has been developed as to how interventions from the WASH sector can be strategically optimized for alleviating disease burden.

## Exploratory modeling approach
The case study investigated various WASH and clinical methods for combatting the spread of Rotavirus, *Ascaris lumbricoides*, *Cryptosporidium*, and *Escherichia coli* in Uganda. The compartmental model included five age cohorts and was based on the Susceptible-Infectious-Susceptible (SIS) structure widely used in epidemiology. Data used to parameterize the model were obtained from previously published aggregate sources and thus did not require ethical approval. The model was constructed using Vensim system dynamics software and validated against available, open source information. Model experimentation was facilitated by the open source Python library known as the [exploratory modeling workbench](https://github.com/quaquel/EMAworkbench) by J. H. Kwakkel.

## Model Conceptualization
Conceptually, the multi-disease model was outlined using the XLRM Framework by [Lempert et al.](link) which organizes the model’s main objectives, policy levers, uncertainties and relationships.

Summary of XLRM Framework


- **Levers (L)**: Levers refer to the policy options that the decision makers have control over or an ability to influence. Policymakers may increase or decrease the values of these levers to try and achieve their objectives.   
- **Uncertainties (X)**: The exogenous factors that are beyond the control of policymakers and cannot be predicted in advance, yet heavily influence policy performance. Ideally, the chosen strategy would be relatively insensitive to shifts in these uncertainties.
- **Outcomes (M)**: Refers to the performance metrics of interest to the health policymaker(s).
- **Relationships (R)**: Relationships are the internal connections between parameters that determine how combinations of levers and uncertainties translate to different performance outcomes.

The model includes nine policy levers that are under control of public health policymakers; seven deeply uncertain exogenous factors that affect the system; and five conflicting objectives that ideally should all be minimized. The system diagram is outlined in the figure below.

![multiple disease model system](../assets/img/multi-disease-model-xlrm.png)

While the ability of these policy levers to reduce the burden of the infectious pathogens mentioned here are widely agreed upon, the quantification of these relationships is deeply uncertain. The next section provides a brief discussion about data availability for the relationships described.

### Data Gaps
The data used to parameterize the model were obtained from online, open-source databases. The data regarding disease prevalence in Uganda is secondary information gathered from online, open source databases and documents, which were originally collected by government agencies or non-governmental organizations. Similarly, information surrounding the transmission of pathogens of interest were taken from published cohorts, clinical trials, and meta-analyses. This information was synthesized into a single database for purposes of this model application (a link to the database is provided in Appendix ##). These parameters were held fixed during model runs. This section describes data availability and limitations for purposed of model formalization.

## Model Formalization
To evaluate the impact and potential tradeoffs of different intervention strategies, a system dynamics model of five age cohorts and four infectious pathogens in Uganda was developed. The model was created using the System Dynamics software known as Vensim ® DSS 7.3.5. The model was instantiated from starting year 1990 until year 2040, with policy experiments beginning in year 2020. Data about each cohort were extrapolated from the 1991 and 2014 censuses administered by the Uganda Bureau of Statistics (Information from http://data.un.org). Data generated for the period 1990 to 2019 was used for historical calibration of the model results. Additional model details are available in Appendix #. Experimentation occurred for the years 2020 to 2040 by systematically changing the values of the unknown parameters (Fig #) between their plausible maximum and minimum values.

## Experimentation
The ability of a public health policy to achieve its objectives ultimately depends on many uncertain factors beyond of the control of policymakers. Traditionally, this uncertainty is accounted for by using an expected value from on an established probability distribution. However, this is difficult in situations of deep uncertainty, when stakeholders do not agree on the likelihood or impact of a particular uncertainty on the system. An alternative is to test policy performance against a wide range of values for these unknown parameters, thus stakeholders do not need to agree on the probabilities of these parameters upfront.

## Using Various Problem Formulations
Since MORDM does not require assumptions about policymaker preferences before determining the Pareto front, this approach represents a posteriori decision support (Kasprzyk et al., 2013). MORDM was selected for this analysis because of this benefit of enabling the decision maker to gain an understanding of a larger set of superior solutions without the premature aggregation of performance measures. Ultimately, it is up to the decision maker to select the final policy once these trade-offs between different options are made clear. Though to the author’s knowledge MORDM has not been used so far to inform public health policymaking, the approach holds great potential for supporting experts in discovering, analyzing, and fine-tuning health development policies.





# Methods and Findings

Information on four gastroenteric pathogens common to low-income countries (Rotavirus, *Ascaris lumbricoides*, *Cryptosporidium*, and *Escherichia coli*) was used to create a system dynamics model instantiated for 122 districts in Uganda. The model uses publicly available information to estimate the prevalence of disease and project that information until year 2040. Where data was missing or deeply uncertain, parameter values were systematically explored with the goal of finding policy options that are relatively insensitive to these unknowns. Sub-models of different intervention strategies commonly employed in development settings were created to understand their potential effectiveness against each of the four pathogens at meeting long-term policy objectives. Intervention strategies included: groundwater well installation, household water treatment with chlorine, rotavirus vaccination, hygiene education, latrine construction, oral rehydration treatment promotion, and mass drug administration. The impacts of these control strategies were evaluated against four policy objectives: (1) morality reduction; (2) morbidity reduction; (3) upfront investment cost; and (4) maintenance or administration costs over time.
The findings provide a proof of concept model for guiding evidence-based public health policymaking when faced with multiple diseases and many (conflicting) objectives. When problem objectives were formulated in terms of a single disease, the range of policy options were sub-optimal compared to a multi-disease formulation.

#### Why was this study done?
* While a great deal of detailed research exists concerning the characteristics of individual infectious diseases, this information is unable to support policymakers in deciding how they should allocate limited resources among a large number of different public health concerns. For policymakers with finite resources, any decision to invest in an intervention against one disease as also an implicit decision to not invest in controlling another disease.
* To date, no quantitative models have been developed to design control strategies that take into account multiple diseases for purpose of supporting policy decisions in deeply uncertain environments. Traditional methods of predictive modeling are ill-suited to this endeavor because of: large data gaps, unknown future scenarios, and the subjectivity surrounding which diseases/objectives ought to be prioritized.









<!-- ##What did the researchers do and find?
* This research adopts an exploratory modeling and analysis approach in order to create a multi-disease model and evaluate its findings in the presence of uncertainty.
* The multi-disease model was developed by extending the SIS model to contain compartments for four widespread infectious pathogens in Uganda (Rotavirus, *Ascaris lumbricoides*, *Cryptosporidium*, and *Enterotoxigenic Escherichia coli*). Because transmission of these four pathogens are all exacerbated by inadequate water, sanitation and hygiene conditions, there is a great deal of overlap in their control strategies.
* Sub-models of intervention strategies common to low-income communities (e.g. well construction, drinking water treatment, latrine construction, hygiene education, vaccination) were included. These parameters were systematically explored using many-objectives optimization techniques in order to find policies that perform well at minimizing conflicting policy objectives (mortality, morbidity, cost, etc) across the spectrum of pathogens considered.
* The findings of this exploratory multi-disease model indicate that problem perspectives which focus on controlling a single pathogen produce different recommendations than model formulations which take more than one infection into account, even if the pathogens share many of the same intervention strategies. -->

## Conclusions
This study introduces a novel exploratory multi-disease model, which can be used to support policy decisions and identify robust options for efficiently targeting more than one pathogen, even when data are scarce. A multi-disease model may be used to develop integrated solutions, by seeking interventions that work well against more than one public health concern concurrently. Due to the presence of data gaps and uncertainties, a multi-disease decision support tool is likely better suited to exploratory modeling and analysis approaches that are equipped to handle them.
The model is advantageous in its ability to provide one system for comparing interventions, over current methods requiring policymakers to refer to many different single-disease models. The primary benefit of this is to support policymakers in comparing different strategic ideas for using limited public health resources. Going forward, researchers should strive to support policymaker decisions by putting interventions within a broader, whole-system context.

## Path Forward: recommendations
* Policymakers interested in finding optimal uses of their limited resources may need to consider more than one disease at a time. The multi-disease formulation is advantageous for finding integrated solutions that work well across different pathogens, ideally to reduce wasted resources.
* Where information is deeply uncertain or there are severe data gaps, traditional methods of quantitative modeling that focus on probability or risk are impracticable. Public health modelers may provide more policy-relevant support by adopting a systems approach and exploring (rather than assuming away) critical uncertainties.





#
