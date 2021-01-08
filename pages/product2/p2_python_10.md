---
title: Conditionals
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: p2_python10.html
# simple_map: true
# map_name: usermap
# box_number: 5
folder: product2
---

## The `if` and `else` Statements

Up to this point, all of the code that we've written will always execute sequentially regardless of the inputs that we provide (assuming that we don't cause an error). In this lesson, we're going to learn about conditionals. Conditionals allow us to add branching logic to our code, and take different actions based on conditions.

### Documentation For This Video

- [The if and else Statements](https://docs.python.org/3/tutorial/controlflow.html#if-statements)

### The if and else Statements

With a grasp on comparisons, we can now look at how to use conditionals to run different pieces of logic based on values. The main keywords for conditionals in Python are if and else. Conditionals are the first language feature we're using that require us to utilize whitespace to separate our code blocks. We will always use 4 spaces as indentation. The basic shape of an if statement is this:

```
if CONDITION:
    print("CONDITION was True")
```

The CONDITION portion can be anything that evaluates to True or False, and if the value isn't explicitly a boolean then it will be implicitly converted to determine how to proceed past the conditional (essentially wrapping the CONDITION with the bool constructor):

```
>>> if True:
...     print("Was True")
...
Was True
>>> if False:
...     print("Was True")
...
>>>
```
To add an alternative code path, we'll use the else keyword, followed by a colon (:), and indent the code underneath:

```
>>> if False:
...     print("Was True")
... else:
...     print("Was False")
...
Was False
```

{% include links.html %}
