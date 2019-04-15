---
layout: post
title:  3 Tips of Booking NYC Airbnb Homes for Solo Adventurers
---

![nyc_map5](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/nyc_map5.png)

For those who love traveling around the world and exploring new things, New York City should be, without doubt, among the top lines in your to-do list. You will find tons of fun and countless surprises in this famous metropolitan city once you get there.<!-- more -->

A living place is always the first thing to worry about when planing. Luckily we can turn to Airbnb for help. It provides us a large diversity of locations, room types and prices, chances to live with local host and then enjoy local life.

However, too many choices could be a disaster sometimes. So today I will analyze some dataset and try to answer three main questions below about Airbnb in New York.

* What are the differences of Airbnb Homes among boroughs of New York?
* How much time in advance is best to book an Airbnb before going to NYC?
* What are the key features that affects NYC Airbnb prices?

* * *

## 1. Manhattan or Brooklyn?

There are five boroughs in New York: Manhattan, Brooklyn, Queens, Bronx, Staten Island. Overall speaking, Manhattan and Brooklyn have contributed nearly 90% of Airbnb listings in NYC.

<div align=center>![w0](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/w0.png)</div>

While most listings are located in Manhattan and Brooklyn, locations in Midtown and Downtown Manhattan are more expensive than others.(Refer to below Map for details.)

![nyc_price1](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/nyc_price1.png)

Why Manhattan properties more expensive? Let dive deep into details.

![w1](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/w1.png)

* Larger proportion of ‘Entire home/apt’ than other boroughs.
* Less time to reach nearby point of interest. (i.e.: transit stop, subway station)
* Higher chance of getting better amenities like GYM and Pool.

In one word, Manhattan listings are **LUXURY**. At this point, if you want the best quality of living, Manhattan is your first choice.

On the other hand, if you want the best on a budget, Customer Review Rating is a good reference. people often rate perfect score for those beyond their expectations.

|Rank	|neighbourhood_group|neighbourhood|average_rating|
|:----|:----|:----|:----|
|1	|Brooklyn	|Brooklyn Heights	|96.125000|
|2	|Brooklyn	|Boerum Hill	|96.084416|
|3	|Brooklyn	|Prospect Heights	|96.046358|
|4	|Brooklyn	|Cobble Hill	|96.035294|
|5	|Brooklyn	|Windsor Terrace	|95.838462|
|6	|Brooklyn	|Fort Greene	|95.836461|
|7	|Brooklyn	|South Slope	|95.768595|
|8	|Brooklyn	|Bay Ridge	|95.586538|
|9	|Brooklyn	|Greenpoint	|95.367561|
|10 |Brooklyn	|Park Slope	|95.360190|

Surprisingly, top 10 neighborhoods of highest ratings all come from Brooklyn. In this case, Brooklyn areas, like Brooklyn Heights, Boerum Hill, Prospect Heights, could be a better choice for solo adventurers.

* * *

## 2. Book in advance but not too early.

In fact, most Airbnb hosts are private owners, so it is understandable they may not have a fixed plan for far future.

From calendar info recorded on 2019–03–06, we do see obvious drops of available listings count on 90 days and 180 days after, which implies owners’ behavior for updating their properties.

![w3](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/w3.png)

If you are going to New York after more than three months later, do not bother booking an Airbnb too soon because many apartments are not ready for rent.

However, it is also unwise to wait until last minute. If you are on a budget and plan to live outside Manhattan, 1–3 months ahead is a safe period which grant you better chance to get a decent bid.

* * *

## 3. How features affect pricing strategy?

To answer this question, I build a predictive model for price. Refer to below plot to see important features.

![w4](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/w4.png)

* **Room Type**: whether the given property is rent for entire home/apt brings largest difference on price;
* **Location:** properties generally located in Manhattan or Williamsburg,Brooklyn will give positive effects on price, while outlying areas like Harlem and Washington Heights have negative effects on price;
* **Facilities**: properties with more accommodates, bedrooms, bathrooms, with amenities like GYM, TV, Air Conditioning will charge you more;
* **Customer Rating**: while not as much as above 3 factors, relatively low customer rating does give some negative force on price.

To further interpret how different features give positive or negative force on predicting price, I picked one example below:

![w5](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/w5.png)

* Positive force: Entire home/apt, Relatively high accomodates, Good location: Greenpoint Brooklyn, Perfect customer review score on location(10);
* Negative force: Not located in Manhattan, Only one bedrooms, Without TV in the room;

Based on forces from opposite directions, the predicted price comes to $133.75. This give us a guideline when stuck in a trade-off situation.

* * *

## Conclusion

In this article, we looked into real Airbnb dataset and extract three tips for solo adventurers who plans to visit New York City.

1. Go live in Manhattan and enjoy the metropolitan life if your wallet is full, otherwise try Brooklyn which may surprise you.
2. Book in advance but not too early, 1–3 month ahead is a safe period for getting a decent bid.
3. Listing price are mainly affected by room type, location, facilities, and customer ratings. Be clear of your personal preference is a wise move in making a final deal.

* * * 

{{ page.date | date: '%Y-%m-%d' }}: Data Science Blog Post written by Tianxiang Ma. First published on [Medium](https://medium.com/@tma995/3-tips-of-booking-nyc-airbnb-homes-for-solo-adventurers-10782392e12f).

