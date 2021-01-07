---
title: Lists
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: p2_python7.html
# simple_map: true
# map_name: usermap
# box_number: 2
folder: product2
---

## Lists

In Python, there are a few different sequence types that we're going to work with, the most common of which is the list type. In this lesson, we'll go through how we can create and modify lists.

### Python Documentation For This Video

- [Sequence Types](https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range)
- [Lists](https://docs.python.org/3/library/stdtypes.html#list)

### Lists

We create a list in Python by using the square brackets ([]) and separating the values with commas. Here's an example list:

```cmd
>>> my_list = [1, 2, 3, 4, 5]
```

For standard use, there's not a limit to how long our list can be. Lists are a heterogeneous collection type, so the items within the list do not all need to be of the same type:

```cmd
>>> other_list = ['a', 1, 1.0, False]
```

### Reading from Lists

To access an individual element of a list, we index it the same way that we would for a character in a string:

```cmd
>>> my_list[0]
1
>>> my_list[2]
2
```

If we try to access an index that is too high (or too low) then we'll receive an error:

```cmd
>>> my_list[5]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```

To make sure that we're not trying to get an index that is out of range, we can test the length using the len function (and then subtract 1):

```cmd
>>> len(my_list)
5
```

Additionally, we can access subsections of a list by "slicing" it. We provide the starting index and the ending index (the object at that index won't be included):

```cmd
>>> my_list[0:2]
[1, 2]
>>> my_list[1:0]
[2, 3, 4, 5]
>>> my_list[:3]
[1, 2, 3]
>>> my_list[0::1]
[1, 2, 3, 4, 5]
>>> my_list[0::2]
[1, 3, 5]
```

### Modifying a List

Unlike strings, which can't be modified (we can't change a character in a string), we can change a value in a list using the subscript equals operation:

```cmd
>>> my_list[0] = "a"
>>> my_list
['a', 2, 3, 4, 5]
```

Lists can be added together (concatenated). This operation will return a new list, but we can use the += compound operator to add items to the end of our lists:

```cmd
>>> my_list + [8, 9, 10]
['a', 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> my_list += [8, 9, 10]
>>> my_list
['a', 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

Items in lists can be set using slices as well:

```cmd
>>> my_list[1:3] = ['b', 'c']
>>> my_list
['a', 'b', 'c', 4, 5, 6, 7, 8, 9, 10]
```

Slicing and assigning can still be used if the slice size is smaller than the list being assigned. This will insert additional elements:

```cmd
>>> my_list[3:5] = ['d', 'e', 'f']
>>> print(my_list)
['a', 'b', 'c', 'd', 'e', 'f', 6, 7, 8, 9, 10]
```

We can remove a section of a list by assigning an empty list to the slice:

```cmd
>>> my_list = ['a', 'b', 'c', 'd', 5, 6, 7]
>>> my_list[4:] = []
>>> my_list
['a', 'b', 'c', 'd']
```

### Removing Items from a List

Another way that we can remove an item from a list is by using the del statement and the indexing operation:

```cmd
>>> my_list = ['a', 'b', 'c', 'd']
>>> del my_list[0]
>>> my_list
['b', 'c', 'd']
```

One thing to note about del is that it will remove the entire list variable if we don't pass it an index:

```cmd
>>> del my_list
>>> my_list
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'my_list' is not defined
```

## List Functions and Methods

We've learned how to use some list operators to interact with our lists, but there are quite a few useful methods and functions that will make working with lists even easier.

### Documentation For This Video

- [List Methods](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)
- [The sorted function](https://docs.python.org/3/library/functions.html#sorted)
- [The reversed function](https://docs.python.org/3/library/functions.html#reversed)
- [Common Sequence Operations](https://docs.python.org/3/library/stdtypes.html#common-sequence-operations)

### List Methods

When it comes to lists, some methods allow us to easily achieve the same things that we previously did using operators, and in an arguably more readable way. Indexing and slicing for the sake of reading objects is easy enough, but when it comes to adding new items to a list, there are better methods.

If we want to add an object to the end of a list, then we can use the append method:

```cmd
>>> my_list = [1, 2, 3]
>>> my_list.append(4)
>>> my_list
[1, 2, 3, 4]
```

Additionally, if we'd like to insert an item at a particular index, we can use the insert method:

```cmd
>>> my_list.insert(0, 'a')
>>> my_list
['a', 1, 2, 3, 4]
```

Notice that we didn't replace the item that had previously been at the 0 index. We moved all items at or after the desired index, further back in the list.

If we need to know the index of an item in a list (if the item is in the list), then we have the index method:

```cmd
>>> my_list = [1, 2, 3]
>>> my_list.index(2)
1
>>> my_list.index(15)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: 15 is not in list
```

Since index raises an error, it's not something that we'll usually want to use by itself. Thankfully, there's an easy way for us to determine if an item is in a list.

### The in and not in Operators

Sequence types have a few additional operators that make it easy for us to check the contents. The in and not in operators take a value that we'd like to search the sequence for on the left-hand side and a sequence on the right-hand side:

```cmd
>>> my_list = [1, 2, 3]
>>> 4 in my_list
False
>>> 4 not in my_list
True
>>> 2 in my_list
True
```

These operators are great to use before employing the index method to ensure that we don't get a ValueError.

### Helpful Functions

Besides methods, some built-in functions work great with lists. We've already seen the len function that will return the length of the list to us, but if we need to sort the contents of a list, then we have the sorted and reversed functions:

```cmd
>>> my_list = [1, 3, 4, 8, 2]
>>> sorted(my_list)
[1, 2, 3, 4, 8]
>>> reversed(my_list)
<list_reverseiterator object at 0x110330d90>
```

The reversed function doesn't return a list, but typecasting works for the list type also, and when we have a list iterator we can turn it back into a list using the list function:

```cmd
>>> reversed(my_list)
<list_reverseiterator object at 0x110330d90>
>>> list(reversed(my_list))
[2, 8, 4, 3, 1]
```

If we want to sort, reverse, and get a list back, we can combine all three of these functions:

```cmd
>>> list(reversed(sorted(my_list)))
[8, 4, 3, 2, 1]
```

## Nested Lists: Matrices and Cubes

Lists are a heterogeneous data structure and can hold onto a variety of data types, this includes other lists. In this lesson, we'll take a look at how we can model matrices in Python by nesting lists.

### Creating a Matrix

Matrices are a structure that has rows and columns. To model a matrix in Python, we need a new list for each row, and we'll need to make sure that each list is the same length so that the columns work properly.

Here's an example matrix not in code:
```
1 2 3
4 5 6
```

To model this matrix in Python, we'll do this:

```cmd
>>> my_matrix = [[1, 2, 3],
...              [4, 5, 6]]
>>> my_matrix
[[1, 2, 3], [4, 5, 6]]
```

To determine how many rows are in a multi-dimensional list, we need to use the len function on the matrix itself. To get the number of columns, we would use len on any row in the matrix (assuming that it's a proper matrix with each row having the same number of columns):

```cmd
>>> row_count = len(my_matrix)
>>> column_count = len(my_matrix[0])
>>> row_count
2
>>> column_count
3
```

Now if we want to interact with an individual item in the matrix, we need to index our variable two times, first with the row, and second with the column:

```cmd
>>> my_matrix[0][1]
2
```

### Squares and Cubes

Matrixes with specific dimensions have names. If a matrix has the same number of rows as columns, then it can be classified as a "cube", and some cubes have unique names. A square is 2x2, and a cube (like the 3D shape) is 3x3. The matrix that we've already created is a 2x3 matrix, and this doesn't have a special name.



{% include links.html %}
