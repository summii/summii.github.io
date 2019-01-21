---
layout: post
title: "Machine Learning for Everyone"
date: 2019-01-17
---


## We Understand Simple Words

Machine Learning is like a new drug in a city. Now a days everyone talks about it in the corners and only few able to get it. In my past year, articles about machine learning
 divided into two types: these are either full book of formulas and theorems that i have never able to finish reading even to middle, or magical stories about Artificial
 Intelligence and about google data scientist.

So, I decide to write few post myself, an introduction in my words - in simple language, without formula-theorems, but with examples of real problems and solutions. I will try to write same thing with ugly formula-theorems too in another post.

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

Now Let's decode the fancy terms.

Artificial Intelligence is the name of the whole field, like biology or chemistry.

Machine learning is a section of Artificial Intelligence. Important, but not the only one.

Neural Networks are the type of machine learning. There are others too.

Deep learning is the architecture of neural networks, one of the approach to their construction and training.


In machine learning there are only four main areas

# PART 1 Classical Training

### Teaching with a teacher

They like to divide classical  training into two categories: with teacher - supervised, without teacher - unsupervised. In this first case, the machine has a teacher who tells her how to properly find. Tells that in this picture a cat, and on this a dog. The teacher has already distinguish all the data into cats and dogs and machine can learn from it.

Second case, we will discuss in later part.

Supervised tasls are divided into two types: classification - the prediction of category of the object and regression - the prediction of the place on the number line.

### Classification

"It separates objects according to a previously known attribute. Socks by colors, documnets by language, music by genres"

Today is used to:
* Spam filters
* Language definition
* Search for similar documents
* Tonality analysis
* Recognitionof handwritten letters and numbers
* Suspicious transaction detection

Take an example of a useful classification, Here you apply for a credit card. How can the bank make sure you pay your emi on time or not? Similarly, but bank has thousands of profiles of other people who have already applied for credit card before you. It shows their age, education, position, salary level and importantly, which of them paid their emi's on time and who faced the problems.

Popular algorithms: Naive Bayes , Decision Trees , Logistic Regression , K-Nearest Neighbors , Support Vectors Vectors

### Regression
"Draws a line along my point"

Today is used to:
* Forecast of the value of securities
* Analysis of demand, sales
* Medical diagnosis

Popular algorithms: Linear or Polynomial Regression

Regression is the same as classification, but instead of a category we predict a number. The cost of the car by its mileage, the number if traffic jams by the time of day.

When regression draws a straight line, it is called linear, when the curve is polynomial and logistic regression is not really a regression but a classification method, which is always confusing.

### Teaching without a teacher

In training withour a teacher, the machine just dumps a bunch of photos of animals on the table and say "figure out who here is like someone". The data is not labeled and has no teacher and she tries to find patterns itself.

Unsupervised is more often used us a method of data analysis and not as basic algorithm.


### Clustering

"Splits objects by an unknown attribute. The machine itself decides how best."

Today is used to: 
* Market segmentation(types of customers loyalty)
* Image compression
* Analysis and markup of new data
* Abnormal behaviour detectors

Popular algorithms: K- Mode , Mean-Shift , DBSCAN

Clustering is a classification , but without previously known classes. She herself searches for similar objects and unites then into clusters. An excellent example of clustering can be remembered in iphoto or google photos applications, shich find the faces of people in photos and group them into albums.

It can also be used as an anomaly detector.

### Dimension Reduction (Generalization)

"Collects specific features in a higher level abstraction"

Today is used to: 
* Recommended systems
* Identification and search for similar documents
* Fake image analysis
* Risk management


Popular algorithms: Principal component method (PCA), Singular decomposition (SVD), Dirichlet latent placement (LDA), Latent semantic analysis (LSA, pLSA, GLSA), t-SNE (for visualization)

Intially, these were the methods os hardcore data scientists, who were loaded with trucks of numbers and told to find something interesting. When Excel did not help, they thought to train machines to look for patterns.

For us, the pratical use of their methods is that we can combine several signs into one and get abstraction. For example, dogs with triangular ears, long noses and large tails are joined into useful abstraction of the "shepeerd".

### Search for rules(Association)

"Looking for patterns in the flow of orders"

Today is used to:
* Forecast stock ans sales
* Analysis of goods purchased together
* Placing goods on shelves
* Analysis of patterns of behaviour on websites

Suppose a customer takes a beer in the far corner of a store and goes to the cashier. Should I put nuts on his ways? Do people take thme together?When you own a hypermarket chain, the answer is not always obvious to you but one tactical improvemnet int the placement of inprovement in the placement of goods can make a good profit.


# Part 2 Ensembles

"A bunch of stupid trees learns to correct each others mistakes"

Today is used to:
* In total, where classical algorithm are suitable
* Search Engine
* Computer vision
* Object Recognition

Ways to to ensemble:

**Stacking** We train different algorithms and transfer their results to the input of the latter, which takes the final decision.

**Begging** It is Bootstrap Aggregating. We train one algorithm many times on sample from the source data. At the very end we average the answers.

# Part 3 Neural Networks and deep learning

Here is my last blog on this [Neural Networks](https://summii.github.io/blog/2018/05/05/neural-network-from-scratch)

Today is used to:

* Instead of all the above algorithm in general
* Identification of objects in the photo
* Speech recognition and synthesis
* Image processing, style transfer


Any neaural network is a collection of neurons and connections between them. A neuron is best represented simply as a function with a bunch of inputs and one output. The task of a neuron is to take numbers from its inputs, performs a fucntion on them and give the results to the output. A simple example example of a useful neron, sum up all the digits from the inputs and if their sum is more than N, output a unit, otherwise, zero.

### CNN





