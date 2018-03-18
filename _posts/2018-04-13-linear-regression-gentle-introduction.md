---
layout: post
title: "Linear Regression - A Gentle Introduction"
date: 2018-04-13
---

In this post I will use python to explore **Linear Regression**. Linear Regressions are form of regression, which means that it is a 
machine learning model that attempts to find a relationship between predictors and a response variable(it should be continous) or 
Linear Regression is a class of techniques for fitting a straight line to a set of data points.
            
![alt text](/img/linear4.jpeg)

* y -> response variable
* xi -> ith variable
* B0 -> intercept
* Bi -> coeff of Xi variable

Lets take a look at some data before we go in-depth.We will to try to predict the number of bike needed on a particular day for a bike 
sharing program.



```python
    # read the data and set the datetime as the index
    # taken from Kaggle: https://www.kaggle.com/c/bike-sharing-demand/data
    import pandas as pd
    import matplotlib.pyplot as plt
    %matplotlib inline
    url =     'https://gist.githubusercontent.com/summii/d6bab7e50cbb691d61354564b0972b69/raw/8d3ec48ac2e2c12fa4b95c8d8aa257c1799e31bc/bikeshare.csv'
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

Now let's actually build our linear regression model with more features and we will take a look at the model's coefficients. Later, we will use Regression metrics to check which of the predictors are useful for us.

```python
# create a list of features
feature_cols = ['temp', 'season', 'weather', 'humidity']
# create X and y
X = bikes[feature_cols]
y = bikes['count']

# instantiate and fit
linreg = LinearRegression()
linreg.fit(X, y)

# pair the feature names with the coefficients
zip(feature_cols, linreg.coef_)
```
 

 
## Regression Metrics
 
 * The mean absolute error
 * The mean squared error
 * The root mean squared error
 
 ![alt text](/img/B05260_10_16.jpg)
 
 RMSE is the most preferred metric for regression but you can choose any one.
 
 using temperature only
 
 ```python
 from sklearn import metrics
# import metrics from scikit learn

feature_cols = ['temp']
# create X and y
X = bikes[feature_cols]
linreg = LinearRegression()
linreg.fit(X, y)
y_pred = linreg.predict(X)
np.sqrt(metrics.mean_squared_error(y, y_pred)) # RMSE
# Can be interpreted loosely as an average error
#166.45
```

Now, let's try it using temperature and humidity.

```python
feature_cols = ['temp', 'humidity']
# create X and y
X = bikes[feature_cols]
linreg = LinearRegression()
linreg.fit(X, y)
y_pred = linreg.predict(X)
np.sqrt(metrics.mean_squared_error(y, y_pred)) # RMSE
# 157.79
```

Better than last one, Now try with more features

```python
feature_cols = ['temp', 'humidity', 'season', 'holiday', 'workingday', 'windspeed', 'atemp']
# create X and y
X = bikes[feature_cols]
linreg = LinearRegression()
linreg.fit(X, y)
y_pred = linreg.predict(X)
np.sqrt(metrics.mean_squared_error(y, y_pred)) # RMSE
# 155.75
```

Much better results now, but we are doing something wrong here. We are training the line to fit **X** and **y** and asking to predict **X**. This thing can lead us to **overfitting**, which means that our model is memorizing the data and giving us back. A great way to approach this problem by using test/train to fit machine learning model.


```python
from sklearn.cross_validation import train_test_split
# function that splits data into training and testing sets


feature_cols = ['temp']
X = bikes[feature_cols]
y = bikes['count']
# setting our overall data X, and y
# Note that in this example, we are attempting to find an association between the temperature of the day and the number of bike rentals.

X_train, X_test, y_train, y_test = train_test_split(X, y) # split the data into training and testing sets
# X_train and y_train will be used to train the model
# X_test and y_test will be used to test the model
# Remember that all four of these variables are just subsets of the overall X and y.

linreg = LinearRegression()
# instantiate the model

linreg.fit(X_train, y_train)
# fit the model to our training set

y_pred = linreg.predict(X_test)
# predict our testing set

np.sqrt(metrics.mean_squared_error(y_test, y_pred)) # RMSE
# Calculate our metric: 166.91
```

### Conclusion
In this blog post I tried to cover Linear Regression by building a model that can predict the number of bike needed on a particular day for a bike sharing program.






