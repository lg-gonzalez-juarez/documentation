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


{% include links.html %}
