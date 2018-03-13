---
layout: post
title: "Linear Regression - A Gentle Introduction"
date: 2018-04-13
---

In this post I will use python to explore **Linear Regression**. Linear Regressions are form of regression, which means that it is a 
machine learning model that attempts to fina a relationship between predictors and a response variable(it should be continous) or 
Linear Regression is a class of techniques for fitting a straight line to a set of data points.

Lets take a look at some data before we go in-depth.We will to try to predict the number of bike needed on a particular day for a bike 
sharing program.

```python
# read the data and set the datetime as the index
# taken from Kaggle: https://www.kaggle.com/c/bike-sharing-demand/data
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline
url = 'https://gist.githubusercontent.com/summii/d6bab7e50cbb691d61354564b0972b69/raw/8d3ec48ac2e2c12fa4b95c8d8aa257c1799e31bc/bikeshare.csv'
bikes = pd.read_csv(url)

bikes.head()
```

![alt text](/img/Screen Shot 2018-03-13 at 8.38.59 PM.png)

We can see that every row represents single hour of bike usuage and we are interested in predicting **count**.

And now let's use the module called **seaborn** to draw a line of best fit.

```python
import seaborn as sns #using seaborn to get a line of best fit
sns.lmplot(x='temp', y='count', data=bikes, aspect=1.5, scatter_kws={'alpha':0.2})
```
![alt text](/img/linear2.png)

To make a prediction, we simply find the temp and see where the line would predict the count. For example, if temperature is 20 degree, then our line would predict that 200 bikes will be needed.


