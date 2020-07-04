---
layout: post
title: Covolutional Neural Network Part-1
description: Covolutional Neural Network
author: sumeet
use_math: true
tags: [machine learning, python, neural network, beginner]
---

Understanding the fundamentals of `CNN` can be hard to undestand. I find it difficult to meaningfully understand a system without knowing how everything fits together. Hence, the purpose of this blog is to explain through simple peices of code, how CNN works.

From a very top, This is how **CNN** works.

![CNN architecture](/blog/assets/images/00.png)

A **CNN** is a neural network. An algorithm used to recognize patterns in data. Neural network in general are composed os a collection of neurons that are organized in layers, each with their own learnable weights and biases.

# What does each layer of network do?


**Input layer**: The input layer represents the input image into `CNN`. The input layer has channels, corresponding to RGB.

**Convolution layer**: The covolution layers are the foundation of CNN, as they contain the learned kernels(weights), which extract features that distinguish different images from one another.

[Convolution](https://en.wikipedia.org/wiki/Convolution) is a mathematical operation on two functions (f and g) that produces a third function expressing how the shape of one is modified by the other.


A feed forward neural network can be thought of as the composition of number of functions:

\begin{align}
f(x) = f_L(\dots f_2(f_1(x;w_1);w_2)\dots),w_{L}).
\end{align}

The "dot products" between weights and inputs are "integrated" across channel.

Filter weights are shared across receptive fields. The filter has same number of layers as input volume channels, and output volume has some "depth" as the number of filters.

In simple terms, a convolution of image A and Filter B describes to what degree A is "like" B. Here "Filter B" is a kernel, ie., a parameter set learnt by the network.

**Features**:

They accepts a volume of size W * H * D.

Requires four hyperarameters:

- Number of filters
- their spatial extent
- the stride
- the amount of zero padding

**Padding** is often necessary when the kernel extends beyond the activation map. Padding conserves data at the borders of activation maps.

**kernel size** is dimension of the window over input.

**stride** indicates how many pixels the kernel should be shifted over at a time.

**Hyperparameter** an aspect of the algorithm, a dial which changes model production.

**Parameter** an aspect of the model, a dial which is fixed by data.



Let's try out few of above features on an image using `PyTorch`




Supported code to run this practical can be found [here](https://gist.github.com/summii/095567d9cbb9b7daf79e28c2d79d2579)

```python
import lab
from matplotlib import pyplot as plt

# Read an image as a PyTorch tensor
x = lab.imread('<path to image>')

# Visualize the input x
plt.figure(1, figsize=(12,12))
lab.imarraysc(x)

# Show the shape of the tensor
print(f"The image tensor shape is {list(x.shape)}")

# Show the data type of the tensor
print(f"The image tensor type is {x.dtype}")
```

[comment]: <> (![alt text] /blog/assets/images/20.png)


Let us create a bank of 10 linear filters each dimension 3*5*5.

```python
import torch

# Create a bank of linear filters
w = torch.randn(10,3,5,5)

# Visualize the filters
plt.figure(1, figsize=(12,12))
lab.imarraysc(w, spacing=1) ;
```

[comment]: <> (![alt text] /blog/assets/images/21.png)


The next step is applying the filter to the image using `conv2d` function from `torch.nn.functional`

```python
import torch.nn.functional as F

# Apply the convolution operator
y = F.conv2d(x, w)

# Visualize the convolution result
print(f"The output shape is {y.shape}")

#We can now visualise the output y of the convolution. 
fig = plt.figure(figsize=(15,10))

#Visulaize the output image, one channel per image
lab.imarraysc(lab.t2im(y));
```

[comment]: <> (![alt text] /blog/assets/images/22.png)


Note that filters preserve the resolution of the input feature map. However, it is often useful to downsample the output. This can be obtained by using stride option in `conv2d`. 

```py
# downsample output image using stride
y_ds = F.conv2d(x,w, stride=16)
plt.figure(figsize=(15,10))
lab.imarraysc(lab.t2im(y_ds));
```

[comment]: <> (![alt text](/blog/assets/images/23.png)

Note also that applying a filter to an image or fetaure map interacts with boundaries, we can pad unput array with zeros by using `padding` option.

```py
#downsample using padding
y_ds = F.conv2d(x,w, padding=8)
plt.figure(figsize=(15,10))
lab.imarraysc(lab.t2im(y_ds));
```

[comment]: <> (![alt text](/blog/assets/images/24.png)


Try changing padding value to see the difference between above too images.

Now we will design a filter from scratch.

```py
#Initialize a filter
w = torch.Tensor([
    [0,  1, 0 ],
    [1, -4, 1 ],
    [0,  1, 0 ]
])[None, None, :, :].expand(1,3,3,3)


print(f"The shape of the filter w is {list(w.shape)}")

#Apply the covolution
y_lap = F.conv2d(x, w) ;

# Output
plt.figure(1, figsize=(12,12))
lab.imsc(y_lap[0]);

# absolute value of output
plt.figure(2, figsize=(12,12))
lab.imsc(abs(y_lap[0]));
```

[comment]: <> (![alt text](/blog/assets/images/25.png)

[comment]: <> (![alt text](/blog/assets/images/26.png)

## Activation Functions

Let us try out non-linear operators as well. 

The simplest non-linearity is obtained by following a linear filter by a non-linear activation function, applied identically to each component (i.e. point-wise) of a feature map. The simplest such function is the **Rectified Linear Unit** (ReLU).

**ReLU**: Most of the modern CNNs perform on highest level because:

- They consist of an absurd amount of layers, which are able to learn more and moe features.

- their non-linearity

ReLU applies much needed non-linearity into the model without affecting receptive fields of convolution layers. Non-linearity is necesary to produce non-linear decision boundaries, so that the output cannot be written as a linear combination of inputs. CNNs using ReLU are faster to train than their counterparts. The activation function is applied elemnetwise on every value from the input tensor. For example, if applied ReLU on the value 2.24, the result would be 2.24, since 2.24 is larger than 0.


## Pooling

A pooling operator operates on individual feature channels, coalescing nearby feature values into one by the application of a suitable operator. Common choices include max-pooling (using the max operator) or sum-pooling (using summation). The max-pooling operation requires selecting a kernel size and a stride length during architecture design.

## Flatten layer

This layer converts a three-dimensional layer in the neural network into a one-dimesional vector to fit the input of a fully connected layer for classification. For example, a 5*2*2 tensor would be converted into a vector of size 50. We will use the softmax function to classify these features which requires a one-dimensional input. This is why flatten layer is necessary.


```python
#Initialize a filter
w = torch.Tensor([1, 0, -1])[None,None,:].expand(1,3,3,3)

#Convolution
y = F.conv2d(x,w)

#Relu
z = F.relu(y)

plt.figure(1, figsize=(12,12))
lab.imsc(y[0]);

plt.figure(2, figsize=(12,12))
lab.imsc(z[0]);
```

[comment]: <> (![alt text](/blog/assets/images/27.png)
[comment]: <> (![alt text](/blog/assets/images/28.png)


```python
y = F.max_pool2d(x, 15)

plt.figure(1, figsize=(12,12))
lab.imarraysc(lab.t2im(y));
```

[comment]: <> (![alt text](/blog/assets/images/29.png)



```python
#Normalisation
y_nrm = F.local_response_norm(x, 5, alpha=5, beta=0.5, k=0)

plt.figure(1, figsize=(12,12))
lab.imarraysc(lab.t2im(y_nrm));
```

[comment]: <> (![alt text](/blog/assets/images/210.png)

## Softmax

A special kind of activation layer, usually at the end of FC layer outputs. A softmax operation serves a key purpose, making sure CNN outputs sum to 1. Because of this, softmax operations are useful to scale model outputs into probabilities.

In the next [part](https://summii.github.io/blog/2020/04/07/convolutional-neural-network-part-2.html), We will try to build an tiny `CNN` model.

Reference:
- https://web.stanford.edu/class/cs231a/lectures/intro_cnn.pdf


