---
title: 09. Dictionaries
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: python_09.html
folder: python
---


## 9.1. Dictionaries

Learn how to use dictionaries (the dict type) to hold onto key/value information in Python.

### Documentation 

[Dictionaries](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict)


### Dictionaries

Dictionaries are the main mapping type that we'll use in Python. This object is comparable to a Hash or "associative array" in other languages.

Things to note about dictionaries:

1. Unlike Python 2 dictionaries, Python 3.7 keys are ordered in dictionaries. We will need OrderedDict if we want this to work on another version of Python.
2. You can set the key to any IMMUTABLE TYPE (no lists).
3. Avoid using things other than simple objects as keys.
4. Each key can only have one value (so we don't have duplicates when creating with dict).
We create dictionary literals by using curly braces ({ and }), separating keys from values using colons (:), and separating key/value pairs using commas (,). Here's an example dictionary:

```powershell
>>> ages = { 'kevin': 59, 'alex': 29, 'bob': 40 }
>>> ages
{'kevin': 59, 'alex': 29, 'bob': 40}
```

We can read a value from a dictionary by subscripting using the key:

```powershell
>>> ages['kevin']
59
>>> ages['billy']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'billy'
```

Keys can be added or changed using subscripting and assignment:

```powershell
>>> ages['kayla'] = 21
>>> ages
{'kevin': 59, 'alex': 29, 'bob': 40, 'kayla': 21}
```

Items can be removed from a dictionary using the del statement:

```powershell
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

```powershell
>>> ages = {'kevin': 59, 'bob': 40}
>>> 'kevin' in ages
True
>>> 59 in ages
False
Alternative Ways to Create a dict Using Keyword Arguments
```

There are a few other ways to create dictionaries that we might see, which are those using the dict constructor with key/value arguments and a list of tuples:

```powershell
>>> weights = dict(kevin=160, bob=240, kayla=135)
>>> weights
{'kevin': 160, 'bob': 240, 'kayla': 135}
>>> colors = dict([('kevin', 'blue'), ('bob', 'green'), ('kayla', 'red')])
>>> colors
{'kevin': 'blue', 'bob': 'green', 'kayla': 'red'}
```

## 9.2. Dictionary Methods

The `dict` type has plenty of useful methods that we should know, in order to make them even more useful in our code. This lesson illustrates the main methods that we'll use:

* `keys`
* `values`
* `items`

### Documentation 

- [Dictionary Methods](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict)

### Dictionary Methods

When we're working with dictionaries, we often need to perform actions on all of the keys, all of the values, or each pair (item). Thankfully the keys, values, and items methods each return something to make this easier. Let's take a look at the key method first:

```powershell
>>> ages = {'kevin': 61, 'bob': 79}
>>> ages.keys()
dict_keys(['kevin', 'bob'])
```

Take notice of the return value, it's a dict_keys item. This by itself may not seem useful, but it can be cast to a list if that type makes more sense for what we're doing:

```powershell
>>> list(ages.keys())
['kevin', 'bob']
```

We'll also follow this pattern for both values and items:

```powershell
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
