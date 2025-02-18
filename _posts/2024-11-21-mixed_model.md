---
title:  "Sone Mixed model"
tags:
    - R
    - Mixed-effects Model
    - Kaggle
    - Tutorial
---

<!--more-->

Something I use *all the time* when working with consulting clients is a mixed-effects model. It is so useful, but I didn't even learn what it was or how to use it until I was in my Master's program. 

In this post I am going to go through an analysis as a tutorial/demonstration of how to use a mixed-effects model and why it is useful. So, let's begin! 🎉😤

## What is a "mixed-effects" model?

Mixed-effects models are very useful when a fixed and random effect are present. What does that mean?
- A **fixed effect** is one that has a consistent relationship with the response, or "fixed" effect on the population in question.
- A **random effect** is one that introduces variability in the data, but we are not interested in knowing how it affects a response or population. In randomized experiments we treat blocks or groups as random effects.

If this doesn't make sense yet, don't freak out! It will all become clearer when we get into the data analysis.

## Bell's Palsy Clinical Trial Data

Bell's palsy is a medical condition in 
facial nerves that causes weakness or paralysis on one side of the face. This can be manifest in various symptoms such as, a drooping of facial features, pain in the jaw, etc. The condition can be temporary or permanent.

[This kaggle dataset](https://www.kaggle.com/datasets/dillonmyrick/bells-palsy-clinical-trial) contains data from a double-blind clinical trial assessing the effectiveness of different drugs on patient facial recovery. Facial recovery is measured on the House–Brackmann scale. See the [kaggle page](https://www.kaggle.com/datasets/dillonmyrick/bells-palsy-clinical-trial) for more details.

How does this apply to the mixed-model framework?
- The response variable will be 


