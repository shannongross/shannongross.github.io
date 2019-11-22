---
layout: post
title: "Open Exploration in EMA Workbench - Visualization Examples"
date: 2019-09-09
description: "Visualization tips for open exploration of model objectives using EMA workbench."
img: rotav_OE_title.webp
fig-caption: Open exploration in EMA workbench
tags: [ema workbench, exploratory model, policy analysis with python, deep uncertainty, python visualization]
categories: [Tutorial]
---
As the availability of computational power grows, the potential of exploratory modeling continues to expand. Advancements have been made in fields such as: [water resources](https://doi.org/10.1111/j.1539-6924.2007.00940.x), [policy analysis](https://doi.org/10.1016/j.envsoft.2017.06.054), [ecosystem management](https://www.jstor.org/stable/26270230), and [operations research](https://doi.org/10.1287/opre.41.3.435). Open-source languages like python have supported powerful simulations in becoming more accessible than ever before. One of the most challenging frontiers, however, has been the ability of an analyst to visualize the results of an exploratory model. Visualization is difficult because the results of exploratory modeling are often in the form of high-dimensional information ensembles, making many traditional plotting methods ill-equipped to handle the data. The following article contains some python visualization examples for high-dimensional exploratory modeling output.

* TOC
{:toc}


# Exploratory Modeling Workbench
This post is intended for readers with an intermediate to advanced knowledge of the [EMA workbench](https://github.com/quaquel/EMAworkbench), created by Jan Kwakkel from TU Delft. The EMA workbench documentation and GitHub tutorials contain many examples of how to implement the module. For this article, emphasis is placed on multidimensional visualization techniques for open exploration of the objective space.

In this example, I am using a model that simulates the burden of disease caused by four different infectious pathogens in a community. Here, users are interested in finding combinations of public health policy levers (e.g. providing clean water, sanitation, vaccination, medical treatment) that reduce the burden of disease. The model was created in Vensim (although you can substitute your own model made in python, Netlogo, etc). Readers interested in this multi-disease model can find more details [here](https://github.com/shannongross/multi_disease_model).

The first step to performing open exploration on the model is to import it (in this case, using a `.py` file), along with some standard packages. In this case, I use the function `get_model_for_problem_formulation` to retrieve the Vensim model.


{% highlight ruby %}
# standard packages
import numpy as np
import scipy as sp
import pandas as pd
import time, copy
import seaborn as sns
import matplotlib.pyplot as plt

# EMA workbench imports
from ema_workbench.connectors.vensim import VensimModel
from ema_workbench import (SequentialEvaluator, IntegerParameter, save_results, load_results, Model)
from ema_workbench.em_framework.evaluators import perform_experiments
from ema_workbench.analysis import (pairs_plotting, plotting, plotting_util, feature_scoring, parcoords)
from ema_workbench.util import ema_logging
ema_logging.log_to_stderr(ema_logging.INFO)

# problem-specific imports
from disease_model_problems import get_model_for_problem_formulation
{% endhighlight %}

 One of the advantages of importing the model from a `.py` file is that it makes it easier to incorporate **multiple problem formulations**. I won't cover the benefits of using more than one problem formulation here, but will dedicate a later blog post to it. For readers interested in how I have formulated the problems, you can download the full python file [here](https://github.com/shannongross/code_support/blob/master/disease_model_problems.py).

 Once we have the model and necessary packages imported into our environment, we can move on to the next section where we perform some investigative experiments. This open exploration will allow us to gain an initial understanding of the solution space.


{% highlight ruby %}
# First, retrieve the model. Here, I have more than one way of formulating the model, but we will just use problem formulation 1 in this example.
disease_model = get_model_for_problem_formulation(1)

# Specify the number of different policies to generate and the number of scenarios to test them against.
n_policies = 6
n_scenarios = 20
{% endhighlight %}

Using 20 scenarios and 6 policies, 120 experiments will be performed. Unless your machine is extremely slow, this should not take more than few minutes. You should also liberally experiment with different numbers of scenario-policy combinations during this open exploration phase to get a better impression of your system's behavior.

{% highlight ruby %}
# Incorporate the 'time' module to understand how long the experimental design takes (some designs can take hours or days).
start = time.time()
with SequentialEvaluator(disease_model) as evaluator:
  results = evaluator.perform_experiments(policies=n_policies, scenarios=n_scenarios)
  file_name = './results/open_exploration/PF1_scenarios'.format(n_scenarios) + '.tar.gz'
  save_results(results, file_name)
# Save the file with a descriptive name (here, in the "open_exploration" folder with a name that includes the number of scenarios "n_scenarios")
end = time.time()
str(round((end - start)/60)) + ' minutes')
# Print the amount of time it took to run the perform the experiments. For faster performance, consider using MultiprocessingEvaluator.
print('Simulation time for Problem Formulation 1 is '+
{% endhighlight %}


<br>
## Visualization Examples

### Visualization 1: Pairs Plotting
First, let's try visualizing the results using a [pairs plot](https://emaworkbench.readthedocs.io/en/latest/ema_documentation/analysis/pairs_plotting.html) in order to gain a general first impression of the objective space. In a pairs plot, each objective is paired against every other objective (thus the x- and y-axis labels are duplicated). The EMA workbench includes a pairs plot functionality that creates an R-style scatter multiplot, although you can also use the Seaborn library to accomplish the same thing.

{% highlight ruby %}
# PAIRS PLOT EXAMPLE
# First, retrieve the results from the previous step
file_name = './results/open_exploration/PF1_scenarios'.format(n_scenarios) + '.tar.gz'
results = load_results(file_name)
disease_model = get_model_for_problem_formulation(1)    
experiments, outcomes = results

# Generate Pairs Plots
df_outcomes = pd.DataFrame.from_dict(outcomes)
df_outcomes = df_outcomes.assign(policy=experiments['policy'])
grid = sns.pairplot(df_outcomes, hue='policy', vars=outcomes.keys(),
                        palette=sns.color_palette("bright", 8),plot_kws={'alpha': 0.8})
ax = plt.gca()
fig = plt.gcf()
fig.set_size_inches(12,12)
plt.suptitle('Open exploration under PF1: {}'.format(disease_model.name) , size = 15, y=1.03)
plt.show()
{% endhighlight %}

The result of this is something like the following:

<br>
![pairs plotting](../assets/img/rotav_OE_para.png)

Readers should realize that each objective of the problem formulation is plotted against the other objectives, so the x- and y-axes mirror each other. These scatter plots are useful for providing visual insight into the relations between the different objectives.

<br>
### Visualization 2: 3D Plots
If you have a three-dimensional objective space, you might consider making a 3D plot:

{% highlight ruby %}
## 3D PLOT EXAMPLE
df_outcomes = pd.DataFrame(outcomes)
fig = plt.figure(figsize=(8,8))
ax = fig.add_subplot(111, projection='3d')
ax.scatter(df_outcomes.iloc[:,0], df_outcomes.iloc[:,1],df_outcomes.iloc[:,4], depthshade=100)

# Figure formatting
ax.set_xlabel(list(df_outcomes)[0])
ax.set_ylabel(list(df_outcomes)[1])
ax.set_zlabel(list(df_outcomes)[4])
plt.title('Problem Formulation 1: {}'.format(disease_model.name), fontsize=16)
plt.show()
{% endhighlight %}

As expected, the resulting 3D plot shows the solution space of our three objectives (in this case, *Mortality*, *Morbidity* and *OpEx costs*). In some cases, 3D plots can be useful for identifying interesting clusters of the objective space. In other cases, however, it may be difficult to distinguish meaningful trends. If you don't take care, 3D plots may even obfuscate important information.

![3D plotting python](../assets/img/rotav_OE_3d.png)

<br>

### Visualization 3: Parallel Coordinate Plots

Sometimes, using 3D plotting may not be an effective visualization strategy for high-dimensional spaces. An alternative is to try using [parallel coordinate plotting](https://emaworkbench.readthedocs.io/en/latest/ema_documentation/analysis/parcoords.html), which is often better equipped to handle 3+ objectives.

{% highlight ruby %}
# PARALLEL COORDINATE PLOT EXAMPLE

# Begin by rescaling objectives. Get the maximum and minimum value of each result.
limits = parcoords.get_limits(df_outcomes)
# Set the lower limit of all objectives to zero.
lower_lim = limits.loc[0, list(df_outcomes)]
# Set the upper limit of all objectives to one.
upper_lim = limits.loc[1, list(df_outcomes)]

# Normalize the limits to make tradeoff plots easier to read (same scale)
lower_lim_for_sub = lower_lim
lower_lim_for_sub[2] = 0
upper_lim_for_sub = upper_lim
upper_lim_for_sub[2] = 1
normalized_limits = df_outcomes - lower_lim_for_sub
normalized_limits = normalized_limits/upper_lim_for_sub

# If you want to differentiate by policy, map the experiment set to the objective space.
df_normalized_limits = normalized_limits.assign(policy=experiments['policy'])
df_normalized_limits['policy'] = df_normalized_limits['policy'].map({p:i for i, p in enumerate(set(experiments['policy']))})  
newlimits = parcoords.get_limits(df_normalized_limits)

# Create parallel axis plot
paraxes = parcoords.ParallelAxes(newlimits, fontsize=14,rot=90)
for i,p in enumerate(set(experiments['policy'])):
   paraxes.plot(df_normalized_limits[df_normalized_limits['policy']==i],
                  label=p, color=sns.color_palette("bright", 8)[i],alpha= 0.45)#colors[i])
fig = plt.gcf()
fig.set_size_inches(10,7)
paraxes.legend()
plt.title('Problem Formulation 1: {}'.format(disease_model.name), fontsize=16, y=1.08, loc='right')
plt.show()
{% endhighlight %}

Each line represents a possible policy option, with lines closest to the bottom of the y-axis being performing more favorably in terms of the decision maker’s objectives. The result of the previous code resembles the following:

<br>
![parallel axis plot](../assets/img/rotav_OE_paraplot.png)


<br>
### Visualization 4: Feature Scoring
A final visualization strategy relevant to the open exploration process is known as [feature scoring](https://emaworkbench.readthedocs.io/en/latest/ema_documentation/analysis/feature_scoring.html#module-ema_workbench.analysis.feature_scoring). Feature scoring is a method for testing the effect that different regressors have on a target variable. It is a simple first pass function to help understand the data and to assist with feature selection.

{% highlight ruby %}
# FEATURE SCORES EXAMPLE
x = experiments
y = outcomes
fs = feature_scoring.get_feature_scores_all(x, y)

levers = [l.name for l in disease_model.levers]
df_levers = fs.copy()         
df_levers = df_levers[df_levers.index.isin(levers)]

ax = sns.heatmap(df_levers, cmap='viridis', annot=True)
plt.title('Problem Formulation 1 {}'.format(disease_model.name), fontsize=16)
plt.show()
{% endhighlight %}

<br>
The resulting heatmap shows features that have relatively higher/lower levels of influence on our five objectives. Here for instance, the number of wells constructed (i.e. *Well construction*) has a big effect on the Capital Expenditure outcome (i.e. *CapEx*).

<br>

![feature scoring](../assets/img/rotav_OE_fs.png)

<br>

## Visualizing Open Exploration - Conclusion
Exploratory modeling and analysis is a powerful tool that is growing in popularity for many complex policy problems. Open Exploration is a crucial first step towards achieving the goal of "understanding the factors that make the biggest difference" on policy objectives. Especially in situations where information is deeply uncertain or there are severe data gaps, traditional methods of quantitative modeling that focus on probability or risk are impracticable. Exploratory models are more appropriate for helping decision makers learn about the system and different strategic options, rather than models that use big assumptions to prescribe a single solution.

 In an upcoming blog post, I'll dive deeper into the pros and cons of different visualization methods. I'll also discuss the use of multiple problem formulations. You can view the full Jupyter notebook containing this code <a href="https://github.com/shannongross/code_support/blob/master/OE_Visualization_Example.ipynb" target="_blank">here</a>.
