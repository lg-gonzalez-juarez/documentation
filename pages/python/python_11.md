---
title: Conditionals
tags: [python]
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: python_11.html
folder: python
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

## Handling Multiple Cases with `elif`

Being able to perform one thing or another based on a condition is useful. But there are many situations where we want to check multiple possible conditions, and have more than two possible branches. In this lesson, we'll learn about how we can use the elif statement to have multiple branching paths in our conditionals.

### Documentation For This Video

-[The if, elif, and else Statements](https://docs.python.org/3/tutorial/controlflow.html#if-statements)

### The elif Statement

When we want our programs to have more than two possible outputs, then the elif statement will work perfectly for us. The elif statement looks a lot like the if statement:

```cmd
if CONDITION:
   # do something
elif CONDITION_2:
   # do a different thing
else:
   # do something if all conditions are False
```

We can chain as many elif statements together as we need, so the number of cases that we can handle is effectively limitless. Let's put elif to use by creating a script to evaluate the length of a name provided when we run the script:

```
learning-conditionals.py

name = input("What is your name? ")
if len(name) >= 6:
   print("Your name is long.")
elif len(name) == 5:
   print("Your name is 5 characters.")
elif len(name) >= 4:
   print("Your name is 4 or more characters.")
else:
   print("Your name is short.")
```

When we run this, we can see the various results:

```
$ python3.7 learning-conditionals.py
What is your name? Keith
Your name is 5 characters.
$ python3.7 learning-conditionals.py
What is your name? Alex
Your name is 4 or more characters.
$ python3.7 learning-conditionals.py
What is your name? Alex
Your name is 4 or more characters.
$ python3.7 learning-conditionals.py
What is your name? Bob
Your name is short.
$ python3.7 learning-conditionals.py
What is your name? Cynthia
Your name is long.
```

Notice that we fell into the first elif statement's block, and then the second elif block was never executed even though it was true. We can only exercise one branch in an if statement.

## Utilizing `pass`

Occasionally, we want to add a branch or other code block without providing any useful code in the block. This is a useful approach if we're outlining some code. In this lesson, we'll learn how to achieve this by using the pass statement.

### Documentation For This Video

[The pass Statement](https://docs.python.org/3/reference/simple_stmts.html?highlight=pass#the-pass-statement)

### The pass Statement

When we're first working through a conditional, it's good to handle all cases, even if we don't have an else case that we'd like to run. This is good practice, just to ensure that we're thinking about the whole problem. We can remove it later.

To add an else statement without a body, we'll place a pass statement within. The pass statement is what is known as a null operation. Absolutely nothing happens when we execute a pass statement, but they are useful as a code placeholder:

```cmd
>>> name = "Keith"
>>> if name == "Kevin":
...     print("Hello Kevin")
... else:
...     pass
...
>>>
```

There are other types of code contexts with Python such as functions, classes, and loops. In all of these, we're able to leverage pass if we want to create the context and not do anything.


{% include links.html %}
