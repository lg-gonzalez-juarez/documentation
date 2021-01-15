---
title: 23. Using NumPy
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: pyth_03.html
folder: python
---

## 23.1. What are NumPy Arrays?

[NumPy](https://numpy.org/) is a fundamental package for many math and science computations using Python. NumPy provides an array that can have N-dimensions. NumPy serves as the base for many packages that can extend its capabilities, such as, ```pandas``` and ```scikit-learn```. It is a lean package focusing on operations on arrays. These other packages add functionality to it. However, it is a powerful package for many higher-level math operations.

## Overview of NumPy

### Installing and Using NumPy

Installing NumPy is as simple as using ```pip install```:

```
python -m pip install numpy
```

Once the package is installed, it must be imported to use it. Enter into the REPL, by entering ```python```. Once inside the REPL, standard practice is to import it as ```np```:

```
import numpy as np
```

### Arrays

NumPy operates on arrays. A 1-d array can be thought of as a Python list or as a column from a database. A multi-dimensional array can be thought of as many lists or columns in a database. While this is not exactly what the array is, it's a useful way to imagine them. If you create arrays using the array module, all elements of the array must be of the same type.

### Create Array

Let's create an array that holds the first ten integers:

```
>>> import numpy as np
>>> simple_array = np.arange(10)
>>> simple_array
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
>>>
```

We can also do the same thing, but instead of integers we'll use floats by using [dtypes](https://numpy.org/doc/stable/user/basics.types.html):

```
>>> float_array = np.arange(10, dtype=float)
>>> float_array
array([0., 1., 2., 3., 4., 5., 6., 7., 8., 9.])
>>>
```

It is possible to change the type of the elements in an array using ```astype```. Let's convert our float array to complex numbers:

```
>>> complex_array = float_array.astype(complex)
>>> complex_array
array([0.+0.j, 1.+0.j, 2.+0.j, 3.+0.j, 4.+0.j, 5.+0.j, 6.+0.j, 7.+0.j,
       8.+0.j, 9.+0.j])
>>>
```

We can also create a NumPy array for a list or data file.

Let's load ```int_list``` as an array named ```example_array```:

```
int_list = [1297, 603, 1071, 539, 1222, 1424, 986, 397, 970, 1102, 499, 533, 908, 559, 386, 1183, 595, 69, 1141, 76, 863, 1343, 185, 895, 1312, 50, 918, 677, 394, 629, 1317, 944, 466, 751, 1050, 301, 415, 784, 19, 1395, 1223, 979, 252, 1155, 59, 107, 632, 995, 972, 867, 332, 751, 810, 50, 55, 218, 997, 1085, 475, 1494]
>>> int_list = [1297, 603, 1071, 539, 1222, 1424, 986, 397, 970, 1102, 499, 533, 908, 559, 386, 1183, 595, 69, 1141, 76, 863, 1343, 185, 895, 1312, 50, 918, 677, 394, 629, 1317, 944, 466, 751, 1050, 301, 415, 784, 19, 1395, 1223, 979, 252, 1155, 59, 107, 632, 995, 972, 867, 332, 751, 810, 50, 55, 218, 997, 1085, 475, 1494]
>>> int_array = np.array(int_list)
>>> int_array.dtype
dtype('int64')
>>> int_array
array([1297,  603, 1071,  539, 1222, 1424,  986,  397,  970, 1102,  499,
        533,  908,  559,  386, 1183,  595,   69, 1141,   76,  863, 1343,
        185,  895, 1312,   50,  918,  677,  394,  629, 1317,  944,  466,
        751, 1050,  301,  415,  784,   19, 1395, 1223,  979,  252, 1155,
         59,  107,  632,  995,  972,  867,  332,  751,  810,   50,   55,
        218,  997, 1085,  475, 1494])
>>>
```

Let's load the same information from a file named ```scores.csv```. We will use ```np.genfromtxt``` function to read the file and create an array out of its content. First, let's download the ```scores.csv``` file we want to use:

```
$ curl -O https://raw.githubusercontent.com/linuxacademy/content-using-pythons-maths-science-and-engineering-libraries/master/scores.csv 
>>> scores_array = np.genfromtxt('scores.csv', delimiter = ',', dtype=int)
>>> scores_array
array([1297,  603, 1071,  539, 1222, 1424,  986,  397,  970, 1102,  499,
        533,  908,  559,  386, 1183,  595,   69, 1141,   76,  863, 1343,
        185,  895, 1312,   50,  918,  677,  394,  629, 1317,  944,  466,
        751, 1050,  301,  415,  784,   19, 1395, 1223,  979,  252, 1155,
         59,  107,  632,  995,  972,  867,  332,  751,  810,   50,   55,
        218,  997, 1085,  475, 1494])
>>>
```

### Index and Slice an Array

Slicing an array in NumPy looks like slicing a list in Python.

From ```scores_array```, let's count the elements by using ```.size```:

```
>>> scores_array.size
60
>>>
```

Let's make an array with the 2nd, 3rd, and 4th element of ```scores_array```. It should be equal to [1071, 539, 1222]:

```
>>> scores_array[2:5]
array([1071,  539, 1222])
>>>
```

As you can see, the indexing and slicing works the same here as it does in basic Python.

### Basic Operations on NumPy Arrays

Information on these operations can be found here.

### Printing

Printing an array is as simple as using ```print```:

```
>>> print(scores_array)
[1297  603 1071  539 1222 1424  986  397  970 1102  499  533  908  559
  386 1183  595   69 1141   76  863 1343  185  895 1312   50  918  677
  394  629 1317  944  466  751 1050  301  415  784   19 1395 1223  979
  252 1155   59  107  632  995  972  867  332  751  810   50   55  218
  997 1085  475 1494]
>>>
```

Note this array doesn't possess commas as the ```genfromtxt()``` does.

### Simple Math Operations

In NumPy, math operations are elementwise. That is, NumPy applies the math operand to the zeroth element of each array, and that is the zeroth element of a new array. It does this for each element in the arrays. You can perform all basic math operands on these arrays.

Let's raise each element in the scores_array to the zero power:

```
>>> scores_array ** 0
array([1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1])
>>> scores_array
array([1297,  603, 1071,  539, 1222, 1424,  986,  397,  970, 1102,  499,
        533,  908,  559,  386, 1183,  595,   69, 1141,   76,  863, 1343,
        185,  895, 1312,   50,  918,  677,  394,  629, 1317,  944,  466,
        751, 1050,  301,  415,  784,   19, 1395, 1223,  979,  252, 1155,
         59,  107,  632,  995,  972,  867,  332,  751,  810,   50,   55,
        218,  997, 1085,  475, 1494])
>>>
```

As you can see, the resulting array is an array of 1's. Remember: Raising a number to the exponent 0 results in 1.
You can also see that this created a new array and did not affect the original array.

### What Did We Learn?

In this lesson, we looked at NumPy arrays. We learned to create them by various means, including reading a CSV file. We learned how to change the type stored in the array and how to index and slice. Finally, we discussed basic operations on arrays, such as printing and simple math. For more information on [NumPy arrays](https://numpy.org/devdocs/user/quickstart.html), take a look at the official documentation.

## 23.2 Reshaping a Numpy Array Into a Matrix

[NumPy](https://numpy.org/) has a matrix function, but the documentation indicates that this function is being deprecated, and using multi-dimension arrays is strongly suggested instead. We will be doing just that in this lesson: creating multi-dimension arrays that are matrices.

Arrays, or vectors, are one-dimensional. That is, they have a single column of items. A matrix is a rectangular arrangement of n rows and m columns, where n and m are greater than one. (For example: A 1 by 5 matrix is an array.)

Vectors (arrays) and matrices are essential to many science, math, and engineering operations. With these, we are reminded of linear algebra.

Note: If you have never used NumPy before, we strongly suggest you see the first lesson in this section, "What are NumPy Arrays?".

## Matrices

### Create a Matrix From a Single Array

A matrix can be formed from a single array by re-arranging it. From the last lesson, we looked at int_list as an array. Remember to import NumPy.

```
>>> import numpy as np
>>> int_list = [1297, 603, 1071, 539, 1222, 1424, 986, 397, 970, 1102, 499, 533, 908, 559, 386, 1183, 595, 69, 1141, 76, 863, 1343, 185, 895, 1312, 50, 918, 677, 394, 629, 1317, 944, 466, 751, 1050, 301, 415, 784, 19, 1395, 1223, 979, 252, 1155, 59, 107, 632, 995, 972, 867, 332, 751, 810, 50, 55, 218, 997, 1085, 475, 1494]
>>> int_array = np.array(int_list)
>>> print(int_array)
[1297  603 1071  539 1222 1424  986  397  970 1102  499  533  908  559
  386 1183  595   69 1141   76  863 1343  185  895 1312   50  918  677
  394  629 1317  944  466  751 1050  301  415  784   19 1395 1223  979
  252 1155   59  107  632  995  972  867  332  751  810   50   55  218
  997 1085  475 1494]
```

```shape``` is a tuple that gives dimensions of the array.

```
>>> int_array.shape
(60,)
```

Let's [reshape](https://numpy.org/doc/1.18/reference/generated/numpy.reshape.html) the ```int_array``` into a 10 x 6 matrix:

```
>>> int_matrix = int_array.reshape(10, 6)
>>> print(int_matrix)
[[1297  603 1071  539 1222 1424]
 [ 986  397  970 1102  499  533]
 [ 908  559  386 1183  595   69]
 [1141   76  863 1343  185  895]
 [1312   50  918  677  394  629]
 [1317  944  466  751 1050  301]
 [ 415  784   19 1395 1223  979]
 [ 252 1155   59  107  632  995]
 [ 972  867  332  751  810   50]
 [  55  218  997 1085  475 1494]]
 >>> int_matrix
array([[1297,  603, 1071,  539, 1222, 1424],
       [ 986,  397,  970, 1102,  499,  533],
       [ 908,  559,  386, 1183,  595,   69],
       [1141,   76,  863, 1343,  185,  895],
       [1312,   50,  918,  677,  394,  629],
       [1317,  944,  466,  751, 1050,  301],
       [ 415,  784,   19, 1395, 1223,  979],
       [ 252, 1155,   59,  107,  632,  995],
       [ 972,  867,  332,  751,  810,   50],
       [  55,  218,  997, 1085,  475, 1494]])
>>>
```

As you can see above, while we are calling this a matrix and it will function as a matrix, it is actually an array type.

### Stacking Arrays

Two functions can be used to stack arrays, [vstack](https://numpy.org/doc/1.18/reference/generated/numpy.vstack.html#numpy.vstack) and [hstack](https://numpy.org/doc/1.18/reference/generated/numpy.hstack.html#numpy.hstack). ```vstack``` stacks the arrays vertically and ```hstack``` stacks the arrays horizontally:

```
>>> a = np.array([1, 2, 3])
>>> print(a)
[1 2 3]
>>> b = np.array([4, 5, 6])
>>> print(b)
[4 5 6]
>>> c = np.vstack((a, b))
>>> print(c)
[[1 2 3]
 [4 5 6]]
>>> d = np.hstack((a,b))
>>> print(d)
[1 2 3 4 5 6]
>>>
```

These functions can also be used on a matrix, however the matrices must be of the same dimensions. As an example, let's do a horizontal stack of a, b, and c:

```
>>> np.hstack((a,b,c))
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<__array_function__ internals>", line 5, in hstack
  File "/Users/lfritts/.pyenv/versions/621-3.8.2/lib/python3.8/site-packages/numpy/core/shape_base.py", line 343, in hstack
    return _nx.concatenate(arrs, 0)
  File "<__array_function__ internals>", line 5, in concatenate
ValueError: all the input arrays must have same number of dimensions, but the array at index 0 has 1 dimension(s) and the array at index 2 has 2 dimension(s)
```

This is also an example of a well-formed error message. It is specific in describing the problem. ```a``` (index 0) has one dimension, and ```c``` (index 2) has two dimensions.

### The concatenate function

```concatenate``` joins arrays and/or matrices along an axis. Axis ```0``` stacks them horizontally, axis ```1``` stacks them vertically, and axis ```None``` flattens them into an array.

```axis = None```

```
>>> a = np.array([[1, 2], [3, 4]])  # this is a matrix
>>> b = np.array([[5, 6]])
>>> np.concatenate((a,b), axis=None) # should flatten them
array([1, 2, 3, 4, 5, 6])
>>>
```

```axis = 0```

```
>>> np.concatenate((a,b), axis = 0)
array([[1, 2],
       [3, 4],
       [5, 6]])
>>>
```

Notice the element in ```b``` was appended to the items in ```a```. But what would happen if ```b = [5]``` instead of ```b = [5, 6]```? An error would occur.

```
>>> b = np.array([5])
>>> np.concatenate((a,b), axis = 0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<__array_function__ internals>", line 5, in concatenate
ValueError: all the input arrays must have same number of dimensions, but the array at index 0 has 2 dimension(s) and the array at index 1 has 1 dimension(s)
>>>
```

Remember, the dimensions must be the same along the axis you are joining.

```axis = 1```

```
>>> b = np.array([[5, 6]])
>>> np.concatenate((a,b), axis = 1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<__array_function__ internals>", line 5, in concatenate
ValueError: all the input array dimensions for the concatenation axis must match exactly, but along dimension 0, the array at index 0 has size 2 and the array at index 1 has size 1
>>>
```

Please take a minute and determine what the problem is before reading on for the fix.

```
>>> b = np.array([[5, 6], [7, 8]])
>>> np.concatenate((a,b), axis = 1)
array([[1, 2, 5, 6],
       [3, 4, 7, 8]])
>>>
```

### What Did We Learn

In this lesson, we learned various ways of making matrices and ways to concatenate matrices. It is important to consider the dimensions when concatenating arrays or matrices, regardless of the method.

## 23.3. Math Operations on Arrays/Matrices

[NumPy](https://numpy.org/) allows for simple math and linear algebra operations to be used on arrays and matrices. In this lesson, we will look at simple math operands. Here are some [linear algebra](https://numpy.org/doc/stable/reference/routines.linalg.html) operations.

Note: If you have never used NumPy before, we strongly suggest you see the first two lessons in this section, What are NumPy Arrays? and Reshaping a Numpy Array into a Matrix.

### Math Operands on Arrays and Matrices

In NumPy, math operations are elementwise. That is, NumPy applies the math operand to the zeroth element of each array, and that is the zeroth element of a new array. It does this for each element in the arrays.

Let's try addition on two arrays. Note that these arrays need the same amount of elements in both arrays when adding:

```
>>> a = np.array([1, 2, 3, 4, 5])
>>> b = np.array([10, 20, 30, 40, 50])
>>> c = a + b
>>> print(c)
[11 22 33 44 55]
>>>
```

You can also perform operations between an array and a single value:

```
>>> print(a)
[1 2 3 4 5]
>>> a / 2.5
array([0.4, 0.8, 1.2, 1.6, 2. ])
>>>
```

Notice the ints in the array were changed to floats.

### Linear Algebra

In this lesson, we looked at simple math operands. You can also do linear algebra on arrays and matrices. For more information, see [here](https://numpy.org/doc/stable/reference/routines.linalg.html).


## Hands-On Lab 23: Creating a Matrix Using NumPy Arrays






{% include links.html %}
