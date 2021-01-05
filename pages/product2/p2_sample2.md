---
title: Literals, variables, and comments
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: p2_sample2.html
simple_map: true
map_name: usermap
box_number: 2
folder: product2
---

## Comments

When writing scripts, we often want to leave ourselves notes or explanations. Python (along with most scripting languages) uses the # character to signify that the line should be ignored and not executed.

### Single Line Comment
We can comment out a whole line:

```python
# This is a full line comment
```
or we can comment at the end of a line:

```python
2 + 2 # This will add the numbers
```
### What About Block Comments?
Python does not have the concept of block commenting that you may have encountered in other languages. Many people mistake a triple quoted string as being a comment, but it is not. It's a multi-line string. That being said, multi-line strings can functionally work like comments, but they will still be allocated into memory.

```
"""
This is not a block comment,
but it will still work when you need
for some lines of code to not execute.
"""
```

## Variables and the Assignment Operator

Almost any script that we write will need to provide a way for us to hold onto information for use later on. That's where variables come into play.

### Working with Variables
We can assign a value to a variable by using a single `=` and we don't need to (nor can we) specify the type of the variable.

```cmd
>>> my_str = "This is a simple string"
```

Now we can print the value of that string by using `my_var` later on:

```cmd
>>> print(my_str)
This is a simple string
```

We can also change the value that is assigned to a variable later on, either by using the standard assignment operator = or by using some of the short-hand operators that we'll learn about as we continue.

```cmd
>>> my_str += " testing"
>>> my_str
'This is a simple string testing'
```

An important thing to realize is that the contents of a variable can be changed and we don't need to maintain the same type:

```cmd
>>> my_str = 1
>>> print(my_str)
1
```
Ideally, we wouldn't change the contents of a variable called `my_str` to be an interger, but it is something that Python will allow us do.

One last thing to remember is that, if we assign a variable with another variable, it will be assigned to the initial result of the variable and not whatever that variable points to later.

```cmd
>>> my_str = 1
>>> my_int = my_str
>>> my_str = "testing"
>>> print(my_int)
1
>>> print(my_str)
testing
```

### Short-Hand Assignment Operators

There are numerous shorthand assignment operators we can use that allow us to perform operations and also assign back to variables in the way that we did with the `+=` operator. The form for these shorthand assignment operations always follows the same pattern. We'll take the operator that we want to use, say `+`, and create a new operator by adding `=` to the right-hand side of it. So, for the subtraction operation, we could subtract from the current value and assign the new value to a variable using the `-=` operator.

As we learn about more and more operators we'll be able to follow this pattern if we want to reassess our current variable based on an operation.


{% include links.html %}
