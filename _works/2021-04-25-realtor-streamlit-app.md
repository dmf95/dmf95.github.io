---
category: Data Analytics
title: A simple Streamlit app to analyze Vancouver real-estate listings
description: Use Python and the Streamlit library to build an app that describes real-estate listings data in the Greater Vancouver Area.
date: 2021-04-25
image: /images/realtor_app/vancouver.jpg
tags: [all-projects, python, streamlit]
---



## Real-Estate + Vancouver = $

Most Vancouverites don't need to be reminded that Vancouver is an expensive place to live. In a 2021 analysis by [FCT PropTalk](https://proptalk.fct.ca/2021/04/09/most-expensive-canadian-cities-to-live-in-2021-edition/), Vancouver was ranked the 2nd most expensive city to live in Canada, and 7th in North America. 

To prospective home-buyers like myself - good luck! 

![Expensive GIF](https://media0.giphy.com/media/QWd0DkjWZrH3bxW1c9/giphy.gif)

According to the [analysis](https://proptalk.fct.ca/2021/04/09/most-expensive-canadian-cities-to-live-in-2021-edition/), the price to income ratio for Vancouver was 11.41. Said another way, it would take 11.4 years of saving every penny of  your disposable income to afford an average home. 

Renters aren't so lucky either. The median rent per month for a 1-bedroom apartment was $2,013 CAD. Note that these figures more than likely follow a seasonality trend, which was proven so for a [few major cities in the USA in a 2017 analysis](https://medium.com/free-code-camp/how-to-analyze-seasonality-and-trends-to-save-money-on-your-apartment-lease-714d1d82771a) by a fellow data pro.

## Building an app to analyze real-estate listings

As my partner and I started browsing around for 2-bedroom apartments, we kept wondering what "good" looked like. After talking to a few of our friends looking for homes in the GVA, we quickly found out that good real-estate insights were few and far between. 

This was enough to convince my good friend and data wizard [Shannon Lo](https://shannonhlo.github.io/) to collaborate with me on diving deeper into the issue. Using the dark arts of analysis, we decided to build a simple analytics application.

Our application uses Python and the Streamlit library to describe real-estate listings. Simply put, the user can upload their own real-estate listings dataset, and the application will describe it for them. By default, our applications uses a one-time scrape of GVA listings data from [REW](https://www.rew.ca/).

![Simple](/images/realtor_app/simple-very-simple.jpg)

This was our first time working with the Streamlit library, and I must say that I agree with the popular opinion that it is a great resource to deploy data science projects quickly! Being an R guy with some familiarity with building Shiny apps, I was very impressed with how easy it was to implement. 

In a future post, I will be covering the logic of our app. For now, feel free to explore the app and check out the source code available on our [github repo](https://github.com/dmf95/realtor_streamlit_app/blob/main/realtor_streamlit_app.py). 

<iframe src="https://share.streamlit.io/dmf95/realtor_streamlit_app/main/realtor_streamlit_app.py" width="360" height="600">
  <p>Your browser does not support iframes.</p>
</iframe>