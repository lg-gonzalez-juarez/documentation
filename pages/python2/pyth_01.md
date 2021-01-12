---
title: Pyth 02
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: pyth_01.html
folder: python
---

# Using SciPy

## Overview of SciPy

[SciPy](https://scipy.org/) is an ecosystem of Python, distinct and separately maintained packages for math, science, and engineering. This ecosystem is composed of:

- [NumPy](https://numpy.org/): array package
- [SciPy library](https://scipy.org/scipylib/index.html): scientific computing package
- [matplotlib](https://matplotlib.org/): 2-d plotting package
- [Ipython](https://ipython.org/): interactive console package, Jupyter Notebook
- [SymPy](https://www.sympy.org/en/index.html): symbolic math package
- [pandas](https://pandas.pydata.org/): data structure and analysis package

In later lessons, will be demonstrating NumPy, matplotlib, and pandas. In this lesson, we are going to briefly look at the documentation for the SciPy library.

The SciPy library contains functions that make computation of higher-order math, science, and engineering calculations easier. However, these concepts are not the focus of this course, and we will not do more than become aware of the possibilities.

# Using NumPy

## What are NumPy Arrays?

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