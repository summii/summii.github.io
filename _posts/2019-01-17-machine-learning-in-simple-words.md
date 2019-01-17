---
layout: post
title: "Machine Learning for Everyone"
date: 2019-01-17
---


## We Understand Simple Words

Machine Learning is like a drug in a city. Now a days everyone talks about it in the corners and only few able to get it. In my past year, articles about machine learning
 divided into two types: these are either full book of formulas and theorems that i have never able to finish reading even to middle, or magical stories about Artificial
 Intelligence and about google data scientist.

So, I decide to write few post myself, an introduction in my words - in simple language, without formula-theorems, but wiht examples of real problems and solutions. I will try to write same thing with ugly formula-theorems too in another post.

### Birth of Machine Learning

Let's analyze with very simple example.

Suppose ravi wants to buy a car and considers how much money he needs to save for this. He reviewed  a dozen ads on the internet and saw that new car cost about Rs. 10lakh ,
one-year-old about Rs. 9lakh , two-year-old about Rs. 8 lakh and so on.

In his mind, Ravi use the formula: the price of a car start at Rs. 10lakh and drops Rs. 1lakh each year, until it reaches Rs 1 lakh.

Ravi did what is callled linear regression in machine learning - he predicted the price from known data. People do it all the time, when they think about to sell an iphone, cycle etc.

Yes, there are dozen more thing to take into account before buying a car but we do not need to think about them to understand machine learning.

People are stupid and lazy - they force machine to work. Let the computer look at your data, find pattern in them and learn how to predict the answer for us.

This is how machine learning was born.


### Three components of learning

The goal of machine learning is to predict the result from input data. The more diverse the input data, the easier it is for the machine to find patterns and the more accurate the result.

So, if we want to train a machine, we need three things.

**Data** We want to define a spam - we need examples of spam letters, to predict the stock price - we need price history, find out the interests if the user - we need his likes or posts.

Data is collected as they can, The most cunning, such as Google, use their own users for free. Remember the ReCaptcha, which sometimes require "to find all the road signs in a photo" - this is it.

![alt text](/img/recaptcha.jpg)

There is a big hunt for good data sets. Large companies can reveal their algorithms, but datasets are extremly rare.

**Attributes** Features, properties, characteristics, signs - they can be the mileage of the car, color of the car, gender of the user. More the information, better results.

**Algorithms** One problem can be solved by various methods approximately always. Accuracy, speed and size of the finished model depend on the choice of algorithm. But there is problem: if the data is shit, even the best algorithm will not help.

