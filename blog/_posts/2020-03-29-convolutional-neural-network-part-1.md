---
layout: post
title: Covolutional Neural Network Part-1
description: Covolutional Neural Network
author: sumeet
use_math: true
tags: [machine learning, python, neural network, beginner]
---

Covolution: A feed forward neural network can be thought of as the composition od number of functions:
				𝑓(𝐱)=𝑓𝐿(…𝑓2(𝑓1(𝐱;𝐰1);𝐰2)…),𝐰𝐿).

One of the property of `CNN` is that the functions 𝑓 have a convolutional structure. This mean that 𝑓 applies to the input map x and operator that is local and translation in variant. Examples of convolutional operators are applying a bank of linear filters to x. The first one is regular linear convolution.

Let us try out now.

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
#In order to do this, use the provided lab.imarraysc function to display an image for each feature channel in y
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