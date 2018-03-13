---
layout: post
title: "Linear Regression - A Gentle Introduction"
date: 2018-04-13
---

In this post I will use python to explore **Linear Regression**. Linear Regression are form of regressions, which means that it is a 
machine learning model that attempts to fina a relationship between predictors and a response variable(it should be continous) or 
Linear Regression is a class of techniques for fitting a straight line to a set of data points.

Lets take a look at some data before we go in-depth.We will to try to predict the number of bike needed on a particular day for a bike 
sharing program.

`
# read the data and set the datetime as the index
# taken from Kaggle: https://www.kaggle.com/c/bike-sharing-demand/data
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline
url = 'https://gist.githubusercontent.com/summii/d6bab7e50cbb691d61354564b0972b69/raw/8d3ec48ac2e2c12fa4b95c8d8aa257c1799e31bc/bikeshare.csv'
bikes = pd.read_csv(url)

bikes.head()
`

[Link Text](https://github.com/summii/summii.github.io/blob/master/img/Screen%20Shot%202018-03-13%20at%208.38.59%20PM.png)
