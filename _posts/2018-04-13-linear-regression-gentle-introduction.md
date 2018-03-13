---
layout: post
title: "Linear Regression - A Gentle Introduction"
date: 2018-04-13
---

In this post I will use python to explore **Linear Regression**. Linear Regressions are form of regression, which means that it is a 
machine learning model that attempts to find a relationship between predictors and a response variable(it should be continous) or 
Linear Regression is a class of techniques for fitting a straight line to a set of data points.
            
![alt text](/img/linear4.png)

* y -> response variable
* xi -> ith variable
* B0 -> intercept
* Bi -> coeff of Xith variable

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

![alt text](/img/linear0.png)

We can see that every row represents single hour of bike usuage and we are interested in predicting **count**.

And now let's use the module called **seaborn** to draw a line of best fit.

```python
import seaborn as sns #using seaborn to get a line of best fit
sns.lmplot(x='temp', y='count', data=bikes, aspect=1.5, scatter_kws={'alpha':0.2})
```
![alt text](/img/linear2.png)

To make a prediction, we simply find the temp and see where the line would predict the count. For example, if temperature is 20 degree, then our line would predict that 200 bikes will be needed. Now, we can see that if temperature goes up, count also goes up. Let's check the correlation value.

```python
bikes[['count', 'temp']].corr()
# 0.3944
```

Let's build the model in python,

```python
# create X and y
feature_cols = ['temp'] # a lsit of the predictors
X = bikes[feature_cols] # subsetting our data to only the predictors
y = bikes['count'] # our response variable
```
Now, we will import machine learning module,

```python
# import scikit-learn, our machine learning module
from sklearn.linear_model import LinearRegression
```

Finally, we will do fitting and print the *coefficient*

```python
linreg = LinearRegression() #instantiate a new model
linreg.fit(X, y) #fit the model to our data

# print the coefficients
print linreg.coef_
[ 9.17054048]     # our beta parameters
```

It represents how x and y move together. A change in 1 degree will result in increase of about 9 nikes rented.

Using *scikit-learn* to make prediction.

```python
linreg.predict(20)
# 189.4570
```

This means that 190 bikes will likely be rented if the temperature is 20 degrees.






