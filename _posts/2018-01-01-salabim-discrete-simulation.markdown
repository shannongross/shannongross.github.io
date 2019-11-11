---
published: true

layout: post
title: Salabim Discrete Modeling Tutorial
date: 2018-01-01
description: discrete # Add post description (optional)
img:  water-well-collection.webp # Add image post (optional)
fig-caption: Using a DES model to simulate women queueing at a water collection point
tags: [discrete modeling, Salabim, water well simulation, WASH model, water policy analysis]
categories: [Modeling]
---
Figuring out the best way to route components through a system is a complicated problem, with many real-world applications. For example, disaster responders may want to know the best way to distribute relief items after a hurricane. Or, hospital administrators may want to know the best way to set up their rooms to ensure patients are seen as quickly as possible. In either of these examples, the problems are too critical to just find the best way through trial-and-error. Instead, it can be highly useful to create a **simulation**, which models the transport of relief goods or patients through a process. In the following article, I'll cover some key points on simulations as well as how you can start building your own for free using the Salabim library in Python.

**Article contents:**
- TOC
{:toc}
<br>

# Discrete Event Simulation (DES)
A model helps to perform "what if?" analysis, where questions about the system are posed and tested in the simulation, helping decision makers prepare for different future scenarios. Injecting elements of stochasticity help reflect the uncertainty inherent in the real world and can provide a better understanding of the system. **Discrete event simulation** in particular, is well-suited to problems where components change at different points in time as a result of events. Between two consecutive events, the system is assumed to be steady-state, so the simulation effectively skips from one event to the following event. This is different than **continuous simulation**, where the dynamics of the system are tracked over time uninterrupted.

<br>
![discrete vs continuous model](../assets/img/discrete-cont.jpg){:.post-img-med}
<br>


## Salabim Tutorial
One library for discrete simulation is **Salabim**, an open-source python library. There are many alternatives for performing discrete simulation (for instance, see [this Wikipedia list](https://wiki2.org/en/List_of_discrete_event_simulation_software)) however, many of them have considerable learning curves and expensive licenses.

The Salabim library was written by Ruud van der Ham, an expert in discrete modeling from the Netherlands, who wrote the library to make discrete modeling more accessible to python users. The library can be installed easily using pip:

`pip install salabim`

Documentation and examples are available [here](https://www.salabim.org/manual/index.html).


### Components
To begin modeling in Salabim, the most important part of the library to understand are **components**. Components are defined as classes in Salabim, using the syntax `sim.Component`. Unlike traditional definitions in python however, Salabim components do not *return* something, they *yield* something. Basically, the best way to create a component is to define it like so:
{% highlight ruby %}
    class Patient(sim.Component):
        def process(self):
            ....
{% endhighlight %}

<!-- A **generator** is a function with at least one yield statement, which are used as a signal to give control to the sequence mechanism. -->

<!-- When yield is followed by self, it means that it is the component to be held for some time -->

There are two kinds of components in Salabim simulations: data components and active components.


#### (1) Active components
An active component contains one or more **processes**. To create an active component, you have to define a class first, and then you can add processes (which usually contain at least one yield statement).
{% highlight ruby %}
    class Doctor(sim.Component):
        def process(self):
        ...
        yield ...
        ...
{% endhighlight %}

Once this class is created, it is then *activated* at some point in time. you can activate the class you created by making a new instance of the class:
{% highlight ruby %}
     doctor_1 = Doctor()
     doctor_2 = Doctor()
     doctor_3 = Doctor()
{% endhighlight %}

An active component can later become a data component through one of two ways: (1) using *cancel* or (2) by reaching the end of its process. If no processes are found in a class you created, it will be treated as a data component.

#### (2) Data components
A data component is one that has no associated process method. To create a data component, simpy use:
`data_component = sim.Component()`

You can make a data component active later by means of an activate statement.
{% highlight ruby %}
     nurse1 = Nurse()
     nurse1.activate(process='treat')
{% endhighlight %}

## Water collection example
In this example, we'll use Salabim to simulate women walking to a public well in order to fill up a container of water. Today, [tens of millions of women](https://www.npr.org/sections/goatsandsoda/2016/07/07/484793736/millions-of-women-take-a-long-walk-with-a-40-pound-water-can) still walk long distances to collect water for household use. These water containers are heavy and bulky (generally weighing 40 pounds or more) and trips take 30 minutes or longer. Often, multiple trips are taken per day.

### Simulation setup
We'll create the following processes:
- The <span style="color:violet">**person generator**</span> creates the women, with a uniform inter arrival time.
- The <span style="color:violet">**women**</span> who visit the well. They wait in a queue and are served in a first-in, first out order.
- The <span style="color:violet">**water well**</span> collection point, which we'll model as a *resource* in Salabim.
  - Resources have a limited capacity, just like our water collection point. They are useful for simulation because they can be claimed by components and released later, which is the case here because not every woman who arrives can fill her bucket all at once. Instead, they must form a queue.

To make things a little more interesting, we'll also include two environmental features:
- The **number who turn around** when they arrive at the well and see that the line is too long.
- The **number who leave early** after waiting in the queue for a long time.

{% highlight ruby %}
import salabim as sim

class PersonGenerator(sim.Component):
    def process(self):
        while True:
            Woman()
            yield self.hold(sim.Uniform(5, 25).sample())
            #Uniform sample time between 5 and 25 minutes until next person is created

class Woman(sim.Component):
    def process(self):
        if len(well.requesters()) >= 5:
            env.num_turn_around += 1   #women who turn around because lines are too long
            env.print_trace("","","Too many other people in line, turned around.")
            yield self.cancel()        #this makes the current component a data component if queue length is greater than 5 people
        yield self.request(well, fail_delay=50)
                                       #if the request is not honored within 50 time units,
                                       #the process continues to next statement
        if self.failed():              #check if the request failed
            env.num_leave_early +=1    #women who turn around because they have waited in queue too long
            env.print_trace("","","Waited in line too long, left queue early.")
        else:
            yield self.hold(50)
            self.release()

##Setup the Environment         
env = sim.Environment()        #create environment
PersonGenerator()              #activate component
env.num_turn_around = 0        #initialize list
env.num_leave_early = 0        #initialize list
well = sim.Resource("well", 3) #3 places where women can fill up at the well resource

##Run the simulation for 2000 time units
env.run(till=2000)

##Display key information
well.requesters().length_of_stay.print_histogram(30,0,10)
print("number who turned around when seeing the line length: ", env.num_turn_around)
print("number who waited too long and left early: ", env.num_leave_early)
{% endhighlight %}

You can download the full Jupyter notebook of this example from [my github page](https://github.com/shannongross/website_tutorials/tree/master/salabim_discrete_example).
