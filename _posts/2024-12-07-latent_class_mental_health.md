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

## Why latent class analysis?

Latent class analysis (LCA) is a technique used to identify subgroups, or classes, within a given population. These subgroups are unobserved, or latent, and they are created based on discrete characteristics in hopes of discovering an underlying grouping in data. LCA is commonly used on survey data and in fields such as sociology and epidemiology where separating data into different classes can reveal informative patterns, behaviors, or characteristics that identify those groups. LCA will also return the size of each group which can inform us about the size of each group in the population.

I want to use LCA on university mental health data because I want to explore two things:
1. How many classes provide groups of students with distinct characteristics?
2. Are there specific habits and characteristics that will separate students with depression and
anxiety from those without?

## How does it work?

Now, if you're not a fan of math stuff then feel free to skip ahead a little bit, but I'm going to just give a brief glimpse into how LCA works. In LCA the latent classes are formed based on observed categorical variables, called manifeset variables.

The joint probability of manifest variables \(\textbf{x} = (x_1, x_2, ..., x_p)\) is modeled by a mixture of probabilities across \(K\) latent classes. The probability for individual \(i\) is given in the equation below where \(\eta_j\) is the probability of membership in the \(j^{th}\) class. \(P(\textbf{x}_{ij} \vert \text{Class } k)\) is the probability of observing response \(\textbf{x}_{ij}\) on variable \(i\) for an individual in class $k$ and its product is the joint probability of observing the vector \textbf{$x_i$} given that the individual belongs to class \(k\).

The joint probability of manifest variables (**x** = \( (x_1, x_2, \dots, x_p) \)) is modeled by a mixture of probabilities across \( K \) latent classes. The probability for individual \( i \) is given in the equation below, where \( \eta_j \) is the probability of membership in the \( j^{th} \) class. \( P(\mathbf{x}_{ij} \mid \text{Class } k) \) is the probability of observing response \( \mathbf{x}_{ij} \) on variable \( i \) for an individual in class \( k \), and its product is the joint probability of observing the vector \( \mathbf{x}_i \) given that the individual belongs to class \( k \).

$$P(\textbf{x}_{i}) = \sum_{j=1}^{K}\eta_j \prod_{i=1}^p P(\textbf{x}_{ij} \vert \text{Class } k)$$

In other words, LCA assumes that the observed variables in $x_i$ can be summarized as a weighted sum of conditional response probabilities, where the weights are the class proportions.

## How is this different than other methods?

LCA and traditional clustering methods yield similar results, but clustering methods rely on measures of distance to create groups, or clusters, while LCA is a probabilistic modeling approach. This means that it is possible to use model selection tools with LCA. For examples, using LCA we can compare a 3-class and 4-class model using AIC, among other tools, to decide which number of classes makes the most sense in our data. Model fit metrics like AIC can't be used with a clustering solution. 

LCA also differs from traditional classification analysis in that there are no predetermined groups we are trying to correctly assign to individuals.

## About the mental health data

The data I decided to use is a survey given to university students the inquires about their academic and demographic characteristics as well as their social habits and mental state. The variables I chose to use are: gender, major, academic year, cumulative GPA, average sleep per night in hours, financial concerns (ranked 1 to 5), quality of current social relationships (ranked 1 to 5), depression severity (ranked 1 to 5), and anxiety severity (ranked 1 to 5).

Unfortunately the exact dataset I used is no longer available for download, but a similar one can be found !(here)[https://www.kaggle.com/datasets/sonia22222/students-mental-health-assessments].

## Model Fitting

I fit models for 2, 3, and 4 classes and compared their AIC and $\chi^2$ goodness-of-fit statistics (shown in the table below) to decide which was more appropriate for this data. It appears that the 3-class model has the lowest AIC, but the 4-class model has the best goodness-of-fit. I chose to continue with the 3-class model because when I took a closer look and compared the distribution of manifest variables, the 3-class solution seemed to create groups with more distinct groups. If you're interested, in !(another post)[insert link here] I do through a simulation study to see how well these metrics identify the "correct" number of latent classes.

| **Model**  | **AIC**  | **Chi-Square Statistic** |
|------------|---------|------------------------|
| 2-Class   | 1977.63 | 146868                 |
| 3-Class   | 1953.11 | 226491                 |
| 4-Class   | 2011.34 | 113801                 |

## Results

## Conditional Probabilities of Variables for the Three Latent Classes

The table below presents the conditional probabilities of each variable for the three latent classes.

\[
\begin{array}{|l|c|c|c|}
\hline
\textbf{Variable} & \textbf{Class 1} & \textbf{Class 2} & \textbf{Class 3} \\
\hline
\textbf{Gender} & & & \\
\text{Pr(Female)} & 0.4211 & 0.1012 & 0.3073 \\
\text{Pr(Male)} & 0.5789 & 0.8988 & 0.6927 \\
\hline
\textbf{Academic Year} & & & \\
\text{Pr(Year 1)} & 0.2106 & 0.1339 & 0.6062 \\
\text{Pr(Year 2)} & 0.0000 & 0.0665 & 0.3034 \\
\text{Pr(Year 3)} & 0.5262 & 0.7575 & 0.0000 \\
\text{Pr(Year 4)} & 0.2631 & 0.0421 & 0.0904 \\
\hline
\textbf{CGPA} & & & \\
\text{Pr(0.0-1.5)} & 0.0000 & 0.0000 & 0.1130 \\
\text{Pr(1.5-2.0)} & 0.0526 & 0.0000 & 0.0226 \\
\text{Pr(2.0-2.5)} & 0.0000 & 0.0917 & 0.0411 \\
\text{Pr(2.5-3.0)} & 0.2631 & 0.3073 & 0.2193 \\
\text{Pr(3.0-3.5)} & 0.2632 & 0.2259 & 0.3759 \\
\text{Pr(3.5-4.0)} & 0.4210 & 0.3751 & 0.2280 \\
\hline
\textbf{Average Sleep} & & & \\
\text{Pr(2-4 hours)} & 0.1052 & 0.0430 & 0.0447 \\
\text{Pr(4-6 hours)} & 0.7367 & 0.5546 & 0.5159 \\
\text{Pr(7-8 hours)} & 0.1580 & 0.4024 & 0.4394 \\
\hline
\textbf{Financial Concerns} & & & \\
\text{Pr(1) (Unconcerned)} & 0.0000 & 0.2104 & 0.1808 \\
\text{Pr(2)} & 0.0527 & 0.0432 & 0.1576 \\
\text{Pr(3)} & 0.1579 & 0.2363 & 0.3026 \\
\text{Pr(4)} & 0.2632 & 0.1720 & 0.1788 \\
\text{Pr(5) (Very Concerned)} & 0.5262 & 0.3381 & 0.1801 \\
\hline
\textbf{Social Relationships} & & & \\
\text{Pr(1) (Very Dissatisfied)} & 0.4736 & 0.1678 & 0.0907 \\
\text{Pr(2)} & 0.0526 & 0.1705 & 0.2023 \\
\text{Pr(3)} & 0.4211 & 0.3639 & 0.3696 \\
\text{Pr(4)} & 0.0526 & 0.2552 & 0.2246 \\
\text{Pr(5) (Very Satisfied)} & 0.0000 & 0.0425 & 0.1128 \\
\hline
\textbf{Depression} & & & \\
\text{Pr(1) (No Depression)} & 0.1054 & 0.0000 & 0.2486 \\
\text{Pr(2)} & 0.0000 & 0.2540 & 0.1801 \\
\text{Pr(3)} & 0.0000 & 0.3938 & 0.2632 \\
\text{Pr(4)} & 0.0526 & 0.3522 & 0.2177 \\
\text{Pr(5) (Severe Depression)} & 0.8420 & 0.0000 & 0.0904 \\
\hline
\textbf{Anxiety} & & & \\
\text{Pr(1) (No Anxiety)} & 0.0527 & 0.0000 & 0.2034 \\
\text{Pr(2)} & 0.0526 & 0.1711 & 0.2924 \\
\text{Pr(3)} & 0.0000 & 0.3857 & 0.2224 \\
\text{Pr(4)} & 0.0000 & 0.4433 & 0.2818 \\
\text{Pr(5) (Severe Anxiety)} & 0.8946 & 0.0000 & 0.0000 \\
\hline
\end{array}
\]

### Interpretation of Latent Classes

The conditional probabilities for each variable help interpret the characteristics of each latent class.  

- **Class 1**: Characterized by high levels of depression and anxiety, severe financial concerns, and low satisfaction with social relationships. These students tend to have low academic performance (CGPA) and report sleeping 4-6 hours. This class may represent students struggling significantly with mental health and related stressors.  

- **Class 2**: Represents students with moderate levels of depression and anxiety, balanced financial concerns, and moderate social relationship satisfaction. Their academic performance is more varied, and they tend to have better sleep habits than Class 1. This class could represent students facing some challenges but not at the extremes seen in Class 1.  

- **Class 3**: The largest group, consisting of students with moderate to low levels of depression and anxiety, with a high proportion in their first academic year. These students tend to report good sleep habits, moderate financial concerns, and relatively neutral social relationship satisfaction. This class could represent a healthier subgroup of students experiencing fewer mental health challenges.  

The estimated latent class proportions for the three classes were **21.84%**, **27.31%**, and **50.84%**, respectively. These proportions suggest a greater representation of Class 3, while the other two classes represent more distinct but smaller subgroups.


## Final thoughts...

By looking at the final model, I discovered that university students can be classified into three distinct subgroups based mostly on their mental health, sleep patterns, financial concerns, and social relationships. It does seem like there are certain characteristics, such as poor sleep and poor social relationships, associated with students who report stronger symptoms of depression and anxiety. 
<!-- The identification of these subgroups provides a deeper understanding of the experiences among students, that can help inform university leadership and resources in supporting their students. -->