---
title: Strings, Operations, and Calculations
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: p2_python6.html
# simple_map: false
# map_name: usermap
# box_number: 1
folder: product2
---

## Understanding Immutability

As we start digging into sequence types like strings, lists, tuples, and dictionaries, we need to start thinking about the mutability of a type or whether or not it can change. Normally, we'll talk about whether or not a type is "immutable," meaning that it can't be changed, and most of the types we've looked at thus far are immutable.

### Documentation For This Video

[Immutable Sequences](https://docs.python.org/3/library/stdtypes.html#immutable-sequence-types)

### Why Does Immutability Matter?

Immutability is something that we don't always have to think about, but it does matter in a few very common cases:

### Understanding why we can't modify a string in-place

Using objects as keys for dictionaries (we'll get to this later)
We'll cover dictionaries in a different section, but when it comes to strings, wanting to modify a string variable is fairly common. Strings are an immutable type in Python, so we can't change a string object. We can only create new strings with the modifications that we wanted. This means that the only way for us to change the string value of a variable is to explicitly reassign it. As we learn about mutable types, we'll see that other types allow us to modify the value of a variable without explicitly reassigning it.

### Immutability of Strings

When looking at str class there are many methods that return a str to us, such as capitalize:

```cmd
>>> my_str = 'testing'
>>> my_str.capitalize()
'Testing'
>>> my_str
'testing'
```
We won't find a method that changes the value of my_str in this example. Beyond this, each unique string that we can only type will only exist once in memory. In our case, we referenced the literal 'testing' when we assigned the value to our variable, and if we ever use the literal of 'testing' again it will point to the same point in memory, because that value can't be modified.

```cmd
>>> id(my_str)
4522355248
>>> id('testing')
4522355248
```
This feature prevents the same value being allocated more than once and taking up more spots in our computer's memory than we need it to.


{% include links.html %}
