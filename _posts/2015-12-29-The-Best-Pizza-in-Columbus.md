---
layout: post
title: The Best Pizza in Columbus, Ohio
tags: [data-science]
fullview: false
comments: true
---

It's no secret that pizza is one of my favorite things. Pizza is so versatile - its great to have delivered during a Netflix marathon, as a late night snack after the bar, and served cold for breakfast. Although my city of Columbus, Ohio isn't exactly known for its amazing pizza, you can still find amazing pies if you know where to look.

One of my favorite things about my neighborhood is what I believe to be an abundance of superior pizza joints. Maybe even the best in the city. I thought that this question would be perfect for a data analysis, not to mention it would allow me to combine two of my interests: pizza and data visualization! 

The question I decided to try to answer is: 

**What is the best neighborhood for pizza in Columbus?**

Now, before we get rolling on the analysis, it's important to quantify what it means for an area to have the *best* pizza? What is the metric to most adequately measure pizza quality?

As a child of the internet, I personally rely on sites like Yelp and Foursquare when I am looking to try a new restaurant or other establishment. Luckily, Yelp has a nifty [API](https://www.yelp.com/developers/documentation/v2/overview) that is fairly easy to use and allows you to pull data on the location, rating, and other basic info for establishments in a specified area. Although the functionality is fairy limited (for example, you cannot get full review text via the API), it was enough for my purposes and significantly less frustrating than trying to scrape the data from the website.

Now that I had a dataset containing information on all of the pizza joints in Columbus (excluding the rare restaurant not yet on Yelp), my next question was: How can I aggregate and use this data to create a location based pizza rating?

I thought that a sensible solution has to take into account both the number of pizza places nearby and the quality of the pizza. After all, I think that most people would rather have one amazing place to get pizza nearby than 2 or 3 mediocre places. But, how do we measure the quality of each pizza restaurant? We could go with the average star rating by users on Yelp, which ranges from 1 to 5. However, this would treat restaurants with hundreds of reviews the same as restaurants with only one review, which doesn't seem right. It turns out that this is a common problem when dealing with customer ratings, easily solved by using a [Bayesian estimate](http://fulmicoton.com/posts/bayesian_rating/) of the average rating. I won't go into the nitty-gritty details, but the above link is a great resource on how to do this.

 For the location-based rating, I decided to go with a weighted distance score for each point on the map, which I call the "Pizza Density". This score attempts to hit on the idea of the "best" pizza by weighting the distance to each restaurant by the pizza quality in order to favor both restaurants that are close by and restaurants with amazing pizza. If you are interested in learning more about what the pizza density score entails, I have included the R script I used to create the map, linked below on Github.

 To construct the map, I used the R package [ggmap](http://vita.had.co.nz/papers/ggmap.pdf), which interfaces with Google Maps to create awesome map-based data visualizations. This was my first time using ggmap, but I found it very intuitive, especially because you can plot right on top of the map by using the latitude and longitude coordinates in conjunction with [ggplot2](https://cran.r-project.org/web/packages/ggplot2/ggplot2.pdf), which I was already familiar with.

Now, without further ado, here are the results of the investigation:

<br/>
<a href="/assets/images/columbus_pizza_map.png"><img class="regular" src="/assets/images/columbus_pizza_map.png" width="800px" height="800px"/></a>
<br/>

For simplicity in the map coloring, I ended up converting the raw density score into a 1 to 5 rating, where 1 is the worst and 5 is the best. The areas with no coloring were (unfortunately for those that live there) not close enough to any pizza joints to merit inclusion.

The neighborhoods with the best pizza (scoring 4 or 5) are as follows:

#### **Grandview**

The neighborhood of Grandview Heights has the honor of being the best place for pizza in Columbus, outscoring all other locales. Grandview boasts almost 20 pizza restaurants, with Bono Pizza, Dewey's, and Meister's being among the most loved. 

#### **OSU University District and the surrounding areas**

Unsurprisingly, college students love pizza. And their pizza is not only cheap, but evidently amazing as well. After Grandview, the area near High Street comprising the OSU campus from the Short North in the south to Clintonville in the north is the next best place to go to grab a slice. Common campus favorites are Adriatico's, Houndog's, and Tommy's. 

It turns out that while I live fairly close to campus, my neighborhood is not explicitly known for the best pizza. While I had fun answering this question, the results of this analysis will not stop me from trying the pizza all over Columbus (and anywhere else I find myself!)

This project was a great introduction to ggmap, as well as to analyzing web data. In the near future, I hope to explore creating visualizations using more complex web scraping. 

For more information on the construction of the pizza map, check out the R script I've uploaded along with some accompanying info on [Github](https://github.com/emilyrbartha/ColumbusPizzaMap). This script can provide an example of a basic map in ggmap, and can demonstrate how to load a Google map, define the bounds of the map, and plot layers using ggplot2. 

Please don't hesitate to contact me if you have any questions or comments! 