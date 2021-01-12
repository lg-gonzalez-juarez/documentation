---
title: Tuples & Dictionaries
tags: [python]
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: python_09.html
folder: python
---

## Tuples

The most common immutable sequence type that we're going to work with is going to be the tuple.

### Documentation For This Video

- [Sequence Types](https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range)
- [Tuples](https://docs.python.org/3/library/stdtypes.html#tuple)

### Tuples

Tuples are a fixed width, immutable sequence type. We create tuples using parenthesis (()) and at least one comma (,):

```mcd
>>> point = (2.0, 3.0)
```

Since tuples are immutable, we don't have access to the same methods that we do on a list. We can use tuples in some operations like concatenation, but we can't change the original tuple that we created:

```mcd
>>> point_3d = point + (4.0,)
>>> point_3d
(2.0, 3.0, 4.0)
```

One interesting characteristic of tuples is that we can unpack them into multiple variables at the same time:

```mcd
>>> x, y, z = point_3d
>>> x
2.0
>>> y
3.0
>>> z
4.0
```

When we'll most likely to see tuples is while looking at a format string that's compatible with Python 2 (though this will go away soon):

```mcd
>>> print("My name is: %s %s" % ("Keith", "Thompson"))
```

## Tuples Versus Lists

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

```mcd
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

```mcd
>>> my_list = [1, 2, 3]
>>> my_tuple = (my_list, 1)
>>> my_tuple
([1, 2, 3], 1)
>>> other_list = [1, 2, my_tuple]
>>> other_list
[1, 2, ([1, 2, 3], 1)]
```

We're able to embed lists in tuples and tuples in lists without issues. It's worth noting that tuples are immutable, but they do not require that the items within the tuple be immutable. We can modify the list that is inside of my_tuple:

```mcd
>>> my_tuple
([1, 2, 3], 1)
>>> my_list.append(1)
>>> my_tuple
([1, 2, 3, 1], 1)
```

## Dictionaries

Learn how to use dictionaries (the dict type) to hold onto key/value information in Python.

### Python Documentation For This Video

[Dictionaries](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict)


### Dictionaries

Dictionaries are the main mapping type that we'll use in Python. This object is comparable to a Hash or "associative array" in other languages.

Things to note about dictionaries:

1. Unlike Python 2 dictionaries, Python 3.7 keys are ordered in dictionaries. We will need OrderedDict if we want this to work on another version of Python.
2. You can set the key to any IMMUTABLE TYPE (no lists).
3. Avoid using things other than simple objects as keys.
4. Each key can only have one value (so we don't have duplicates when creating with dict).
We create dictionary literals by using curly braces ({ and }), separating keys from values using colons (:), and separating key/value pairs using commas (,). Here's an example dictionary:

```cmd
>>> ages = { 'kevin': 59, 'alex': 29, 'bob': 40 }
>>> ages
{'kevin': 59, 'alex': 29, 'bob': 40}
```

We can read a value from a dictionary by subscripting using the key:

```
>>> ages['kevin']
59
>>> ages['billy']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'billy'
```

Keys can be added or changed using subscripting and assignment:

```cmd
>>> ages['kayla'] = 21
>>> ages
{'kevin': 59, 'alex': 29, 'bob': 40, 'kayla': 21}
```

Items can be removed from a dictionary using the del statement:

```cmd
>>> del ages['kevin']
>>> ages
{'alex': 29, 'bob': 40, 'kayla': 21}
>>> del ages
>>> ages
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'ages' is not defined
```

### The `in` and `not` in Operators

Just like with lists and tuples, dictionaries have access to the in and not in operators. Notably, this only considers the keys:

```cmd
>>> ages = {'kevin': 59, 'bob': 40}
>>> 'kevin' in ages
True
>>> 59 in ages
False
Alternative Ways to Create a dict Using Keyword Arguments
```

There are a few other ways to create dictionaries that we might see, which are those using the dict constructor with key/value arguments and a list of tuples:

```cmd
>>> weights = dict(kevin=160, bob=240, kayla=135)
>>> weights
{'kevin': 160, 'bob': 240, 'kayla': 135}
>>> colors = dict([('kevin', 'blue'), ('bob', 'green'), ('kayla', 'red')])
>>> colors
{'kevin': 'blue', 'bob': 'green', 'kayla': 'red'}
```

## Dictionary Methods

The `dict` type has plenty of useful methods that we should know, in order to make them even more useful in our code. This lesson illustrates the main methods that we'll use:

* `keys`
* `values`
* `items`

### Documentation For This Video

- [Dictionary Methods](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict)

## Dictionary Methods

When we're working with dictionaries, we often need to perform actions on all of the keys, all of the values, or each pair (item). Thankfully the keys, values, and items methods each return something to make this easier. Let's take a look at the key method first:

```mcd
>>> ages = {'kevin': 61, 'bob': 79}
>>> ages.keys()
dict_keys(['kevin', 'bob'])
```

Take notice of the return value, it's a dict_keys item. This by itself may not seem useful, but it can be cast to a list if that type makes more sense for what we're doing:

```cmd
>>> list(ages.keys())
['kevin', 'bob']
```

We'll also follow this pattern for both values and items:

```cmd
>>> ages.values()
dict_values([61, 79])
>>> list(ages.values())
[61, 79]
>>> ages.items()
dict_items([('kevin', 61), ('bob', 79)])
>>> list(ages.items())
[('kevin', 61), ('bob', 79)]
```

Because each item in a dictionary is a key and value, the result of items (when typecast to a list) is a list of 2-tuples (often called "pairs"). This is a good example of using a tuple, because we know these items will always be two items long.

As we learn about iterating, these methods will become incredibly valuable for doing useful things with dictionaries.


{% include links.html %}
