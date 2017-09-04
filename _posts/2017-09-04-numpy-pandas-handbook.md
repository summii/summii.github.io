---
layout: post
title: "Data Science- numpy and pandas Handbook"
date: 2017-09-04
---

## Starting with Numpy and Pandas
Load the library and check its version
```python

Import numpy as np
#np as an alias
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

> ['0', '1', '2', '3', '4', '5', '6','7','8','9']
```
```python
[type(item) for item in L]

> [int,int,int,int,int,int,int,int,int,int]
```

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
       
#creating array with set of sequence

np.arange(0,15,3)
> array([ 0,  3,  6,  9, 12])
```

Array Indexing

```python
x1 = np.array([2,3,4,5,6,7])
x1
array([2,3,4,5,6,7])

#assess zero index

x1[0] #indexing in python starts at 0
> 2

#assess fifth value

x1[4]
> 6

#assess last value

x1[-1]
> 7

# we need to specify row and column in multidimensional array

x2 = np.array([[3, 7, 5, 5],
               [0, 1, 5, 9],
               [3, 0, 5, 0]])
      
#first row and second column

x2[2,3]
> 0

#replace value at 0,0

x2 [0,0] = 12
x2
>
array([[12, 7, 5, 5],
      [0, 1, 5, 9],
      [3, 0, 5, 0]])
      
```
Array Slicing

```python
y = np.arange(10)
y
> array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

#from start to 3rd position

y[:4]

> array([0,1,2,3])

#from 4th position to end

y[4:]

> array([4, 5, 6, 7, 8, 9])

#reverse the array

y[::-1]

> array([9, 8, 7, 6, 5, 4, 3, 2, 1, 0])

# array concatenate

x = np.array([1,2,3])
y = np.array([4,5,6])
np.concatenate([x,y])

> array([1,2,3,4,5,6])

```








