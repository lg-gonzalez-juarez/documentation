---
title: 06. Strings, Operations, and Calculations
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: python_06.html
folder: python
---

## 6.1. Understanding Immutability

As we start digging into sequence types like strings, lists, tuples, and dictionaries, we need to start thinking about the mutability of a type or whether or not it can change. Normally, we'll talk about whether or not a type is "immutable," meaning that it can't be changed, and most of the types we've looked at thus far are immutable.

### Documentation 

[Immutable Sequences](https://docs.python.org/3/library/stdtypes.html#immutable-sequence-types)

### Why Does Immutability Matter?

Immutability is something that we don't always have to think about, but it does matter in a few very common cases:

### Understanding why we can't modify a string in-place

Using objects as keys for dictionaries (we'll get to this later)
We'll cover dictionaries in a different section, but when it comes to strings, wanting to modify a string variable is fairly common. Strings are an immutable type in Python, so we can't change a string object. We can only create new strings with the modifications that we wanted. This means that the only way for us to change the string value of a variable is to explicitly reassign it. As we learn about mutable types, we'll see that other types allow us to modify the value of a variable without explicitly reassigning it.

### Immutability of Strings

When looking at str class there are many methods that return a str to us, such as capitalize:

```powershell
>>> my_str = 'testing'
>>> my_str.capitalize()
'Testing'
>>> my_str
'testing'
```

We won't find a method that changes the value of my_str in this example. Beyond this, each unique string that we can only type will only exist once in memory. In our case, we referenced the literal 'testing' when we assigned the value to our variable, and if we ever use the literal of 'testing' again it will point to the same point in memory, because that value can't be modified.

```powershell
>>> id(my_str)
4522355248
>>> id('testing')
4522355248
```

This feature prevents the same value being allocated more than once and taking up more spots in our computer's memory than we need it to.

## 6.2. The `len` Function

In this short lesson, we're going to take a look at a built-in function that will help us see how long any sequence or collection type is, including strings: the len function.

### Documentation 

[The len function](https://docs.python.org/3/library/functions.html#len)

### The len Function

Needing to know the length of a string is very common. Thankfully, the len function will return how many characters are in a string:

```powershell
>>> len('testing')
7
>>> len('')
0
```

This may seem a little boring, but it will help us to keep from causing too many errors when we start learning about indexing and slicing in the next lesson.

## 6.3. String Indexing and Slicing

Sometimes we need to access a specific item, or a subset of items, in a sequence. To do that in Python, we'll use indexing and slicing.

### Documentation 

[Text Sequence Type str](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str)

### Indexing

When we need to access a single item from a sequence, like a string, we'll use "indexing." Every item in a sequence type has an index that indicates the item's position in the sequence. The first item in a Python sequence has the index of 0, and each subsequent item's index increases by one. To perform indexing, we'll use square brackets ([ and ]) on the right-hand side of our string (or string variable), and within the square brackets we'll put the index number that we'd like to access:

```powershell 
>>> test_str = 'testing'
>>> test_str[0]
't'
```

There isn't a character type in Python, so the return value will be a length one string. When indexing a string, the index must exist, otherwise, Python will raise an error:

```powershell
>>> test_str[10]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
```

This is one of the areas where using len can help us avoid using an index that is too high. But since the starting index is 0, then the final index will always be len(test_str) - 1:

```powershell
>>> test_str[len(test_str) - 1]
'g'
```

If we try to use a negative index, it will actually start giving us items relative to the end of the string:

```powershell
>>> test_str[-1]
'g'
>>> test_str[-4]
't'
>>> test_str[-8]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
```

### Slicing

If we want to get a subsection of our string then we'll do what is called slicing. Slicing allows us to specify the index of the first element that we would like, followed by the index just beyond the last item that we'd like. We separate these indexes by using a colon (:)

```powershell
>>> test_str[0:2]
'te'
>>> test_str[3:5]
'ti'
```

If we'd like to get all of the items after our starting index then we can use the length of the string as our second index, even though it's technically out of range. Or we can simply put nothing after the colon:

```powershell
>>> test_str[2:len(test_str)]
'sting'
>>> test_str[2:]
'sting'
```

The last thing to mention about slicing is that there is a third number that we can use: the "step" value. By default, this value is 1 and just means that we'll go one-by-one through the sequence. But we can change this to grab every other item if we'd like by adding a second colon and the step size that we'd like to use:

```powershell
>>> test_str
'testing'
>>> test_str[1:5:2]
'et'
>>> test_str[1::2]
'etn'
```

One neat thing that we can do with this step option is stepping backward by using a negative step value. We can reverse an entire string by leaving off the start and end indexes and setting the step value to -1:

```powershell
>>> test_str[::-1]
'gnitset'
```
