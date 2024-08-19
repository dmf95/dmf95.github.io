---
category: Python Basics
title: Multi-page scraping Amazon reviews in Python using requests, BeautifulSoup, and Splash
description: Learn how to build a multi-page python web-scraper for product reviews data
date: 2021-05-23
image: /images/amazon-web-scraper/amazon.jpg
tags: [all-projects, python, tutorial, web-scraping]
---

## Multi-page web-scraping

In this post, I'm going to show you how to build a multi-page web-scraper in Python. 

We will be scraping Amazon product reviews data, but the focus will be on looping through multiple pages. 

If you're looking for a basic introduction to web-scraping in Python, check out the [single page Python web-scraper for Amazon product reviews data]((2021-05-12-scraping-amazon-python.md)) from my last post.

Didn't read that post? All good, here is the  TL;DR (too long; didn't read) version:
* Scraped Amazon product reviews data for some Sony Headphones I recently bought
* Introduction to using Splash and Docker for web-scraping
* Step-by-step implementation of popular web-scraping Python libraries: BeautifulSoup, requests, and Splash.

## Getting started
Here's a snippet of code that we can start with:

{% highlight py %}
#-----------------------------------------
# Single-page python web-scraper for Amazon product reviews
#-----------------------------------------

# Import libraries
import requests
from bs4 import BeautifulSoup
import pandas as pd

# URL setup and HTML request
# Note - run Option 2 if you haven't setup Docker & Splash
url = 'https://www.amazon.ca/Sony-WF-1000XM3-Industry-Canceling-Wireless/product-reviews/B07T81554H/ref=cm_cr_dp_d_show_all_btm?ie=UTF8&reviewerType=all_reviews'
# Option 1
r = requests.get('http://localhost:8050/render.html', params = {'url': url, 'wait' : 2})
# Option 2
# r = requests.get(url)

# Parsing the HTML content
soup = BeautifulSoup(r.text, 'html.parser')

# Getting desired data from our parsed soup
reviews = soup.find_all('div', {'data-hook': 'review'})

# Initialize list
data = []

# For every item in review, scrape the following and store as a list called review
for item in reviews:
    review = {
    'product': soup.title.text.replace('Amazon.ca:Customer reviews: ', '').strip(), 
    'title': item.find('a', {'data-hook': 'review-title'}).text.strip(),
    'date': item.find('span', {'data-hook': 'review-date'}).text.strip(),
    'rating': float(item.find('i', {'data-hook': 'review-star-rating'}).text.replace('out of 5 stars', '').strip()),
    'text': item.find('span', {'data-hook': 'review-body'}).text.strip(),
    }
    data.append(review)  

# Save results to a dataframe, then export as CSV
df = pd.DataFrame(data)
df.to_csv(r'sony-headphones.csv', index=False)

{% endhighlight %}

Running this will fetch us the ```product```, ```title```, ```date```, ```rating```, and the actual ```text``` for each review made on Amazon for [these Sony Headphones](https://www.amazon.ca/Sony-WF-1000XM3-Industry-Canceling-Wireless/product-reviews/B07T81554H/ref=cm_cr_dp_d_show_all_btm?ie=UTF8&reviewerType=all_reviews).

## Code refactoring

Before we mess around with the code to loop through multiple pages, its a good practice to refactor a little. We will introduce few functions to help with performance and readability.

Let's start with converting our URL setup & HTML request to a function.

{% highlight py %}
# Function 1: get and return parsed HTML
def get_soup(url):
    r = requests.get('http://localhost:8050/render.html', 
    # Run this instead if you haven't setup Splash & Docker
    # r = requests.get(url)
    params={'url': url, 'wait': 2})
    soup = BeautifulSoup(r.text, 'html.parser')
    return soup

{% endhighlight %}

This function takes in URL as an input, and spits out an HTML-parsed version of the HTTP request we made. Let's call this our ```soup```.

Next, we need to tell Python what data we want to look for in the ```soup```.

{% highlight py %}
# Initialize list to store reviews data later on
reviewlist = []

# Function 2: look for web-tags in our soup, then append our data to reviewList
def get_reviews(soup):
    reviews = soup.find_all('div', {'data-hook': 'review'})
    try:
        for item in reviews:
            review = {
            'product': soup.title.text.replace('Amazon.ca:Customer reviews: ', '').strip(), 
            'date': item.find('span', {'data-hook': 'review-date'}).text.strip(),
            'title': item.find('a', {'data-hook': 'review-title'}).text.strip(),
            'rating':  float(item.find('i', {'data-hook': 'review-star-rating'}).text.replace('out of 5 stars', '').strip()),
            'body': item.find('span', {'data-hook': 'review-body'}).text.strip(),
            }
            reviewlist.append(review)
    except:
        pass

{% endhighlight %}

Here, we ```try``` to scrape for those reviews in our ```soup``` that are tagged in the way we've specified, then append to our list. 

If for whatever reason we cannot find what we are looking for, then we are asking Python to ```pass``` to the next review.

## Looping through multiple pages

One of the easiest methods to scrape multiple pages is to modify the base URL to accept a page variable that increments as needed.

Try for yourself! See how the URL changes as you go through multiple pages. 

For Amazon product reviews, the only thing that seems to change is the number indicating which page it is. 

{% highlight py %}
# Method: loop through a range of values, where x = a sequenced page number
f'https://www.amazon.ca/Sony-WF-1000XM3-Industry-Canceling-Wireless/product-reviews/B07T81554H/ref=cm_cr_dp_d_show_all_btm?ie=UTF8&reviewerType=all_reviews&pageNumber={x}'

{% endhighlight %}

Okay, now let's put this to work in a function:

{% highlight py %}
# Function 3: loop through 1:x many pages, or until the css selector found only on the last page is found (when the next page button is greyed)
for x in range(1,20):
    soup = get_soup(f'https://www.amazon.ca/Sony-WF-1000XM3-Industry-Canceling-Wireless/product-reviews/B07T81554H/ref=cm_cr_dp_d_show_all_btm?ie=UTF8&reviewerType=all_reviews&pageNumber={x}')
    print(f'Getting page: {x}')
    get_reviews(soup)
    print(len(reviewlist))

{% endhighlight %}

We can even add in a a stop condition. For this one, we can tell Python to look for a greyed out "Next Page" button. To identify this element, use the element inspector.

Add this to the bottom of the function above.

{% highlight py %}

# Continue to loop through range so long as greyed out button isn't detected
if not soup.find('li', {'class': 'a-disabled a-last'}):
        pass
    else:
        break

{% endhighlight %}

## Putting it all together

You can find the put-together code here in my [amazon web scraping github repo](https://github.com/dmf95/scrape-amazon-reviews). Look for the file called ```2_amz_review_scraper.py```.

You'll notice that I used Splash & Docker to render and return the page. I found that I needed it to run my code.

Incase you want to try running the scraper without Splash & Docker, simply change ```Line 9``` to the following:

{% highlight py %}

r = requests.get(url)

{% endhighlight %}

## Conclusion

To review, here is what we just did:
* Modularized and refactored our single-page amazon product reviews web-scraper
* Added a for loop that returns Amazon product reviews for the range we specified 
* Added a stop condition that looks for a greyed-out "Next Page" button
* Added printed comments to help us follow the code as it scrapes
* Returned a CSV file with the data we specified called ```sony-headphones.csv```

Once again, credit to [John Watson Rooney](https://www.youtube.com/channel/UC8tgRQ7DOzAbn9L7zDL8mLg) who provided the [methodology in github](https://github.com/jhnwr/scrape-amazon-reviews) from which this tutorial is adapted from.  I would encourage you to check out his content if web-scraping in Python interests you.

There will be one last post on this topic, this time taking the data that we've got and running a basic sentiment analysis in Python.



