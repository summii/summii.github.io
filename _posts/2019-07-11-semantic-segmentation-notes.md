---
layout: post
title: "Semantic Segmentation Notes"
---

### Semantic segmentation

- semantic segmentation of an image is to assign each pixel in the input image a semantic class in order to get pixel wise-dense classification

- semantic segmentation is understanding an image at pixel level, i.e we want to assign each pixel in the image an object class.



Network architecture
- A general semantic segmentation architecture can be broadly thought of as an encoder network followed by decoder network

- The encoder is usually is a pre-trained classification network like VGG/Resnet followed by decoder network

- The task of decoder is to semantically project the discriminative features(lower resolution) learnt by the encoder onto pixel space(higher resolution) to get a dense classification.

- Unlike classification where the end result of the very deep network is the only important thing, semantic segmentation not only require discrimination at pixel level but also a mechanism to project discriminative features learnt at different stages of the encoder onto the pixel space. Different architectures employ different mechanisms (skip connections, pyramid pooling etc) as a part of the decoding mechanism.

- unlike classification, we need dense pixel-wise predictions from our models


Network architecture - take two

- Problems of CNNs

  - pooling layers - pooling layers increase the field of view and are able to aggrgate the context while discarding the 'where' information. However, semantic segmentation requires the exact aligment of class maps and thus, needs the 'where' information to be preserved. 

- Two different classes of architectures in the literature to tackle this issue

  - First one is encoder-decoder architecture. Encoder gradually reduces the spatial dimension with pooling layers and decoder gradually recovers the object details and spatial dimensions

  - There are usually shortcut connections from encoder to decoder to help decoder recover the object details better.Ex: U-Net

- Conditional random fields (CRF) postprocessing are usually used to improve the segmentation. CRFs are graphical models which 'smooth' segmentation based on the underlying image intensities.They work based on the observation that similar intensity pixels tend to be labeled as the same class. CRFs can boost scores by 1-2%.



FCN(fully convolutional network) key features:
  - The features are merged from different stages in the encoder which vary in coarseness of semantic information.

  - The upsampling of learned low resolution semantic feature maps is done using deconolutions which are initialized with bilinear interpolation filters.

  - Excellent example for knowledge transfer from modern classifier network like VGG16, Alexnet to perform semantic segmentation

[Visualization of network](http://ethereon.github.io/netscope/#/preset/fcn-8s-pascal)


Terms:

  - Upsampling is the process of inserting zero-valued samples between original samples to increase the sampling rate.