---
layout: post
title: "Data Science- numpy and pandas Handbook"
date: 2017-09-04
---

## Starting with Numpy and Pandas
Load the library and check its version
```python
# np as an alias
Import numpy as np
np.__version__
> 1.13.1
```
Create a list consist of numbers 0 to 9
```python
L = list(range(10))
```
List comphrehension - converting integers to string
```python
[str(c) for c in L]
```
> ['0', '1', '2', '3', '4', '5', '6','7','8','9']
```python
[type(item) for item in L]
```
> [int,int,int,int,int,int,int,int,int,int]
Creating arrays
Numpy arrays are homogenous in nature, they consists only one data type
```python
np.zeros(10, dtype='int')

> array([0,0,0,0,0,0,0,0,0,0])

#create 3 x 3 matrix
np.ones((3,5), dtype=float)
> array([[ 1.,  1.,  1.,  1.,  1.],
      [ 1.,  1.,  1.,  1.,  1.],
      [ 1.,  1.,  1.,  1.,  1.]])
     
#creating a matrix with predefined values
np.full((3,5), 2.3)
> array([[ 2.3,  2.3,  2.3,  2.3,  2.3],
       [ 2.3,  2.3,  2.3,  2.3,  2.3],
       [ 2.3,  2.3,  2.3,  2.3,  2.3]])
```
