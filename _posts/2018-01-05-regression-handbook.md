---
layout: post
title: "Regression Handbook"
date: 2018-03-13
---



###Linear Regression 

Most basic form of predictive analysis. It is a linear approach to model the relationship between a dependent variable(Y) and a few independent variables(X). 


### Multivariate Linear Regression

Multiple correlated dependent variables are predicted rather than a single scalar variable.


## Optimization

Optimization algorithms are used by machine learning to find a good set of model parameters given a training dataset.

### Cost Fucntion

Cost function tells us how well the neural network is performing. Our goal during training is to find parameters that minimize the cost function. For an example of a cost function, consider Mean Squared Error function:

													MSE=1n∑i=0n(Ŷ i–Yi)2
The mean of square differences between our prediction Ŷ  and desired value Y is what we want to minimize.

### Gradient Descent

Gradient descent is an optimization algorithm used in machine learning to learn values of parameters that minimize the cost function. It’s an iterative algorithm, in every iteration, we compute the gradient of the cost function with respect to each parameter and update the parameters of the function.

### Stochastic Gradient Descent

A technique that evaluates and updates the coefficients every iteration.

How it works:

* Each training instance is shown to the model one at a time.

* Model makes a prediction for a training instance

* Error is calculated and model is updated in order to reduce the error for the next prediction.

b = b-learning rate * error * x

Here,

b = coefficient

learning rate = 0.01

error = prediction error for the model on the training data

x = input value


## Outliers

An outlier is an extreme observation. Typically points further than, say, three or four standard deviations from the mean are considered as “outliers”. Linear Regression models can be heavily impacted by the presence of outliers.

How to fix

Using RANSAC(Random sample consensus), which fits a regression model to a datset of the data, the so-called inliers.

## Evaluation

Residual - The difference or vertical distance between the actual and predicted values

MSE - mean of square differences between our prediction Ŷ  and desired value Y

## Regularization

Regularization is one approach to tackle the problem of overfitting.

Ridge regression is an L2 penalized model where we simply add the squared sum of the weights to our least-square cost fucntion.

Lasso(Least absolute shrinkage and selection operator) - Shrinking the parameter values of the model to induce a penalty against complexity.


## Random Forest Regression 

Random Forest is an ensemble technique that combines multiple decision tree.

* Less sensitive to outliers in the dataset

* Do not require much parameter tuning

* Only parameter in Random forest to experiment with is number of tree.



Reference

2.[sebastian raschka python machine learning](https://www.amazon.in/Python-Machine-Learning-Sebastian-Raschka-ebook/dp/B00YSILNL0)









