---
layout: post
title:  "Landslides: Where do they happen? What causes them?"
date:   2022-11-29
author: Katelyn Nelson
description: Use an interactive plotly figure to learn about common triggers and locations of landslides
image: /assets/images/datastory-post/photo-rain-jungle.jpeg
---

# Quick recap

I came across this landslide dataset on NASA's Open Data Portal and thought it would be interesting to see what I could learn. ⚠️ Be warned: I am not an expert in landslides or any other environmental phenomenon, but I thought this would be a fun dataset to explore. To access the data I used a personal API key (requested on the data portal website) and pulled the data into a Jupyter Notebook file. It turned out to be a pretty big and messy dataset, so I did some data wrangling and chose which fields I wanted to focus on. If you want to see the steps I took check out my other [blog post](https://katelynnelson38.github.io/stat386-projects/2022/10/16/nasa_api.html) and my [github repository](https://github.com/katelynnelson38/nasa_api).

Once the data was nice and tidy, I could begin to explore it. So after brainstorming ⛈️ some questions, I investigated their possible answers through plots that I included as part of my [exploratory data analysis](https://katelynnelson38.github.io/stat386-projects/2022/11/14/EDA.html). This gave me insights about common causes of landslides, occurances of landslides across time, which countries have more fatal landslides, and more. This post focuses on landslide locations and triggers.

# Where and why

When I first found this data, I was most curious about the common causes of landslides and where landslides occur most frequently. Is there a connection with the location and the trigger? Will this information help us to prevent landslides or be more prepared to handle them?

I created a graph of the 10 countries that have the most landslides to help me discover the story about causes and locations of landslides. One cool feature is that you can change which landslide triggers are included in the plot by using the legend on the right. 

**Note:** Clicking on one of the landslide triggers will add or remove it from the plot. Double-clicking a specific landslide trigger will remove all other triggers from the plot and can be reset by double-clicking the same trigger.

{% include country_landslides.html %}

Looking at the graph above we can see that Brazil and Indonesia have the most landslides than any other country included in the data AND that most of their landslides were triggered by some form of rain. I looked into it, and these two countries both receive above average amounts of rain. Futhermore, we can look at the size of each trigger represented in the graph and see that different intensities of rain are the primary cause of landslides in all of these countries. From this we can infer that rainy countries have more landslides, and Brazil and Indonesia both receive a lot of rain (coincidence? I think not 😉).

Removing the top four triggers (downpour, rain, continuous rain, and unknown), we can see that besides rain-related triggers, the most common ones are earthquakes, tropical cyclones, and flooding. This tells us that most landslides are caused by weather-related events.

# Moral of the story

Using the plot above, we learned that rainy countries, namely Brazil and Indonesia, have more landslides because rain is the primary trigger of a landslide. Looking more closely, we also saw that the next most common triggers were weather-related as well, meaning there is not much we can do to prevent landslides. However, being aware of which places are more prone to landslides and what causes them can help us to prepare for them.

If you want to see how I created the plot, take a look at my [github repository](https://github.com/katelynnelson38/nasa_api).
