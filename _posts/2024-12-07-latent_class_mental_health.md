---
title:  "Mental Health in University Students: A Latent Class Introduction and Analysis"
tags:
    - R
    - unsupervised learning
---

<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

<!--more-->

# Why latent class analysis?

Latent class analysis (LCA) is a technique used to identify subgroups, or classes, within a given population. These subgroups are unobserved, or latent, and they are created based on discrete characteristics in hopes of discovering an underlying grouping in data. LCA is commonly used on survey data and in fields such as sociology and epidemiology where separating data into different classes can reveal informative patterns, behaviors, or characteristics that identify those groups. LCA will also return the size of each group which can inform us about the size of each group in the population.

I want to use LCA on university mental health data because I want to explore two things:
1. How many classes provide groups of students with distinct characteristics?
2. Are there specific habits and characteristics that will separate students with depression and
anxiety from those without?

# How does it work?

Now, if you're not a fan of math stuff then feel free to skip ahead a little bit, but I'm going to just give a brief glimpse into how LCA works. In LCA the latent classes are formed based on observed categorical variables, called manifeset variables.

The joint probability of manifest variables \(\textbf{x} = (x_1, x_2, ..., x_p)\) is modeled by a mixture of probabilities across \(K\) latent classes. The probability for individual \(i\) is given in Equation \ref{eq:LCA_general} where \(\eta_j\) is the probability of membership in the \(j^{th}\) class. \(P(\textbf{x}_{ij} \vert \text{Class } k)\) is the probability of observing response \(\textbf{x}_{ij}\) on variable \(i\) for an individual in class $k$ and its product is the joint probability of observing the vector \textbf{$x_i$} given that the individual belongs to class \(k\).

$$P(\textbf{x}_{i}) = \sum_{j=1}^{K}\eta_j \prod_{i=1}^p P(\textbf{x}_{ij} \vert \text{Class } k)$$

In other words, LCA assumes that the observed variables in $x_i$ can be summarized as a weighted sum of conditional response probabilities, where the weights are the class proportions.

# How is this different than other methods?

LCA and traditional clustering methods yield similar results, but clustering methods rely on measures of distance to create groups, or clusters, while LCA is a probabilistic modeling approach. This means that it is possible to use model selection tools with LCA. For examples, using LCA we can compare a 3-class and 4-class model using AIC, among other tools, to decide which number of classes makes the most sense in our data. Model fit metrics like AIC can't be used with a clustering solution. 

LCA also differs from traditional classification analysis in that there are no predetermined groups we are trying to correctly assign to individuals.

# About the mental health data

The data I decided to use is a survey given to university students the inquires about their academic and demographic characteristics as well as their social habits and mental state. The variables I chose to use are: gender, major, academic year, cumulative GPA, average sleep per night in hours, financial concerns (ranked 1 to 5), quality of current social relationships (ranked 1 to 5), depression severity (ranked 1 to 5), and anxiety severity (ranked 1 to 5).

Unfortunately the exact dataset I used is no longer available for download, but a similar one can be found !(here)[https://www.kaggle.com/datasets/sonia22222/students-mental-health-assessments].

# Model Fitting

I fit models for 2, 3, and 4 classes and compared their AIC and $\chi^2$ goodness-of-fit statistics (shown in the table below) to decide which was more appropriate for this data. It appears that the 3-class model has the lowest AIC, but the 4-class model has the best goodness-of-fit. I chose to continue with the 3-class model because when I took a closer look and compared the distribution of manifest variables, the 3-class solution seemed to create groups with more distinct groups. If you're interested, in !(another post)[insert link here] I do through a simulation study to see how well these metrics identify the "correct" number of latent classes.

INSERT TABLE HERE

# Results

# Final thoughts...

By looking at the final model, I discovered that university students can be classified into three distinct subgroups based mostly on their mental health, sleep patterns, financial concerns, and social relationships. It does seem like there are certain characteristics, such as poor sleep and poor social relationships, associated with students who report stronger symptoms of depression and anxiety. 
<!-- The identification of these subgroups provides a deeper understanding of the experiences among students, that can help inform university leadership and resources in supporting their students. -->