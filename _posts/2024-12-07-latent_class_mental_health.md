---
title:  "Mental Health in University Students: A Latent Class Introduction and Analysis"
tags:
    - R
    - Unsupervised Learning
---

<!-- <script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script> -->

<!--more-->

## Why latent class analysis?

Latent class analysis (LCA) is a technique used to identify subgroups, or classes, within a given population. These subgroups are unobserved, or latent, and they are created based on discrete characteristics in hopes of discovering an underlying grouping in data. LCA is commonly used on survey data and in fields such as sociology and epidemiology where separating data into different classes can reveal informative patterns, behaviors, or characteristics that identify those groups. LCA also provides the size of each group, offering insight into their prevalence within the population.

I want to use LCA on university mental health data to explore two things:
1. How many classes provide groups of students with distinct characteristics?
2. Are there specific habits and characteristics that differentiate students with depression and anxiety from those without?

## How does it work?

Now, if you're not a fan of math, feel free to skip ahead, but I’ll briefly explain how LCA works. In LCA, latent classes are formed based on observed categorical variables, called manifest variables.

The joint probability of the manifest variables $$\mathbf{x} = (x_1, x_2, \dots, x_p)$$ is modeled by a mixture of probabilities across K latent classes. The probability for individual i is given by:

$$ P(\mathbf{x}_i) = \sum_{j=1}^{K} \eta_j \prod_{i=1}^{p} P(\mathbf{x}_{ij} \mid \text{Class } j) $$

where each η is the probability of membership in the jth class, and $$ P(\mathbf{x}_{ij} \mid \text{Class } k) $$ is the probability of observing the manifest variable i for an individual in class j.

In other words, LCA assumes that the observed variables can be summarized as a weighted sum of conditional response probabilities, where the weights are the class proportions.

## How is this different from other methods?

LCA and traditional clustering methods yield similar results, but clustering methods rely on measures of distance to create groups, while LCA is a probabilistic modeling approach. This means that we can use model selection tools with LCA. For example, we can compare a 3-class and 4-class model using AIC to decide which number of classes fits the data best. Model fit metrics like AIC are not applicable to clustering solutions.

LCA also differs from traditional classification analysis in that there are no predetermined groups to which we are assigning individuals.

## About the mental health data

The data I used comes from a survey of university students that inquires about their academic and demographic characteristics, social habits, and mental health status. The variables included are:
- Gender
- Major
- Academic year
- Cumulative GPA
- Average sleep per night (hours)
- Financial concerns (ranked 1 to 5)
- Quality of social relationships (ranked 1 to 5)
- Depression severity (ranked 1 to 5)
- Anxiety severity (ranked 1 to 5)

Unfortunately, the exact dataset I used is no longer available for download, but a similar one can be found [here](https://www.kaggle.com/datasets/sonia22222/students-mental-health-assessments).

## Model Fitting

I fit models for 2, 3, and 4 classes and compared their AIC and \( \chi^2 \) goodness-of-fit statistics (shown below) to decide which model was most appropriate. The 3-class model had the lowest AIC, while the 4-class model had the best goodness-of-fit. I proceeded with the 3-class model because it yielded more distinct groupings based on manifest variables.

![model comparison metrics](https://raw.githubusercontent.com/katelynnelson38/my-blog/main/theme/img/lca_post/class_size.png)

<!-- | **Model**  | **AIC**  | **Chi-Square Statistic** |
|------------|---------|------------------------|
| 2-Class   | 1977.63 | 146868                 |
| 3-Class   | 1953.11 | 226491                 |
| 4-Class   | 2011.34 | 113801                 | -->

## Results

Conditional Probabilities of Variables for the Three Latent Classes

![conditional probabilities](https://raw.githubusercontent.com/katelynnelson38/my-blog/main/theme/img/lca_post/conditional_probs.png)

<!-- 
| **Variable**              | **Class 1** | **Class 2** | **Class 3** |
|--------------------------|------------|------------|------------|
| **Gender**               |            |            |            |
| Pr(Female)               | 0.4211     | 0.1012     | 0.3073     |
| Pr(Male)                 | 0.5789     | 0.8988     | 0.6927     |
| **Academic Year**        |            |            |            |
| Pr(Year 1)               | 0.2106     | 0.1339     | 0.6062     |
| Pr(Year 2)               | 0.0000     | 0.0665     | 0.3034     |
| Pr(Year 3)               | 0.5262     | 0.7575     | 0.0000     |
| Pr(Year 4)               | 0.2631     | 0.0421     | 0.0904     |
| **CGPA**                 |            |            |            |
| Pr(0.0-1.5)               | 0.0000     | 0.0000     | 0.1130     |
| Pr(1.5-2.0)               | 0.0526     | 0.0000     | 0.0226     |
| Pr(2.0-2.5)               | 0.0000     | 0.0917     | 0.0411     |
| Pr(2.5-3.0)               | 0.2631     | 0.3073     | 0.2193     |
| Pr(3.0-3.5)               | 0.2632     | 0.2259     | 0.3759     |
| Pr(3.5-4.0)               | 0.4210     | 0.3751     | 0.2280     |
| **Average Sleep**        |            |            |            |
| Pr(2-4 hours)               | 0.1052     | 0.0430     | 0.0447     |
| Pr(4-6 hours)               | 0.7367     | 0.5546     | 0.5159     |
| Pr(7-8 hours)               | 0.1580     | 0.4024     | 0.4394     |
| **Financial Concerns**        |            |            |            |
| Pr(1)(Unconcerned)  | 0.0000     | 0.2104     | 0.1808     |
| Pr(2)               | 0.0527     | 0.0432     | 0.1576     |
| Pr(3)               | 0.1579     | 0.2363     | 0.3026     |
| Pr(4)               | 0.2632     | 0.1720     | 0.1788     |
| Pr(5)(Very Concerned)| 0.5262     | 0.3381     | 0.1801     |
| **Social Relationships**        |            |            |            |
| Pr(1)(Dissatisfied) | 0.4736     | 0.1678     | 0.0907     |
| Pr(2)               | 0.0526     | 0.1705     | 0.2023     |
| Pr(3)               | 0.4221     | 0.3639     | 0.3696     |
| Pr(4)               | 0.0526     | 0.2552     | 0.2246     |
| Pr(5)(Satisfied)    | 0.0000     | 0.0425     | 0.1128     |
| **Depression**        |            |            |            |
| Pr(1)(No Depression)| 0.1054     | 0.0000     | 0.2486     |
| Pr(2)               | 0.0000     | 0.2540     | 0.1801     |
| Pr(3)               | 0.0000     | 0.3938     | 0.2632     |
| Pr(4)               | 0.0526     | 0.3522     | 0.2177     |
| Pr(5)(Severe Depression)| 0.8420     | 0.0000     | 0.0904     |
| **Anxiety**        |            |            |            |
| Pr(1)(No Anxiety)   | 0.0527     | 0.0000     | 0.2034     |
| Pr(2)               | 0.0526     | 0.1711     | 0.2924     |
| Pr(3)               | 0.0000     | 0.3857     | 0.2224     |
| Pr(4)               | 0.0000     | 0.4433     | 0.2818     |
| Pr(5)(Severe Anxiety)| 0.8946     | 0.0000     | 0.0000     | -->

### Interpretation of Latent Classes

The conditional probabilities for each variable help interpret the characteristics of each latent class:

- **Class 1**: Characterized by high levels of depression and anxiety, severe financial concerns, and low satisfaction with social relationships. These students tend to have low academic performance and sleep 4-6 hours per night. This class may represent students struggling significantly with mental health.

- **Class 2**: Represents students with moderate levels of depression and anxiety, balanced financial concerns, and moderate social relationship satisfaction. Their academic performance varies, and they tend to have better sleep habits than Class 1.

- **Class 3**: The largest group, consisting of students with moderate to low levels of depression and anxiety, with a high proportion in their first academic year. These students tend to report good sleep habits, moderate financial concerns, and relatively neutral social relationship satisfaction.

The estimated latent class proportions were **21.84%**, **27.31%**, and **50.84%**, respectively. These proportions suggest a greater representation of Class 3, while the other two classes represent more distinct but smaller subgroups.

## Final thoughts...

By analyzing the final model, I discovered that university students can be classified into three distinct subgroups based mostly on mental health, sleep patterns, financial concerns, and social relationships. Certain characteristics, such as poor sleep and weak social relationships, are associated with students reporting stronger symptoms of depression and anxiety.

