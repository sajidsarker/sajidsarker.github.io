---
layout: post
title: Seattle Airbnb CRISP-DM Project
date: 2022-08-30 02:23:41
tags: [Machine Learning, Data Science]
---
## Seattle Airbnb CRISP-DM Project

[img]

### Motivation

**Airbnb, Inc.**<sup>[[1]](https://en.wikipedia.org/wiki/Airbnb)</sup> is an online marketplace where hosts and guests can organise bookings of temporary lodgings for home-stays. The company itself does not own real estate or hotel properties, but acts as brokers receiving commissions on bookings for maintaining the platform for hosts and guests.

For my project, I utilise data regarding listings of properties by Airbnb hosts in the city of Seattle (WA) between 2016-2017 for exploratory data analysis and regression analysis using the CRISP-DM process. I identify several questions of business interest which I attempt to answer through analysis of the available data.

The Github repository I have created entitled *"Seattle Airbnb CRISP-DM Project"*<sup>[[2]](https://github.com/sajidsarker/seattle-airbnb-crispdm)</sup> contains an HTML knit of the Python Notebook with which I conducted all modelling & analysis.

### CRISP-DM

**Cross Industry Standard Process for Data Mining** is a methodological approach to investigating business questions in a data-driven manner in the field of Data Science. The **CRISP-DM Process** involves the following steps:

1. Business Understanding
2. Data Understanding
3. Data Preparation
4. Modelling
5. Evaluation
6. Deployment

I apply the relevant steps of this process in my approach for this particular Data Science project.

### Business Understanding

On a preliminary review of the data schema, I am interested in finding answers to the following questions:

1. What are the highest rated areas to to reserve accommodations in Seattle?
2. What are the highest revenue generating neighbourhoods in Seattle?
3. Which scores are most important to overall ratings? (Linear Regression)
4. Do hosts with higher ratings overall earn higher revenue? (Linear Regression)
5. What are the most widely provided amenities listed by hosts in Seattle?
6. Which amenities, housing characteristics, and factors contribute positively to revenue? (Linear Regression)
7. Which amenities, housing characteristics, and factors contribute positively to ratings? (Linear Regression)

### Data Understanding

Data is provided courtesy of Airbnb for the city of Seattle, WA during the period of 2016-2017:

- **Listings.csv** contains details of properties and pricing
- **Reviews.csv** contains reviews after home-stays
- **Calendar.csv** contains pricing for listings on specific days

I end up only using the datasets titled **Listings.csv*** and **Reviews.csv**, as **Calendar.csv*** does not contain data pertinent to the context of my questions.

### Data Preparation & Modelling

Given the abundance of quantitative data and the added context of my business questions, much of the modelling I conducted ahead of analysis of my involves **Linear Regression** which is a form of **Generalised Linear Modelling (GLM)**. Aside from this, I use simple descriptive statistical analysis

### Analysis

**1. What are the highest rated areas to to reserve accommodations in Seattle?**

**2. What are the highest revenue generating neighbourhoods in Seattle?**

**3. Which scores are most important to overall ratings? (Linear Regression)**

**4. Do hosts with higher ratings overall earn higher revenue? (Linear Regression)**

**5. What are the most widely provided amenities listed by hosts in Seattle?**

**6. Which amenities, housing characteristics, and factors contribute positively to revenue? (Linear Regression)**

The Top 25 amenities, housing characteristics, and similar factors contributing most greatly in positive association to Airbnb host revenues are depicted in the above bar chart and list.

Revenues are generally positively associated with Airbnb listings with a strict cancellation policy and for hosts with Super Host status. This would imply that verification of hosts in this manner and strong enforcement of scheduling can either ensure higher quality guests, or that well-maintained and valuable properties with experienced hosts tend to attract more guests. It also appears that guest ratings for the Check-In experience is also a factor which is positively associated to revenue.

When considering if a particular listing is of room type 'Entire Home or Apartment' on Airbnb, it is associated strongly with positive contribution to revenue. Listings that are the entire property tend to be more desirable by guests or garner higher prices due to whole units being limited to individual guest demand. No particular neighbourhoods stand out as significant features with positive contributor to revenue, except that for properties listed in the neighbourhoods of West Seattle, Magnolia, Delridge, Rainier Valley, and Seward Park will experience lower revenue.

The nature of the particular housing property listed on Airbnb associated strongly with a positive contribution as a feature that explains revenue includes:

- Chalet
- Tent
- Cabin
- Apartment
- House
- Bed & Breakfast
- Townhouse
- Dormitory
- Bungalow
- Treehouse
- Yurt

Amenities which are valuable in order of descending value in positive association to revenue include:

- Doorman
- Other Pets
- Hot Tub
- Breakfast
- Washer
- Laptop-friendly Workplace
- Pool
- Buzzer / Wireless Intercom
- Washer & Dryer

**7. Which amenities, housing characteristics, and factors contribute positively to ratings? (Linear Regression)**

The Top 25 amenities, housing characteristics, and similar factors contributing most greatly in positive association to Airbnb host ratings are depicted in the above bar chart and list.

Ratings are generally positively associated with Airbnb listings where hosts hold Super Host status and are verified. This would imply that positive recommendation and verification of hosts in this manner attracts and reassures guests that their host can be trusted, is seasoned, and has a reputation for offering a stellar experience. It also appears that prior investigated ratings of value, cleanliness, listing accuracy, host communication, check-in experience, and location all factor positively and significantly as composite measures explaining overall ratings.

Interestingly, dormitory style properties tend to also be well-rated, as do housing with more bathrooms. For the latter characteristic, privacy and accessibility are appreciated by guests, while the former may indicate that guests enjoy shared guest experiences perhaps for socialisation.

Additionally, amenities provided which tend to garner higher ratings are listed as follows:

- Washer & Dryer
- Elevator
- Pets live on property
- Suitable for Events
- Other Pets allowed
- Safety Card
- Kitchen
- Smoker-friendly

Neighbourhoods with positive ratings include Rainier Valley, Central Area, Beacon Hill, Delridge, West Seattle, and Capitol Hill. Interestingly, neighbourhoods previously seen to be associated with lower revenue also tend to be favoured positively in terms of user ratings. This may indicate that such areas offer high value for guests purely for their location while being low revenue generating perhaps due to earning lower prices with frequent to infrequent overall occupancy. It may alternatively also be a combination of being located in a highly desirable urban area but costlier for the guest and therefore infrequently occupied garnering overall lower revenues while still commanding high ratings. The latter alternative would also apply for high revenue generating areas such as Capitol Hill, Central Area, and Rainier Valley which are also highly rated therefore indicating high prices and high occupancy alike.

### Evaluation

### Reference

[[1] Airbnb, Inc. - Wikipedia](https://en.wikipedia.org/wiki/Airbnb)

[[2] Github Repo: Seattle Airbnb CRISP-DM](https://github.com/sajidsarker/seattle-airbnb-crispdm)
