---
layout: defaults/page
permalink: index.html
narrow: true
title: Welcome to <em>My Data & I</em>
---

<!-- ## What is it?

{% include components/intro.md %}

[Here's the full feature list and some quick examples of what it can do.]({{ site.baseurl}}{% link _pages/about.md %}) -->

Hi, I’m **Katelyn Miller**—a statistician with a passion for exploring data. With a master's degree in statistics, I’ve dedicated myself to understanding the stories numbers tell. This site is a collection of my projects, projects I have consulted on, and other application I find interesting.

💡 **What you'll find here:**  
- Data modeling & statistical insights   
- Projects that explore real-world data 📈 
- Tips and techniques in Python, R, and more
- My qualifications and interests as a statistician

I’m glad you stopped by! Feel free to explore and reach out if you’d like to connect.


<hr />

### Recent Posts

{% for post in site.posts limit:3 %}
{% include components/post-card.html %}
{% endfor %}


