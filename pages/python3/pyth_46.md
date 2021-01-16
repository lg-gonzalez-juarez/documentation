---
title: 46. Exceptions and Exception Handling
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: pyth_46.html
folder: python3
---


## 46.1. What are Exceptions?

Things don't always go according to plan when we're programming, and when issues arise, we run into exceptions. In this lesson, we'll learn about what exceptions are and when we'll run into them.

### Documentation
- [Python Errors and Exceptions Documentation](https://docs.python.org/3.7/tutorial/errors.html)
 -[Python Exceptions Documentation](https://docs.python.org/3/library/exceptions.html)

### Syntax Errors vs Exceptions

As we've been learning how to do various things with Python, we've run into both syntax errors and exceptions. There's a subtle difference between the two: syntax errors cannot be recovered from. The reason that we can't recover from a syntax error is that our code is simply not valid Python code, so the parser doesn't know what to do with anything after it runs into the error.

Exceptions are issues that occur during the execution of syntactically valid code that prevents the code from executing as planned. An exception occurring doesn't necessarily mean that our program needs to fail; it might just mean that we need to do something differently.

An example of an exception that we can handle is a `TypeError`. This type of exception that we would run into if we tried to add an `int` and a `str` like this:

```
>>> 1 + 'a'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

This might seem like something that we would never do, but say we had code that tried to add two different variables, without using type checking or type casting we can't know for certain that two random variables both hold onto types that can be added, so it is possible to run into a `TypeError` in that situation.

As we write more and more complex code, there will be times when we need to handle errors, raise errors ourselves, and even create custom error types.

## 46.2. Handling Exceptions with `try`, `except`, `else`, and `finally`

Not everything can go according to plan in our programs, but we should know when these scenarios arise and handle them appropriately. In this lesson, we'll take a look at how to handle exceptions in Python.

### Documentation 

- [The try statement & workflow](https://docs.python.org/3/reference/compound_stmts.html#the-try-statement)
- [Python Errors and Exceptions Documentation](https://docs.python.org/3/reference/compound_stmts.html#the-try-statement)
- [Python Exceptions Documentation](https://docs.python.org/3/library/exceptions.html)

### Handling Exceptions with try/except/else/finally

When we know that our code can raise an exception, we don't need to just accept it and let our program crash. We can handle these exceptions using the [try statement](https://docs.python.org/3/reference/compound_stmts.html#the-try-statement). This is a compound statement kind of like the `if` statement where we will also need to use `except`, and have access to `else` and `finally`. Let's break down what these do by writing a small program that will potentially raise an exception. We'll call this program `using_try.py` and put it in a new directory called `exception_handling`:

```
$ ~/exception_handling
$ touch ~/exception_handling/using_try.py
```

`~/exception_handling/using_try.py`

```
import sys

print(f"Received argument {sys.argv[1]}")
```
If we run this script with an extra argument, then it will run successfully, but if we run it without any arguments, then we'll see an exception.

```
$ python3.7 using_try.py testing
Received argument testing
$ python3.7 using_try.py
Traceback (most recent call last):
  File "using_try.py", line 3, in <module>
    print(f"Received argument {sys.argv[1]}")
IndexError: list index out of range
```

The exception is an `IndexError`, and it's being raised because the list returned from `sys.argv` doesn't have 2 elements, so there is no index of `1`. This is a completely reasonable thing for someone to do when using our script; it is easy to forget to pass in an argument. There are ways to handle this that don't involve using exception handling, but since indexing a list can potentially raise an exception, we should be ready to perform exception handling in our code.

To handle this, we need to place our code that could raise an exception within a try statement and then `except`, if it happens and do something else.

`~/exception_handling/using_try.py`

```
import sys

try:
    print(f"Received argument {sys.argv[1]}")
except:
    print(f"Error: no arguments, please provide at least one argument")
    sys.exit(1)
```

This is the simplest kind of try/except, and this will catch any exception that might be raised by the code inside the `try` block. If we run this file again, we should see our print out.

```
$ python3.7 using_try.py
Error: no arguments, please provide at least one argument
$ echo $?
1
```

Since this is still a case where we want to terminate our script, we're going to explicitly exit with a non-zero status code to indicate the user that things didn't go according to plan, but we're also able to shield the user from seeing the Python traceback and provide a better experience to anyone using our script.

We could make this more specific and only `except` a very specific exception, and even have multiple separate `except` blocks catching different kinds of exceptions. Let's introduce another potential exception and catch the exceptions separately:

`~/exception_handling/using_try.py`

```
import sys

try:
    print(f"First argument {sys.argv[1]}")
    args = sys.argv
    random.shuffle(args)
    print(f"Random argument {args[0]}")
except IndexError as err:
    print(f"Error: no arguments, please provide at least one argument ({err})")
    sys.exit(1)
except NameError:
    print(f"Error: random module not loaded")
    sys.exit(1)
```

Let's run this without an argument and then with an argument:

```
$ python3.7 using_try.py
Error: no arguments, please provide at least one argument (list index out of range)
$ python3.7 using_try.py testing
First argument testing
Error: random module not loaded
```

Notice that like a conditional statement with multiple branches, only one of the except blocks will run because as soon as an exception occurs, the execution of the try block stops. Additionally, we can assign the exception that is raised to a variable so that we can get more information from it by adding as <identifier> to our `except` clause.

### The else and finally Statements

Now we're able to handle exceptions, but the exception handling workflow also facilitates a way for us to run code if no exception gets caught using `else`, and there's also a way to run some code after any error handling, or the `else` block, by using `finally`. Since we're using `sys.exit`, we wouldn't be able to use `finally` as is, but let's make some modifications to see how both of these work.

`~/exception_handling/using_try.py`

```
import sys
import random

try:
    print(f"First argument {sys.argv[1]}")
    args = sys.argv
    random.shuffle(args)
    print(f"Random argument {args[0]}")
except (IndexError, KeyError) as err:
    print(f"Error: no arguments, please provide at least one argument ({err})")
except NameError:
    print(f"Error: random module not loaded")
else:
    print("Else is running")
finally:
    print("Finally is running")
```

We did import `random` so that it is possible to successfully run the script. Let's give this a run to see how it goes:

```
$ python3.7 using_try.py
Error: no arguments, please provide at least one argument (list index out of range)
Finally is running
$ python3.7 using_try.py testing
First argument testing
Random argument using_try.py
Else is running
Finally is running
$
```

## 46.3. Using Built-In Exceptions


## 46.4. Creating Custom Exception Types


## 46.5. Using Assertions


{% include links.html %}
