---
title: 42. The `if` Operator
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: pyth_42.html
folder: python3
---

The PCAP syllabus includes the line "the if operator". This is a term only found in this syllabus. The term that should have been used was "conditional expressions". In this lesson, we'll learn what conditional expressions are and how we can use them.

### Documentation

[Conditional Expressions](https://docs.python.org/3.7/reference/expressions.html#conditional-expressions)

### What Is a Conditional Expression?

The term "conditional expression" is sometimes referred to as a "ternary expression" in other languages, but sometimes we want a single line to do one thing or another based on a condition. For example, we want to set a variable to one value if a condition is true or a different value if the condition is false. Here's what this would look like using a conditional statement:

```
if CONDITION:
    my_var = 1
else:
    my_var = 2
```
Using a conditional expression, we can do this in a single line:

```
my_var = 1 if CONDITION else 2
```

This syntax isn't restricted to variable assignment, but it is a common usage. If we wanted to print a different message based on a condition we can also do that using a conditional expression:

```
print("something") if 1 > 2 else print("something else")
```

Or if we want to simplify this further, we could let the conditional expression return the value directly to the print function:

```
print("something" if 2 > 1 else "something else")
```

{% include links.html %}
