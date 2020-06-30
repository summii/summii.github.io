---
layout: post
title: Covolutional Neural Network Part-1
description: Covolutional Neural Network
author: sumeet
use_math: true
tags: [machine learning, python, neural network, beginner]
---

[Convolution](https://en.wikipedia.org/wiki/Convolution) is a mathematical operation on two functions (f and g) that produces a third function expressing how the shape of one is modified by the other. The term convolution refers to both the result function and to the process of computing it. It is defined as the integral of the product of the two functions after one is reversed and shifted (The convolution of f and g is written f∗g). And the integral is evaluated for all values of shift, producing the convolution function.

A feed forward neural network can be thought of as the composition of number of functions:

\begin{align}
f(x) = f_L(\dots f_2(f_1(x;w_1);w_2)\dots),w_{L}).
\end{align}



One of the property of `CNN` is that the functions f(l) have a convolutional structure. This mean that 𝑓(l) applies to the input map x(l) and operator that is local and translation in variant. Examples of convolutional operators are applying a bank of linear filters to x. 

The first one is regular linear convolution.


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

![alt text](/blog/assets/images/20.png)

Let us create a bank of 10 linear filters each dimension 3*5*5.

```python
import torch

# Create a bank of linear filters
w = torch.randn(10,3,5,5)

# Visualize the filters
plt.figure(1, figsize=(12,12))
lab.imarraysc(w, spacing=1) ;
```
![alt text](/blog/assets/images/21.png)

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

![alt text](/blog/assets/images/22.png)


Note that filters preserve the resolution of the input feature map. However, it is often useful to downsample the output. This can be obtained by using stride option in `conv2d`. 

```python
# downsample output image using stride
y_ds = F.conv2d(x,w, stride=16)
plt.figure(figsize=(15,10))
lab.imarraysc(lab.t2im(y_ds));
```

![alt text](/blog/assets/images/23.png)

Note also that applying a filter to an image or fetaure map interacts with boundaries, we can pad unput array with zeros by using `padding` option.

```python
#downsample using padding
y_ds = F.conv2d(x,w, padding=8)
plt.figure(figsize=(15,10))
lab.imarraysc(lab.t2im(y_ds));
```

![alt text](/blog/assets/images/24.png)

Try changing padding value to see the difference between above too images.

Now we will design a filter from scratch.

```python
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

![alt text](/blog/assets/images/25.png)

![alt text](/blog/assets/images/26.png)

## Non-linear Activation Functions

Let us try out non-linear operators as well. 

The simplest non-linearity is obtained by following a linear filter by a non-linear activation function, applied identically to each component (i.e. point-wise) of a feature map. The simplest such function is the Rectified Linear Unit (ReLU).

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

![alt text](/blog/assets/images/27.png)
![alt text](/blog/assets/images/28.png)

## Pooling

A pooling operator operates on individual feature channels, coalescing nearby feature values into one by the application of a suitable operator. Common choices include max-pooling (using the max operator) or sum-pooling (using summation).

```python
y = F.max_pool2d(x, 15)

plt.figure(1, figsize=(12,12))
lab.imarraysc(lab.t2im(y));
```

![alt text](/blog/assets/images/29.png)

## Normalisation

This operator normalises the vector of feature channels at each spatial location in the input map 𝐱.

```python
#Normalisation
y_nrm = F.local_response_norm(x, 5, alpha=5, beta=0.5, k=0)

plt.figure(1, figsize=(12,12))
lab.imarraysc(lab.t2im(y_nrm));
```

![alt text](/blog/assets/images/210.png)

## Back-propagation and derivatives

We have so far discussed the convolutional operators. We haven’t yet discussed how we learn the parameters of the networks i.e, weights and biases of the layers.

### Derivative

Derivative of function measures sensitivity of change in fucntion value (output value) with respect to a change in its argument (input value).

### Gradient

The gradient is a multi-variable generalization of the derivative. It is a vector valued function.


Training CNNs is normally done using a gradient-based optimization method. The CNN $f$ is the composition of $L$ layers $f_l$ each with parameters $\bw_l$, which in the simplest case of a chain looks like:


 \bx_0
 \longrightarrow
 \underset{\displaystyle\underset{\displaystyle\bw_1}{\uparrow}}{\boxed{f_1}}
 \longrightarrow
 \bx_1
 \longrightarrow
 \underset{\displaystyle\underset{\displaystyle\bw_2}{\uparrow}}{\boxed{f_2}}
 \longrightarrow
 \bx_2
 \longrightarrow
 \dots
 \longrightarrow
 \bx_{L-1}
 \longrightarrow
 \underset{\displaystyle\underset{\displaystyle\bw_L}{\uparrow}}{\boxed{f_L}}
 \longrightarrow
 \bx_L

During learning, the last layer of the network is the *loss function* that should be minimized. Hence, the output $\bx_L = x_L$ of the network is a **scalar** quantity (a single number).

The gradient is easily computed using using the **chain rule**. If *all* network variables and parameters are scalar, this is given by:


 \frac{\partial f}{\partial w_l}(x_0;w_1,\dots,w_L)
 =
 \frac{\partial f_L}{\partial x_{L-1}}(x_{L-1};w_L) \times
 \cdots
 \times
 \frac{\partial f_{l+1}}{\partial x_l}(x_l;w_{l+1}) \times
 \frac{\partial f_{l}}{\partial w_l}(x_{l-1};w_l)

