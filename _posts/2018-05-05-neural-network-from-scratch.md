---
layout: post
title: "Neural Network From Scratch"
date: 2018-05-05
---
![alt text](/img/2.png)

![alt text](/img/1.png)

![alt text](/img/3.png)

![alt text](/img/4.png)

![alt text](/img/5.png)

![alt text](/img/6.png)

![alt text](/img/7.png)



![alt text](/img/neural_net2.jpeg)

Let's say, you want to predict some output Y given some input value X. For example, maybe you want to predict your score in exam based on how many hours you sleep and how many 
hours you study night before. To use a machine learning approach, you need some data,

![alt text](/img/starting.png)

Let's say you recorded your number of study hours ,number of sleep and score on test. We will be using numpy to store our 2d array

![alt text](/img/numpy.png)

This is called supervised regression.It is supervised because this example has inputs and outputs and it is a regression problem because we are predicting your test score, which is 
continous output.If we were predicting your test grade than it will be called classification problem and non-regression problem.

We will use Artificial Neural Network, this is usually based on how the neurons works in our brain.Before we pass through our data into the model, we need to fix the differences in the units of our data. Both our inputs are in hour but our output is a test score on the scale between 0-100. Neural networks are smart but not smart enough to guess the units of our data. It is like asking our model to compare apples to oranges but most learning models want to compare only apples to apples.

The solution is to scale our data that way our model only see standardized units

![alt text](/img/scaling.png)

Now we can build our neural network and we know our network has two inputs and one output. We will call our output data ŷ because it is an estimate of y but not same as y.
Any layer between input and output is called hidden layer and Nowadays we can built many hidden layers,these are known deep network.

![alt text](/img/synapse2.png)

Here, we are going to use one hidden layer with 3 hidden units but if you want to build a deep neural network then just stack bunch of layers together. Synapse have a very simple job, they take a value and multiply by specific weight and update the result. Neurons are little more complicated, their job is to add together the output from all their synapses and apply activation function.Few activation functions allow neuron nets to model complex non-linear patterns that simple model may miss. For our model we will use sigmoid activation function.


## Forward Propagation

Now, we will implement our neural network in python.


Our network has two input  and 3 hidden units and one output and these are the example of hyperparameters. Hyperparameters are constant that establish the structure and behaviour of network but can not be updated as we train the network. Our learning algorithm is not capable of deciding if it needs another hidden layer unit. What neural net do learn are the parameters, specifically weight on synapse. We will move our data through our network, in a method called forward propagation. Rather than passing inputs to networks one at a time,

![alt text](/img/elementwise.png)

we are going to use matrics to pass through multiple inputs at a once. This will allow us doing big computations speed up.

![alt text](/img/matrix.png)

Our input data matrix X is of dimension 3x2 and corresponding output Y is of dimension 3x1

![alt text](/img/starting.png)

Each input value or element in matix X needs to be multiply by corresponding weight than added together with all other result for each neuron.

```python
import numpy as np

X = np.array(([3,5], [5,1], [10,2]), dtype=float)
y = np.array(([75],[82],[93]), dtype=float)
X = X/np.amax(X, axis=0)
y = y/100 #max test score is 100

class Neural_Network(object):
    def __init__(self):
        #define Hyperparamters
        self.inputLayerSize = 2
        self.outputLayerSize = 1
        self.hiddenLayerSize = 3
        
        #Weights (Parameters)
        self.W1 = np.random.randn(self.inputLayerSize, self.hiddenLayerSize)
        self.W2 = np.random.randn(self.hiddenLayerSize, self.outputLayerSize)
    def forward(self, X):
        # Propagate input through network
        self.z2 = np.dot(X, self.W1)
        self.a2 = self.sigmoid(self.z2)
        self.z3 = np.dot(self.a2, self.W2)
        yhat = self.sigmoid(self.z3)
        return yhat
    def sigmoid(self, z):
        #Apply sigmoid activatio function to scalar, vector
        return 1/(1+np.exp(-z))

NN = Neural_Network()

yhat = NN.forward(X)

print(yhat)
```



## Happy Technology Day!!






