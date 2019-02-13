---
layout: post
title: "Build a Simple Recommendation System"
---
I'm going to show you ways to use the information of a group of people to make recommendations to other people.You have seen recommendation 
system before when using an online shopping site like Amazon and flipkart.These sites track the users information and when you go online
, it uses this information to suggest products you might like.

### The Mathematics behind it

Let's say, a customer X loves comedies, hates romatic movies and is ok with action movies on the scale of 1-5.

X = (5,1,3)

Now, lets assume we have to new movies, one is romantic comedy and the other is funny action movie. They have their own vector of qualities.

m1 = (4,5,1) and m2 = (5,1,5)

Now, we have to make recommendation, we will apply dot product between customer's preferences for each movie.

Lets compute,

X.m1 = (5,1,3).(4,5,1)

(5.4) -> user loves comedy movies and this is movie is funny  +  (1.5) -> user hates romance but this movie is romantic  +   (3.1) -> user ok with action and this movie is not action = 28

The score we got is 28, but what does this number mean? First we will look into best score and worst score we can get.

(5,5,5).(5.5.5) = 75

worst score,
(1,1,1).(1,1,1) = 3

So, we must think about 28 on a scale from 3-75.

Let's try for other movie m2,

(5,1,3).(5,1,5) = (5.5) + (1.1) + (3.5) = 41

This is higher than 28, we will recommend movie2 to user.

### More programmatic approach

First thing you need to do is find a way to represent different people and their preferences.In python , a simple way to do this is to use
nested dictionary.We will create a dictionary of movie critics and their ratings of a small movie dataset.

```python
critics={'Lisa Rose': {'Lady in the Water': 2.5, 'Snakes on a Plane': 3.5,
 'Just My Luck': 3.0, 'Superman Returns': 3.5, 'You, Me and Dupree': 2.5,
 'The Night Listener': 3.0},
'Gene Seymour': {'Lady in the Water': 3.0, 'Snakes on a Plane': 3.5,
 'Just My Luck': 1.5, 'Superman Returns': 5.0, 'The Night Listener': 3.0,
 'You, Me and Dupree': 3.5},
'Michael Phillips': {'Lady in the Water': 2.5, 'Snakes on a Plane': 3.0,
 'Superman Returns': 3.5, 'The Night Listener': 4.0},
'Claudia Puig': {'Snakes on a Plane': 3.5, 'Just My Luck': 3.0,
 'The Night Listener': 4.5, 'Superman Returns': 4.0,
 'You, Me and Dupree': 2.5},
'Mick LaSalle': {'Lady in the Water': 3.0, 'Snakes on a Plane': 4.0,
 'Just My Luck': 2.0, 'Superman Returns': 3.0, 'The Night Listener': 3.0,
 'You, Me and Dupree': 2.0},
'Jack Matthews': {'Lady in the Water': 3.0, 'Snakes on a Plane': 4.0,
 'The Night Listener': 3.0, 'Superman Returns': 5.0, 'You, Me and Dupree': 3.5},
'Toby': {'Snakes on a Plane':4.5,'You, Me and Dupree':1.0,'Superman Returns':4.0}}
```

## Finding Similar Users

We need to determine how similar people are in their tastes.We will do this by comparing each person with every other person and  calculating
similarity score. We will use two methods calculating similarity score: Euclidean Distance and Pearson Correlation.

## Euclidean Distance

This is a very simple way to find the similarity score, which takes the items that people have in common ans uses them as axes for a chart
To calculate the dostance between __ and __ , take  the difference in each axis, square them and add them together, then take the square root of the sum

```python
from math import sqrt
def sim_distance(prefs, per1, per2):
    si = {}
    for item in prefs[per1]:
        if item in prefs[per2]:
            si[item] = 1
    if len(si) == 0: return 0
    sum_of_squares = sum([pow(prefs[per1][item]-prefs[per2][item],2) for item in prefs[per1] if item in prefs[per2]])
    return 1/(1+sum_of_squares)
sim_distance(critics, 'Lisa Rose', 'Toby') #this gives similarity score between Lisa Rose and Toby.
```

>> output: 0.2222222222222222 

This function always return a value between 0 and 1, where 1 means that two people have identical preferences.

## Pearson Correlation Score

Pearson correlation coefficient is a measure of how two set of data fit on a staright line. This formula is more comlicated than Euclidean distance score, but it gives better result in situation where data isn't normalized. 

```python
def sim_pearson(prefs, per1, per2):
    si = {}
    for item in prefs[per1]:
        if item in prefs[per2]:
            si[item] = 1
    n = len(si)
    if n==0: return 0
    sum1 = sum([prefs[per1][it] for it in si])
    sum2 = sum([prefs[per2][it] for it in si])
    
    sum1sq = sum([pow(prefs[per1][it],2) for it in si])
    sum2sq = sum([pow(prefs[per2][it],2) for it in si])
    
    psum = sum([prefs[per1][it]*prefs[per2][it] for it in si])
    num = psum-(sum1*sum2/n)
    den = sqrt((sum1sq-pow(sum1,2)/n)*(sum2sq-pow(sum2,2)/n))
    if den == 0: return 0
    r = num/den
    return r
    
sim_distance(critics, 'Lisa Rose', 'Toby') #this gives similarity score between Lisa Rose and Toby.
```

>> output: 0.9912407071619299

This function will return a value between –1 and 1. A value of 1 means that the two
people have exactly the same ratings for every item.
    


