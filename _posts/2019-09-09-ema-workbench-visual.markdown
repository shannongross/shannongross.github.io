---
layout: post
title: "Open Exploration in EMA Workbench - Visualization Examples"
date: 2019-09-09
description: Visualization tips for open exploration of model objectives using EMA workbench # Add post description (optional)
img: rotav_OE_title.png # Add image post (optional)
---
This post is intended for readers with an intermediate knowledge of the [ema workbench](https://github.com/quaquel/EMAworkbench) by Jan Kwakkel. The ema workbench documentation and GitHub tutorials contain many examples of how to implement the module. Here, emphasis is placed on visualization techniques.

In this example, I am using a model that simulates the burden of disease caused by four different infectious pathogens in a community. Users are interested in finding combinations of public health policy levers (e.g. providing clean water, sanitation, vaccination, medical treatment) that reduce the burden of disease. The model was created in Vensim (although you can substitute your own model made in python, Netlogo, etc). The first step in exploring this **multi-disease model** is to import the model and standard packages:

<br>
### Import packages
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
from ema_workbench import (SequentialEvaluator, IntegerParameter,
  save_results, load_results, Model)
from ema_workbench.em_framework.evaluators import perform_experiments
from ema_workbench.analysis import (pairs_plotting, plotting, plotting_util, feature_scoring, parcoords)
from ema_workbench.util import ema_logging
ema_logging.log_to_stderr(ema_logging.INFO)

# problem-specific imports
from disease_model_problems import get_model_for_problem_formulation
{% endhighlight %}

I use the function `get_model_for_problem_formulation` to retrieve the Vensim model. One of the advantages of importing the model from a .py file is that it makes it easier to incorporate **multiple problem formulations**. I won't cover the benefits of using more than one problem formulation here, but will dedicate a later blog post to it. For readers interested in how I have formulated the problems, you can view the full file [here](https://github.com/shannongross/code_support/blob/master/disease_model_problems.py). Otherwise, we can move to the open exploration section:

<br>
# Open Exploration Using Randomly Generated Policies
{% highlight ruby %}
disease_model = get_model_for_problem_formulation(1)
# First, retrieve the model. Here, I have more than one way of formulating the model, but we will just use problem formulation 1 in this example.
n_policies = 6
n_scenarios = 20
# Specify the number of different policies to generate and the number of scenarios to test them under
start = time.time()
with SequentialEvaluator(disease_model) as evaluator:
  results = evaluator.perform_experiments(policies=n_policies, scenarios=n_scenarios)
  file_name = './results/open_exploration/PF1_scenarios'.format(n_scenarios) + '.tar.gz'
  save_results(results, file_name)
# Save the file with a descriptive name (here, in the "open_exploration" folder with a name that includes the number of scenarios "n_scenarios")
end = time.time()
print('Simulation time for Problem Formulation 1 is '+ str(round((end - start)/60)) + ' minutes')
# Print the amount of time it took to run the perform the experiments. For faster performance, consider using MultiprocessingEvaluator
{% endhighlight %}

Using 20 scenarios and 6 policies, 120 experiments will be performed. Unless your machine is extremely slow, this should not take more than few minutes. Next, we can visualize the results using a **paraplot** in order to gain a general first impression of the objective space.

{% highlight ruby %}
file_name = './results/open_exploration/PF1_scenarios'.format(n_scenarios) + '.tar.gz'
# First, retrieve the results from the previous step
results = load_results(file_name)
disease_model = get_model_for_problem_formulation(1)    
experiments, outcomes = results

# Make pairplots
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
![MOEAs](../assets/img/rotav_OE_para.png)

Readers should realize that each objective of the problem formulation is plotted against the other objectives, so the x- and y-axes are duplicated.

<br>
# Visualize objective tradeoffs using 3D plots
To look at more than one objective at a time

{% highlight ruby %}
df_outcomes = pd.DataFrame(outcomes)
fig = plt.figure(figsize=(8,8))
ax = fig.add_subplot(111, projection='3d')
ax.scatter(df_outcomes.iloc[:,0], df_outcomes.iloc[:,1],df_outcomes.iloc[:,4], depthshade=100)
ax.set_xlabel(list(df_outcomes)[0])
ax.set_ylabel(list(df_outcomes)[1])
ax.set_zlabel(list(df_outcomes)[4])
plt.title('Problem Formulation 1: {}'.format(disease_model.name), fontsize=16)
plt.show()
{% endhighlight %}

![MOEAs](../assets/img/rotav_OE_3d.png)
<br>

# Visualize objective tradeoffs using parallel coordinate plots
If there are more than 3 objectives, using 3d plots may not be that effective. Instead, we can try using parallel coordinate plots, which are better equipped to handle many objectives.

{% highlight ruby %}
limits = parcoords.get_limits(df_outcomes)
# Get the maximum and minimum value of each objective result
lower_lim = limits.loc[0, list(df_outcomes)]
# Set the lower limit of all objectives to zero
upper_lim = limits.loc[1, list(df_outcomes)]
# Set the upper limit of all objectives to one

lower_lim_for_sub = lower_lim
lower_lim_for_sub[2] = 0
upper_lim_for_sub = upper_lim
upper_lim_for_sub[2] = 1
normalized_limits = df_outcomes - lower_lim_for_sub
normalized_limits = normalized_limits/upper_lim_for_sub
# Normalize the limits to make tradeoff plots easier to read (same scale)

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

The result of this resembles the following:

<br>
![MOEAs](../assets/img/rotav_OE_paraplot.png)

Each line represents a possible policy option, with lines closest to the bottom of the y-axis being performing more favorably in terms of the decision maker’s objectives.

<br>
# Feature Scoring
Finally, feature scoring:

{% highlight ruby %}
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

![MOEAs](../assets/img/rotav_OE_fs.png)

<br>
You can view jupyter notebook containing this code at: [link](https://github.com/shannongross/code_support/blob/master/OE_Visualization_Example.ipynb)

In an upcoming blog post, I'll dive deeper into the pros and cons of different visualization methods. I'll also discuss the use of multiple problem formulations.
