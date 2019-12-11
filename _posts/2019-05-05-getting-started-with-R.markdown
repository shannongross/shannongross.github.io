---
published: true

layout: post
title: "A Python Lover's Guide for Getting Started with R"
date: 2019-05-05
description: A python lover's guide for getting started with R
img:  R-intro.webp
fig-caption: Introduction to R programming
tags: [R for policy analysis, statistics for data science, beginner machine learning, jupyter notebook, caret]
categories: [Tutorial]
---

1. TOC
{:toc}
{:.toc-styling}

# Setting up an R-environment using Anaconda
Online, you'll find lots of R Intro courses that will tell you the first thing to do is to download RStudio. [RStudio](https://rstudio.com/) is a powerful, interactive IDE for R development - and there are many sources that will show you how to download it so I won't cover that here. Instead, I'll show you how to use R in Jupyter notebook, which is an alternative interactive interface that may be more familiar to anyone coming from a python background. While not the "typical" way of getting started with R, I find it to be a comfortable alternative. It is easy enough to use Anaconda to manage virtual environments and packages for R, and to write R-scripts in Jupyter.

If you have [Anaconda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) downloaded, you can create a new R-environment from the command line (conda shell), by typing:
`conda create -n renv`
  where `renv` is the name of your R environment

Activate this new R-environment using:
`conda activate renv`

Install all of the basic R packages you'll need using a convenient bundle called 'r-essentials':
`conda install r-essentials`
(Note: if you're having trouble, try just *conda install r-base* first. )

## Common R Packages
While r-essentials is downloading, let's go over what these common R packages are that you'll be using:
- [tidyverse](https://www.tidyverse.org/): includes core packages for common data analyses. When you import this library, it comes with the following:
  - ggplot2: for making nice graphs
  - dplyr: Manipulation/cleaning
  - tibble: lazy dataframes
  - tidyr: to get "tidy" data

- non-tidyverse libraries:
  - caret: main machine learning library in R
  - lubridate: for datetime manipulation
  - jsonlite for JSON


Once your conda R environment is activated, you can now launch Jupyter notebook (just like you're used to in Python), by typing:
`jupyter notebook`

Create a new R notebook and start testing.

## Boulder, CO traffic stop demographics
For this example, we'll use the open data set provided by the City of Boulder, CO concerning police traffic stops. You can follow along by downloading the full dataset [here](https://bouldercolorado.gov/open-data/police-stop-demographics/). It contains the following features:


|Name|	Description |
|:--|:--|
|stopdate|	Date of the stop |
|stoptime|	Time (in 24 hour format) when the stop began |
|streetnbr|	Street number where stop occurred |
|streetdir|	Direction of street |
|street|	Street or intersection where stop occurred |
|Min|	Duration of the stop, in minutes |
|sex|	Sex of the individual stopped |
|race|	A=Asian, B=Black or African American, I=American Indian or Alaskan Native, U= Unknown, W=White |
|ethnic| Ethnicity of the individual stopped. H=Hispanic, N=Non-Hispanic |
|Year of birth|	Year of birth of the individual stopped. Typos may be present due to manual entry of this field. |
|enfaction|	Whether the individual is a city of Boulder resident|
|rpmainid|	Unique identifier for the stop |
|appkey	| Type of Police activity as part of the stop |
|appid|	Unique identifier for the stop |


First, begin by importing the dataset and essential R packages:

{% highlight ruby %}
## Libraries to include
library(tidyverse)
library(lubridate) #date wrangling

## Load data
data_file <- "police_data/police_stop_data_main_2018.csv"
df_stops <- read.csv(data_file, , na.strings="")
{% endhighlight %}


## Inspect the traffic stop data
We can inspect the traffic stop dataframe using any of the following commands: `colnames(df_stops)`, `str(df_stops)`, `head(df_stops)`. Another option (which I prefer) is to use the `skimr` library, which we can import and then use to get a nice overview table of the traffic stop data:

{% highlight ruby %}
library(skimr) #for easy descriptive statistics
skim_to_wide(df_stops)
{% endhighlight %}

![R skim dataframe summary](../assets/img/R-intro-skim.png){:.post-img-normal}

<br>

To get subsets of the full dataframe, we can use `filter()` to choose certain rows and `select()` to choose certain columns.

{% highlight ruby %}
## Filter rows
youth_stops <- filter(df_stops, Year.of.birth < 2000)
nrow(youth_stops)

## Select columns
df_stops_subset <- select(df_stops, stopdate, Min, sex,race,ethnic,Year.of.birth)
head(df_stops_subset)
{% endhighlight %}

## Helper functions you can use with `select()`
``starts_with("abc")``: matches names that begin with “abc”.

``ends_with("xyz")``: matches names that end with “xyz”.

``contains("ijk")``: matches names that contain “ijk”.

``matches("(.)\\1")``: selects variables that match a regular expression. This one matches any variables that contain repeated characters. You’ll learn more about regular expressions in strings.

``num_range("x", 1:3)``: matches x1, x2 and x3

## Using `mutate()` to create new columns
Rather than just examining existing features, we can use `mutate()` to create new ones.
{% highlight ruby %}
df_stops_subset <- mutate(df_stops_subset,
                          stop_month = month(as.POSIXlt(df_stops_subset[['stopdate']],
                                             format="%m/%d/%Y")),
                          stop_year = year(as.POSIXlt(df_stops_subset[['stopdate']],
                                            format="%m/%d/%Y")))

head(df_stops_subset)
{% endhighlight %}

We now have new columns 'month' and 'year' that we can select by.

## Pipe operator `%>%`
The Pipe `%>%` is used for continuing an operation without assigning it to a new variable, and is very common in R.
{% highlight ruby %}
#number of stops by race
df_stops_subset %>%
  count(race)
{% endhighlight %}

| race | n |
| :--: | :----:|
| A |	306 |
| B	| 346 |
| I |	33 |
| U	| 9 |
| W	| 7352 |
{: .post-table-small}

This gives us the breakdown in traffic stops by race:
- A=Asian
- B=Black or African American
- I=American Indian or Alaskan Native
- U= Unknown
- W=White

We are also ready to do a more complicated pipes:
{% highlight ruby %}
## Fraction of stops by race
df_stops_subset %>%
  count(race) %>%
  mutate(proportion = n / sum(n))
{% endhighlight %}

| race | n | proportion |
| :--: | :----:| :--: |
|A | 306	 | 0.038031320|
|B | 	346 | 	0.043002734|
|I	 | 33 | 	0.004101417|
|U	 | 9|	0.001118568|
|W	 | 7352	 | 0.913745961 |
{: .post-table-small}

We're starting to get some more interesting values from the original data, but what do these numbers look like? Let's try generating some figures using R's powerful `ggplot2` library.

## Visualization using `ggplot2`
{% highlight ruby %}
### Bar plot 1
barplot1 <- ggplot(df_stops_subset, aes(y = Min, x = ethnic))+
  geom_bar(
    aes(fill = sex), stat = "identity",
    position = position_dodge(.9))

barplot1 + ggtitle("Duration of traffic stop by gender and ethnicity")
{% endhighlight %}

![R barplot ethnic gender](../assets/img/R-intro-barplot1.png){:.post-img-smaller}

Interesting. Non-Hispanic women seem to have longer traffic stops. What if we look at gender across races, instead of ethnicity?

{% highlight ruby %}
### Bar plot 2
barplot2 <- ggplot(df_stops_subset, aes(y = Min, x = race))+
  geom_bar(
    aes(fill = sex), stat = "identity",
    position = position_dodge(.9))

barplot2 + ggtitle("Duration of traffic stop by gender and race")
{% endhighlight %}
![R barplot race gender](../assets/img/R-intro-barplot2.png){:.post-img-smaller}

Again the graph is interesting. For all races except W, the total amount of minutes women are pulled over is much less than men. But is the *total* amount of minutes an appropriate way to look at it? Wouldn't the *average* length of the traffic stop be a better indicator?

{% highlight ruby %}
### Bar plot 3
barplot3 <- ggplot(df_stops_subset, aes(y = Min, x = race))+
  geom_bar(
    aes(fill = sex), stat = "summary", fun.y = "mean",
    position = position_dodge(.9))

barplot3 + ggtitle("Average duration of traffic stop by gender and race")
{% endhighlight %}
![R traffic stop average race](../assets/img/R-intro-barplot3.png){:.post-img-smaller}

This graph showing the *average* length of a traffic stop is closer to what we might expect - there duration is pretty much the same across the sexes regardless of race. The exception is the "U" category, but because this is unknown we cannot draw any meaningful conclusion.

## Visualizing traffic stop by year of birth
{% highlight ruby %}
ggplot(data = df_stops_subset, mapping = aes(x = Year.of.birth, y = Min) +
    geom_point(mapping=aes(color = race))
{% endhighlight %}
The result looks like:
![R scatter plot race](../assets/img/R-intro-race-vs-age.png){:.post-img-smaller}

Can you see anything interesting about the driver's race and their age? Me neither. That's because this plot shows that some of the people being pulled over in Boulder are at least 1,000 years old (they probably shouldn't be behind the wheel). Other drivers haven't even been born yet, since their 'Year.of.birth' is around year 3000.

Clearly, the original dataset contains some mistakes that need to be cleaned. In the next post, I'll review this in R along with the popular machine learning package called [caret](http://topepo.github.io/caret/index.html).
