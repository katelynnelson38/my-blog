---
title:  "Don't Get Kicked: Predicting Lemons 🍋 in Auto Auctions"
tags: 
  - Machine Learning
  - R
  - Kaggle
  - tidymodels
  - Ensemble Learning
---

<!--more-->  

Kaggle competitions are a great way to test your machine learning skills on real-world data. The [Don't Get Kicked](https://www.kaggle.com/competitions/DontGetKicked) challenge was all about predicting which used cars 🚗 at auction would turn out to be lemons—meaning they had major issues that made them a poor investment.  

In this post, I'll walk through my approach, the models I tested, and what I learned along the way. If you'd like to dive in to my code, check out my [repository on github](https://github.com/katelynnelson38/kaggle_dont_get_kicked).

## Exploring the Data  

The dataset contained information about used cars sold at auctions, including details like the manufacturer, vehicle age, mileage, and pricing estimates. The goal? To predict whether a car was a bad buy (`IsBadBuy = 1`).  

📌A few quick observations from my initial exploration:  

- Some categorical features had *a ton* of levels (like `Model` and `Trim`), which could make modeling tricky.  
- There were missing values, especially in variables like `PRIMEUNIT` and `AUCGUART`.  
- The dataset was imbalanced—only about 12% of the cars were labeled as bad buys.  

<!-- <div class="card mb-3">
    <img class="card-img-top" src="https://github.com/katelynnelson38/my-blog/blob/main/theme/img/dont_get_kicked_post/class_imbalance.jpeg"/>
    <div class="card-body bg-light">
        <div class="card-text">
        </div>
    </div>
</div> -->

<!-- ![imbalance](theme/img/dont_get_kicked_post/class_imbalance.jpeg) -->

![imbalance](https://raw.githubusercontent.com/katelynnelson38/my-blog/main/theme/img/dont_get_kicked_post/class_imbalance.jpeg)

<!-- ![fatalities month](https://raw.githubusercontent.com/katelynnelson38/stat386-projects/main/assets/images/edapost/fatalities_month.png) -->

## Feature Engineering & Preprocessing  

To prep the data for modeling, I used the **tidymodels** framework and built a preprocessing pipeline with these steps:  

- Convert categorical variables into factors.  
- Remove high-cardinality features (`Model`, `Trim`, etc.).  
- Drop highly correlated numeric variables.  
- Impute missing values using median/mode.  
- Apply SMOTE to balance the classes (optional for some models).  

## Trying Different Models  

When submitting your preditions on the test data to kaggle, they are scored by what is called a gini index. A higher score is a better score. I experimented with several classification models to see what worked best. Here's what happened:  

| Model                | Gini Index |
|----------------------|------------|
| XGBoost              | 0.2335     |
| Logistic Regression  | 0.2285     |
| Random Forest        | 0.2254     |
| Naive Bayes          | 0.2177     |
| Decision Tree        | 0.2127     |
| KNN                  | 0.1627     |


After tuning hyperparameters and evaluating on the test set, **XGBoost** came out on top 🏆. It consistently had the highest AUC score and performed well despite the class imbalance.  

## Stacking Models

Model stacking is an **ensemble learning** technique (like bagging and boosting) where multiple models are trained separately, and their predictions are combined using a meta-model (also called a blender). The idea is that different models capture different aspects of the data, and combining them can lead to better overall performance.

How It Works:
1. Train multiple base models (e.g., logistic regression, random forest, XGBoost).
2. Generate predictions from each base model on a validation set.
3. Use these predictions as inputs to train a final meta-model (e.g., a simple linear model or another XGBoost model).
4. The meta-model learns how to best combine the base models' outputs to make a final prediction.

Tidymodels has the capability of combing other models into a stacked model, so I went ahead and [tried a few different stacking combos](https://github.com/katelynnelson38/kaggle_dont_get_kicked/blob/main/CarAuction_stacked.R) with the models I fit above. Unfortunately, none of them performed better than the XGBoost model.

## The End  

Overall, this was a super fun project, and it was a great one to try using model stacking.
