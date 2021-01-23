---
title: 14. Generators
tags: [python]
keywords: sample
summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: python_14.html
folder: python
---

## 14.2. Generators

## Creating and Using Generators

Normal functions are the primary way that we'll be bundling up logic that we want to use over and over, but Python also provides a way for us to define functions that behave like iterators. These functions are called "generators." In this lesson, we'll learn why we might want to use generators and how to create and use them.

### Documentation 

- [Python Wiki: Generators](https://wiki.python.org/moin/Generators)
- [The Built-In next Function](https://docs.python.org/3.7/library/functions.html#next)

### What is a Generator?

A generator is a function that behaves like an iterator. This means that we can ask a generator function for its "next" value and it will calculate it, and return it to us. Similar to how a range doesn't calculate all of the values at once, a generator function essentially "pauses" its execution after returning a single result until the next result is requested.

To learn about generators, let's go ahead and implement a function that works like the built-in range type.

### Writing a Generator Function

Generator functions are defined the same way that traditional functions are, except that instead of using the return keyword to provide a result back to the caller, we use the keyword yield. When defining a generator, we will almost always include a loop in the body of the function, and then we'll yield from within the loop. Let's create a new file called gen.py to create our gen_range function.

```powershell
def gen_range(stop, start=1, step=1):
    num = start
    while num <= stop:
        yield num
        num += step
```

Unlike the built-in range function, if we call this function with three arguments, they're in the order of stop, start, and step instead of starting with start. But this function effectively works the same way (although not as performant). Let's load our file into the REPL to test out this function:

```powershell
$ python3.7 -i gen.py
>>> gen_range(10)
<generator object gen_range at 0x1054a8550>
>>>
```

The first thing to note, is that when we call the generator function, it returns a generator object to us instead of giving us the result. To get each result, we'll use the built-in next function to execute the generator until it hits a yield statement. Let's assign the generator object to a variable and pass it to next a few times:

```powershell
>>> generator = gen_range(4)
>>> next(generator)
1
>>> next(generator)
2
>>> next(generator)
3
>>>
```

This is how a generator works. It loops internally, yielding a result each time it's passed to the next function until it reaches the end of the function because it stops looping. Here's what we see if we pass the generator to next too many times:

```powershell
>>> next(generator)
4
>>> next(generator)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

In practice, we won't normally be calling the next function on our generators. We'll be using them with for loops like this:

```powershell
>>> for num in gen_range(10, step=2):
...     print(num)
...
1
3
5
7
9
>>>
```

The for loop automatically knows how to work with generators, so we don't have to worry about running into the StopIteration error.

## 14.2. Converting Generators to Lists

Generators are functions that behave like iterators, and that means that they can be used to dynamically calculate items in a loop. But that also means that they can be converted into lists. In this lesson, we'll take a look when and how we can convert a generator into a list.

### Documentation 

- [Python Wiki: Generators](https://wiki.python.org/moin/Generators)
- [The Built-In next Function](https://docs.python.org/3.7/library/functions.html#next)

### Converting a Generator to a List

When we're working with generators, we'll often write them in such a way that eventually they won't have anything left to yield. And in that case, we can turn the generator into a list. This might sound like it would be difficult, but it's as easy as passing the generator object into the list function that we've used many times before, to convert things like dict_keys objects to be lists.

Let's load our gen.py file into the REPL again so that we can utilize the gen_range function that we wrote in the previous lecture:

```powershell
$ python3.7 -i gen.py
>>> generator = gen_range(10)
>>> list(generator)
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

That was pretty simple. But, it is possible to run into issues with this. Let's say that we define an infinite generator that will always calculate the next item in the Fibonacci sequence we looked at in our recursion lesson.

```powershell
gen.py

def gen_range(stop, start=1, step=1):
    num = start
    while num <= stop:
        yield num
        num += step

def gen_fib():
    a, b = 0, 1
    while True:
        a, b = b, a + b
        yield a
```

This function might look a little weird, but to calculate the next item in the Fibonacci sequence, we combine the previous two items with 0 and 1 being our two starting points. This should yield us 1, 1, 2, 3, 5, 8, etc. as we continue to call next on an instance of this generator object:

```powershell
$ python3.7 -i gen.py
>>> fib = gen_fib()
>>> next(fib)
1
>>> next(fib)
1
>>> next(fib)
2
>>> next(fib)
3
>>> next(fib)
5
```

We'll never reach the end of this generator function because it includes an infinite loop, and we never use a break statement. Let's see what happens if we try to turn this into a list (don't follow along with this):

```powershell
>>> list(fib)
```

We'll see that the prompt hangs. That's because it's looping forever. This is the situation when you can't convert a generator to be a list because the list function will never return.
