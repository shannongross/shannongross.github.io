---
published: false

layout: post
title: Fundamentals of Discrete Modeling
date: 2018-01-01
description: discrete # Add post description (optional)
img:  # Add image post (optional)
fig-caption:
tags: [modeling, simulation, discrete]
categories: [Modeling]
---
**Article contents:**
- TOC
{:toc}
<br>

# Systems
A **system** is a set of things (T) and a set of relations (R). It has some internal structure and some interaction with the environment during a certain period of time. However, according to Ackoff, a system is more than only its objects and relations - there are independent variables influencing the system and dependent variables (outputs) from the system

<br>
![discrete model system](../assets/img/discrete-model.png){:.post-img-smallest}
<br>

# What is a Model?
**Model**: a specification of a relationship that exists between different variables.
To get an analytic solution to a model, simplifying assumptions are necessary. For instance, replacing the random parameters with their most common/probably value. As a contrast, you can use **simulations** to "retain the effects of randomness when determining the consequences of a model". Consequently, you lose model accuracy but gain the ability to explore model results.



A **model** is a purposeful representation of a system. Any system A is a model of a system B if the study of A is useful for the understanding of B without regard to any direct or indirect causal connection between A and B. The **goal of modeling** is to establish a modeling relation between two systems. Thus, models are designed to be more manageable than working with the actual system, and are used for:
- Understanding the system
- Experimentation ("what if we do this?")

# What is a Simulation?
- Enable us to get results from models when analytical solutions are not available. We can use them to test and explore
- Allow us to get a feel/see how the system behaves
- Take a model and only keep what is absolutely essential to the system.
**Simulation** is the process of designing a model of a real system and conducting experiments with this model for the purpose of understanding the behavior of the system and/or evaluating various strategies for the operation of the system.

Inputs cause changes in the system state and these are reflected by changes in the output.	In a discrete-event simulation, inputs are realized by the arrival of dynamic entities. These entities flow through the system and are the structural elements which effect the changes in the system state variables. Entities have attributes, i.e. characteristics of a given entity that are unique to that entity. An attribute can be anything that can cause a state change. **Events** are conditions that occur at a point in time which cause a change in the state of the system.

There are three major types of activities in a simulation: delays, queues, and logic.
1.	**Delay**: activity occurs when the flow of an entity is suspended for a definite period of time
- If the delay is for d time units, then the entity is scheduled to complete the delay d time units after the current time of the simulation. At that time, the delay expires and another event is generated.
2.	**Queue**: activity occurs when the flow of an entity is suspended for an unspecified period of time
- entities waiting for resources to become available.
3.	**Logic**: activities simply allow the entity to affect the state of the system through the manipulation of state variables or decision logic.
- This decision is determined based on the total number of entities currently waiting in queue for service.

A discrete-event simulation progresses by advancing the clock to the time of the next event, instead of by uniform time-intervals. In this sense the simulation is said to be event driven



# Difference between continuous and discrete modeling
- The way we describe state variable change over time in continuous model is a part-wise continuous differential equation. Constant for a certain part of time
- The way we describe state variable change over time in discrete model is arc-wise constant. Continuous for a certain part of time.
- Computer cannot truly model continuously – they break it up into very small timesteps. This is done via a numerical solver (Euler, Heun, Runge-Kutta)
- Discrete event simulation – jumps from event to event - the next time when something changes
- Paradoxically, time axis of a continuous model has discrete steps. The time axis of discrete model is actually quite continuous (any value can be used – even 0 or extremely small timesteps)
- The timestep matters for the precision to which the differential equation is solved
- A discrete state is a value that only changes at event times (customer arrival, machine breakdown, etc.) A continuous state (e.g. tank level, position of a cart, etc.) has a value that changes continuously over time.

# Gathering data for a model/simulation
Having good data is crucial. The old adage is **garbage in = garbage out**, and for good reason. As you work to develop your data gathering plan, make a distinction between important and less important variables. According to Pareto, its usually only 20% of the variables that determine 80% of the performance.

**Exogenous variables** are the external variables (cannot be influenced from within the system, e.g. foreign taxes, the weather, arrival patterns). Compare this to **Endogenous variables**, which are internal to the system and can be influenced by decision makers (e.g., toll, schedules, number of resources).


## Stochastic Distributions
**Probability distributions** refer to a set of probabilities associated with the results of an experiment.

**Discrete probability distributions** are used in experiments where the outcomes can only be integers. For example, the number of patients that arrive at a particular hospital. Or, the medical devices a factory can produce in one day.
-	Discrete density function: The probabilities on all discrete outcomes of an experiment
-	Discrete distribution function: The cumulative probabilities of the discrete outcomes of a certain experiment

**Continuous probability distributions** are used when an experiment can have any value outcome within some interval. For instance, the amount of time a doctor sees a patient. Or the
-	Continuous density function: Theoretical histogram of all outcomes within a limited interval of an experiment
- Continuous distribution function: The probability of a continuous outcome of an experiment smaller than a certain value

Empirical distribution
| advantages    | Disadvantages     |
| :------------- | :------------- |
| data is used ‘directly’ without any transformations  | Empirical data is not always available |
| can be a representative model of data in reality | data might not be representative |
|   | theoretical distributions might be able to model the distribution realistically over a long period of time |


Theoretical distribution
- Used when data is not available
  - use experience (exponential distribution for arrivals, etc.)
  - use experts to estimate parameters
- Used to replace an empirical distribution
  - make a histogram to look at the shape of the distribution
 - choose a theoretical distribution, either on the basis of the shape, or on theoretical grounds, calculate the parameters from the empirical distribution
 - test hypothesis that distributions do not differ significantly

### Discrete probability distributions
- **Uniform distribution**: To model the outcome of an experiment in which all outcomes have the same probability
- **Bernoulli distribution**: To model the outcome of an experiment with only two outcomes (yes/no)
- **Binomial distribution**: To model the number of successes in n Bernoulli experiments
- **Geometric distribution**: To model the number of Bernoulli experiments up to the first success
- **Poisson distribution**: To model the number of events in a certain time interval. Arrivals are Poisson distributed when…
  - Customers arrive one by one
  - Arrivals are really random (no peaks, no quiet periods)
  - Future arrivals do not depend on previous arrivals

### Continuous probability distributions
- **Uniform distribution**: To model outcomes of an experiment in a limited interval that have equal probabilities
- **Triangular distribution**: To model outcomes of an experiment that are concentrated around b in a limited interval
- **Exponential distribution**: To model random arrival and failure intervals
- **Gamma distribution**: To model the time required to perform a task
- **Erlang distribution**: To model the time required to perform several tasks
- **Normal distribution**: To model throughput times, processing times, etc. [note: negative...]
- **Weibull distribution**: To model the reliability of equipment

### Important measures
- **Expected value**: The average value that can be expected after an infinite number of experiments
- **Variance**: Measure for the degree in which the outcomes of an experiment will deviate from the expected value
- **Discrete uniform distribution**: To model the outcome of an experiment in which all outcomes have the same probability

## Verification and Validation of Simulation Models
- **Model verification**: check the design on the model (the model is correct?). Verification is used for ensuring that the computer program of the computerized model and its implementation are correct .
- **Model validation**: check the numbers (it is the “correct” model?). Validation is a check that the computerized model possesses a satisfactory range of accuracy consistent with its intended application.
  - A model is NOT valid or invalid. It is only more or less valid.

A common strategy for good practice is to use half of your data to build your model and the other half to check it. If you use all of your data building the model, you can’t use it to make any valid predictions.

## Preventing errors
Type I, II and III errors must be prevented.
- Type I (**Model builder’s risk**): The simulation results are rejected when in fact they are sufficiently credible
- Type II (**Model user’s risk**): Invalid simulation results are accepted as if they are sufficiently credible
- Type III: The **wrong problem** is solved and committed when the problem formulated does not completely contain the actual problem


<!--
# Confidence intervals
confidence intervals do not require a priori hypotheses and therefore avoid testing of trivial null hypotheses.
Confidence intervals are easier to understand than significance tests and therefore have a definite instructional advantage over significance tests.


A Thus, the outcome is categorized in a misleading manner. This problem is enhanced by the **arbitrariness of the statistical significance level**, which is commonly set at 5 percent . Thus, the process is fundamentally troubling - on the one hand we introduce a strict cutoff to divide between significant or not, and yet that very cutoff is arbitrarily chosen.


### P-Value Controversy

 -->

<!--
#Extra
Classical statistics is primarily interested in the following two procedures:
1. Estimation
 - assume that the population is described by some distribution (e.g. Gaussian) and try to estimate parameters (e.g. mean, standard deviation) based on the sample set
  - *point estimation* yields a specific value for a single parameter
  - *interval estimation* yields a range of values that the parameter is supposed to lie within -->
