---
title: 08. Tuples & Dictionaries
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: python_08.html
folder: python
---

## 8.1. Tuples

The most common immutable sequence type that we're going to work with is going to be the tuple.

### Documentation 

- [Sequence Types](https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range)
- [Tuples](https://docs.python.org/3/library/stdtypes.html#tuple)

### Tuples

Tuples are a fixed width, immutable sequence type. We create tuples using parenthesis (()) and at least one comma (,):

```powershell
>>> point = (2.0, 3.0)
```

Since tuples are immutable, we don't have access to the same methods that we do on a list. We can use tuples in some operations like concatenation, but we can't change the original tuple that we created:

```powershell
>>> point_3d = point + (4.0,)
>>> point_3d
(2.0, 3.0, 4.0)
```

One interesting characteristic of tuples is that we can unpack them into multiple variables at the same time:

```powershell
>>> x, y, z = point_3d
>>> x
2.0
>>> y
3.0
>>> z
4.0
```

When we'll most likely to see tuples is while looking at a format string that's compatible with Python 2 (though this will go away soon):

```powershell
>>> print("My name is: %s %s" % ("Keith", "Thompson"))
```

## 8.2. Tuples Versus Lists

One of the biggest questions that we'll have when working with collections is whether we should use a tuple or a list. In this lesson, we'll take a look at when each is useful.

### Tuples vs Lists

When determining if we should use a list or a tuple, we need to ask ourselves one important question:

Will we ever not know the exact number of items that we're storing?

If we answer "yes" to this question, then we should use a list. Lists are great for holding onto real collections: users, phone numbers, etc.

Tuples make more sense in two general situations:

When we're trying to return more than one piece of information from a function
If we want to model something that has a specific number of fields that we can positionally hold in a tuple:
This would be something like a point in 2D or 3D space having x, y, and potentially z. Those values should always be in a specific spot.
Another way that this could be used is to quickly model a "person" that has a name, age, and phone number:

```powershell
>>> person = ('Kevin Bacon', 61, '555-555-5555')
>>> person2 = ('Bob Ross', 76, '')
>>> person[0]
'Kevin Bacon'
>>> person2[0]
'Bob Ross'
```

In this case index, 0 will always return the "name" for a person stored as a tuple.

Fun Fact: While tuples are immutable, their values can change when a tuple holds a reference to a mutable object, like a list.

### Lists in Tuples and Tuples in Lists

To be thorough, we need to understand how having lists within tuples (and tuples within lists) works. Let's start with lists within tuples, followed by tuples within lists:

```powershell
>>> my_list = [1, 2, 3]
>>> my_tuple = (my_list, 1)
>>> my_tuple
([1, 2, 3], 1)
>>> other_list = [1, 2, my_tuple]
>>> other_list
[1, 2, ([1, 2, 3], 1)]
```

We're able to embed lists in tuples and tuples in lists without issues. It's worth noting that tuples are immutable, but they do not require that the items within the tuple be immutable. We can modify the list that is inside of my_tuple:

```powershell
>>> my_tuple
([1, 2, 3], 1)
>>> my_list.append(1)
>>> my_tuple
([1, 2, 3, 1], 1)
```
