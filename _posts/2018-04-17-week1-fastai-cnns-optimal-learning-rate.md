---
layout: post
title: "Week 1 fast.ai- CNNs, kernel, Learning Rate"
date: 2018-04-17
---

Deep learning is essentially a particularway of doing machine learning whereyou give your system a bunch of examples and then it learns the rules and representations vs manually programming the rules. We have interesting applications today like face detection, self-driving cars , etc. Deep learning allows machine to train itself much longer and therefore learn much "deeper" and ultimately producing much more accurate predictions.

Machine leanring has recently evolved into Deep learning mainly due to these factors:

* Acess to much faster and more powerful computers
* Vast amount of data available now

## CNNs

CNNs are the most important architecture for deep neural networks. They are the state of the art for solving some big problems.

The basic of structure of a CNN is the convolution whicj on its is a relatively starightforward process. A convolution is a linear operation that finds interesting features in an image. Performing ine instance of the convolution operation requires following steps:

* Identify kernel matrix -  this is typically a 3 x 3 matrix or in some cases a 1 x 1 matrix.
* Perform element wise multiplication between kernel and image pixels.
* Sume all the elements
* Assign the sum as the new pixel in the overlayed image crop in the activation map

This operation repeated until we have completed passes over the entire image.

----> Others parameters like kernel and padding that determine the dimension of the activation maps, will discuss in next blog.

To train an image classifier using Fastai library you need to:

* Select a starting architecture: resnet34 is a good start
* determine the number of epochs: start with 1, observe results and then run multiple epochs if needed
* Determine the learning rate: Using the strategy in the cyclical learning rate paper, we keep increasing learning rate until the loss starts decreasing. This will
probably take less tha one epoch if you have a small batch size
* train **learn** size

Reference
