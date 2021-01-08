---
title: Function Basics, Generators and Scoping
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: p2_python12.html
# simple_map: true
# map_name: usermap
# box_number: 5
folder: product2
---

## Function Basics

### Defining and Using Functions

Being able to write code that we can call multiple times without repeating ourselves is one of the most powerful things that we can do when programming. Let's learn how to define functions in Python.

### Documentation For This Video

[Defining Functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)

### Function Basics

We can create functions in Python using the following:

- The def keyword
- The function name - lowercase starting with a letter or underscore (_)
- Left parenthesis (()
- 0 or more parameter names
- Right parenthesis ())
- A colon :
- An indented function body

Here's an example without any parameters:

```
>>> def hello_world():
...     print("Hello, World!")
...
>>> hello_world()
Hello, World!
>>>
```

If we want to define a parameter, we will put the variable name we want it to have within the parentheses:

```
>>> def print_name(name):
...     print(f"Name is {name}")
...
>>> print_name("Keith")
Name is Keith
```

Let's try to assign the value from print_name to a variable called output:

```
>>> output = print_name("Keith")
Name is Keith
>>> output
>>>
```

Neither of these examples has a return value, but we will usually want to have a return value unless the function is our "main" function or carries out a "side-effect" like printing. If we don't explicitly declare a return value, then the result will be None (as you saw when our body used print).

We can declare what we're returning from a function using the return keyword:

```
>>> def add_two(num):
...     return num + 2
...
>>> result = add_two(2)
>>> result
4
```
### Working with Multiple Parameters

When we have a function that takes multiple parameters, we need to separate them using commas and give them unique names:

```
>>> def add(num1, num2):
...     return num1 + num2
...
>>> result = add(1, 5)
>>> result
6
```



{% include links.html %}
