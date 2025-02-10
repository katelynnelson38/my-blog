---
title:  "Bayesian analysis: Comparing age of COVID-19 realted deaths for men an women"
tags: 
    - R
    - Bayesian Methods
---

<!--more-->

Generally, we know that men die earlier than women, but does this also apply to the recent pandemic and the risk of COVID-19 related death?  Let's find out!

Using data from ... I will do a Bayesian analysis to compare the death of 

What we really want to know is whether or not there is a difference in the average age of death between men and women that died due to COVID-19. To compare these values we will approximate the average ages using Gibbs sampling.

# Set up the problem

Before we start the analysis, what are the unknown parameters that we want to approximate? Well, to compare them, we want to know the average age of death due to COVID-19 in men (&mu;<sub>M</sub>) and in women (&mu;<sub>W</sub>).
<!--and the variance of age of death due to COVID-19 for men and women (&sigma;<sub>M</sub> and &sigma;<sub>W</sub>). -->

We also need to decide what our prior distributions will be. The Normal Distribution is a good model for ages and a quick Google search reveals...

# Methods

We will use a normal distribution to model the data because things in humans and nature are often normally
distributed. Looking at the histograms below, both male and female age of death appear to be approximately
normally distributed.

Likelihood model: xi
|µ, σ2
iid∼ N(µ, σ2
)

We will assign µM and µF with normal prior distributions. This is appropriate because it is unimodal,
symmetric, and sample means tend to have a normal distribution.
We will assign σ
2
M and σ
2
F with inverse gamma prior distributions. This is appropriate because the inverse
gamma distribution is used to model variances.

Prior distributions:
µF ∼ N(λF , τ 2
F )
µM ∼ N(λM, τ 2
M)
σ
2
F ∼ IG(γF , ϕF )
σ
2
M ∼ IG(γM, ϕM)

We chose the prior parameters for µi by looking up the average age of death in men and women in Mexico and choosing values slightly lower to account for the death being caused by COVID-19. We also gave it a generous variance to reflect our uncertainty.

We chose the prior parameters for σ
2
i by picking an expected variance that we considered reasonable and
then choosing parameters to give us that expected variance. We expected the variance in both populations
to be similar, so we gave them the same parameters.
1
0 20 40 60 80
0.00 0.02 0.04
Prior distributions of µi
µM and µF
Density
Male
Female
0 10 20 30 40 50
0.00 0.03
Prior distributions of σi
2
σM
2 and σF
2
Density
Male
Female

We downloaded the data from kaggle, but it originally came from the Mexican government. The mean age
of death was 60.91 years for men and 63.02 years for women. The age of death for men ranged from 18 to
109 years and the range for women was 18 to 119 years. The variances were 201.16 years for men and 208.29
years for women.

# Results

The posterior distributions for females are:
µF |xi
, σ2
F ∼ N(λ
′
F ,(τ
2
F )
′
)
σ
2
F |xi
, µF ∼ IG(γ
′
F , ϕ′
F )

The posterior distributions for males are:
µM|xi
, σ2
M ∼ N(λ
′
M,(τ
2
M)
′
)
σ
2
M|xi
, µM ∼ IG(γ
′
M, ϕ′
M)
2
1.8 2.0 2.2 2.4
0 1 2
3

Posterior of µF − µM
µF − µM
Density
0 5 10 15
0.00 0.10
Posterior of σF
2 − σM
2
σF
2 − σM
2
Density

Looking at the plot above we can see that given our data and prior knowledge, on average, the women who died from COVID-19 were 2.12 years older than the men the men who died from COVID-19 and there is about a 100% probability that of deaths caused by COVID-19 men will die at a younger age than women.
Given the data and prior knowledge, there is 95% probability that the average man who dies from COVID-19
will die 1.91 to 2.33 years younger than the average woman who dies from COVID-19.
Looking at the variance we can see that given our data and prior knowledge, on average, the age of women
who died from COVID-19 has a variance that is 7.1 years bigger than the variance in the age of men who died
from COVID-19 and there is about a 99.88% probability that the variance in average age of death caused
by COVID-19 for women will be larger than the variance in the average age of death for men. Given the
data and prior knowledge, there is 95% probability that the variance in average age of women who die from
COVID-19 is 2.73 to 11.46 years larger than the variance in average age for men who die from COVID-19.

# Conclusions

Our research found that there is a difference in the average age of death between men and women that died
due to COVID-19. As we expected, the age of death for women was higher than the age of death for men.
contrary to what we expected, the variance in age of death for women was higher than it was for men. This
is seen in the plot of the Posterior for µF − µM and the Poster for σ
2
F − σ
2
M.

Before we gathered data, we assumed that both men and women lived to be older than what the data
suggests. But the data did confirm that men do die sooner than women even with COVID-19. The data also
showed that the variances in age of death were different for men and women, which is not what we thought
it would show.

We were limited to COVID-19 data from Mexico, so it would be interesting to gather or find data that could
tell us whether these results are the same that we would find in the United States and/or the rest of the
world. It was also surprising to see that the variances differed so much, so it would be interesting to find
out why.
