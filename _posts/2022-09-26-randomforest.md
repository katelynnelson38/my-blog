---
title:  "Beginner's Guide to Creating a Random Forest"
tags: 
  - Machine Learning
  - R
---

We're going to use the iris dataset to train a random forest with tidymodels in R.

<!--more-->

Let me just start with a big disclaimer: I am not an expert on machine learning. I am just here to share what I know and maybe it will help someone else. Having said that, I LOVE 😍 the tidymodels packages in R. There can be a lot of different pieces, but I think they come together beautifully and I hope this tutorial helps you understand why.

If you do not already have a basic understanding of random forests, I suggest taking a few minutes to read about them so you understand what our model is doing. [Here](https://careerfoundry.com/en/blog/data-analytics/what-is-random-forest/) is a good website to get you started!

## Let's begin!

Don't forget to load the tidyverse and tidymodels libraries before you begin.

For the sake of simplicity, we will be using the 'iris' dataset that is already built into R. I like to use the function `glimpse()` to take a peek at my data.
```
glimpse(iris)
```
![glimpse](https://raw.githubusercontent.com/katelynnelson38/stat386-projects/main/assets/images/rfpost/glimpse.PNG)

When we run this, we can see that this a fairly simple dataset containing four explanatory variables that we will use to train a model that predicts which of three species that an iris belongs to.

## Prepping the data

Because the dataset is very small (150 rows), we will use bootstrapping to simulate samples that will be used in training and evaluating the random forest. 

(Note: in larger datasets we often use training, testing, and/or validation sets)
```
iris_boot <- bootstraps(iris)
```
One of my favorite parts of using tidymodels is the recipe feature. Recipes allow for quick and easy cleaning of your data before you use it to create a model. In this case the iris data is already very clean, but if the dataset was messy, you can include step functions in the recipe below. A default random forest will generally perform pretty well, but for the sake of demonstration I included two step functions in the iris recipe. Some consider it good practice to normalize the data so that variables have similar centers and spreads. `step_center()` gives the data a mean of 0 and `step_scale()` adjusts the standard deviation to be 1. For more information on recipes and step functions, click [here](https://recipes.tidymodels.org/reference/index.html).

The `prep()` function applies the recipe to the data and the `juice()` function will output the prepped data so you can take a look at what your recipe did.

```
iris_rec <- recipe(Species ~ ., data = iris) %>%
  step_center() %>%
  step_scale()

iris_prep <- prep(iris_rec)
juice(iris_prep)
```

## Creating a random forest model

The best thing to do when creating a random forest model is to give it a lot of trees, we'll use 1000 trees. Set the mode to "classification" because we are predicting a categorical response (use "regression" for continuous response variables). You can also use the "randomForest" engine, but here we will use "ranger". 

(You could also put everything in the `rand_forest()` function, but I like to use piping for clarity)
```
rf_model <- rand_forest(trees = 1000) %>%
  set_mode("classification") %>%
  set_engine("ranger")
```
Once we have prepped our recipe and created a model outline, we can add both to a workflow. Workflows are not crucial to creating a model, but they help organize the process into a clean format that comes in handy when we work with more complicated models.
```
iris_wf <- workflow() %>%
  add_recipe(iris_rec) %>%
  add_model(rf_model)
```
Output your workflow and see what you have so far!
```
iris_wf
```
It should look something like this...

![workflow](https://raw.githubusercontent.com/katelynnelson38/stat386-projects/main/assets/images/rfpost/workflow.PNG)

## Evaluate the model

Now that we've created a random forest model (GREAT job 😏) we want to see how well it performs. `fit_resamples()` will use the workflow and our bootstrapping samples to see how accurate the predictions are compared to the actual iris species.

(This may take a few minutes to run)
```
iris_resamples <- fit_resamples(
  iris_wf,
  resamples = iris_boot,
  control = control_resamples(save_pred = TRUE))
```
Once we've run the code above, we can extract the performance metrics with `collect_metrics()`. A great way to visualize the results of a classification model is a confusion matrix, so we will make one of those, too.
```
iris_resamples %>%
  collect_metrics()

iris_resamples %>%
  collect_predictions() %>%
  conf_mat(Species, .pred_class)
```

![metrics](https://raw.githubusercontent.com/katelynnelson38/stat386-projects/main/assets/images/rfpost/metrics.PNG)

## Variable importance

Just for fun, I'm also going to add code below that will tell you how important each variable is in predicting the iris species.

```
library(vip)

rf_model %>%
  set_engine("ranger", importance = "permutation") %>%
  fit(Species ~ ., data = juice(iris_prep)) %>%
  vip()
```

![variable importance plot](https://raw.githubusercontent.com/katelynnelson38/stat386-projects/main/assets/images/rfpost/var_importance.png)

## Helpful resources

This post was meant to be a brief example of a tidymodels random forest, but I encourage you to try something more complicated next time! I have found a lot of great resources online that helped me a lot when training more complex models. I love Julia Silge's blog and she has a free interactive machine learning course that you can find [here](https://juliasilge.com/blog/tidymodels-ml-course/). The [tidymodels webite](https://www.tidymodels.org/) is also a great resource!
