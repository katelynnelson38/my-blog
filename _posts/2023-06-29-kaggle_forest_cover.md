---
title: "Predicting Forest 🌳 Cover Type: A Multiclass Problem"
tags: 
  - Machine Learning
  - R
  - Kaggle
  - tidymodels
  - Multiclass Classification
---

<!--more-->  

Hello! Today, I’m diving into a Kaggle competition called [Forest Cover Type Prediction](https://www.kaggle.com/competitions/forest-cover-type-prediction). If you're interested in seeing any of my code check out my [repository](https://github.com/katelynnelson38/kaggle_forest_cover).

### What's the Goal?  
The task is to classify forest cover types based on cartographic features like elevation, soil type, and wilderness area. Basically, given some environmental data, we need to predict which type of forest cover exists in that location.  

The dataset comes from the Roosevelt National Forest in Colorado and contains seven forest cover types, ranging from spruce/fir to aspen and lodgepole pine. Since there are more than two possible categories, this is a **multiclass classification problem**—a common challenge in machine learning where the goal is to assign one label out of many possible options.  

Some other real-world applications of multiclass classification include:  
✅ Handwriting recognition (identifying letters or digits)
✅ Medical diagnosis (predicting diseases based on symptoms) 
✅ Image classification (sorting images into categories) 

With that in mind, let’s jump right in!  

### 🛠️ Prepping the Data  
Before training models, I explored the dataset to understand the distribution of cover types. A quick `ggplot` visualization revealed some imbalances—certain cover types are way more common than others. That’s something to keep in mind when evaluating model performance!  

I then split the data into training and test sets and created a **recipe** using `tidymodels`, applying transformations like normalization and feature engineering.  

### 🚀 Trying Out Different Models  

I tested a variety of classification models to see which one worked best:  

| **Model**                | **Best Accuracy** 📈 |
|--------------------------|----------------------|
| Logistic Regression      | 0.595  |
| Naïve Bayes             | 0.577  |
| k-Nearest Neighbors     | 0.666  |
| Decision Tree           | 0.626  |
| **Random Forest** 🌟     | **0.747**  |
| XGBoost                 | 0.610  |
| Neural Network (Single Layer) | 0.027 😬  |
| SVM                     | 0.528  |
| **Stacked Model (LR, NB, RF, XGB)** 🔥 | **0.761** 🎉 |

🔹 **Random Forest** performed really well, scoring **0.747**, but my best result came from **stacking multiple models** (Random Forest, Naïve Bayes, Logistic Regression, and XGBoost), reaching **0.761**!  

🔹 The **neural network (single layer)** was a total flop at **0.027**—which means it was basically guessing. Clearly, deep learning isn't the best fit for this problem without heavy tuning.  

---

### 💡 Key Takeaways  

1️⃣ **Random Forest is a strong baseline** for structured data like this—no surprise there! 🌲  
2️⃣ **Stacking models** can boost performance by leveraging the strengths of multiple algorithms.  
3️⃣ **Some models, like simple neural networks, aren’t always the best choice** without deeper tuning.  

---

### 📢 What’s Next?  

I might try tweaking hyperparameters more, adding feature selection, or experimenting with deep learning architectures to see if I can squeeze out more accuracy. Any ideas? Let me know what you'd try! 🚀  

Check out the competition [here](https://www.kaggle.com/competitions/forest-cover-type-prediction) if you want to join in!  

---

This version keeps it fun and engaging while still being informative. Let me know if you'd like any refinements! 😊

