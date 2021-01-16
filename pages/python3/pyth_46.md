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

When it comes to exceptions most of the time we'll be using exception handling, but sometimes we want to raise an exception from our code and then expect the code using our code to handle the exceptions that we might potentially raise.

### Documentation 
- [Python Errors and Exceptions Documentation](https://docs.python.org/3.7/tutorial/errors.html)
- [Python Exceptions Documentation](https://docs.python.org/3/library/exceptions.html)

### Creating an Exception

To trigger an exception in Python code we need to utilize another keyword: `raise`. We refer to this as "raising an exception". Before we can raise an exception though, we need to create an exception, but thankfully exceptions are objects just like everything else. Hoping into the REPL, let's create our first exception:

```
$ python3.7
>>> err = Exception('something went wrong')
>>> err
Exception('something went wrong')
>>> str(err)
'something went wrong'
>>> dir(err)
['__cause__', '__class__', '__context__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__get
attribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__ne__', '__new__', '__reduce__', '__redu
ce_ex__', '__repr__', '__setattr__', '__setstate__', '__sizeof__', '__str__', '__subclasshook__', '__suppress_context__', '__traceb
ack__', 'args', 'with_traceback']
```

Notice that just creating an exception doesn't stop excecution. The `Exception` class is the parent class for most exceptions, and we can see these by using `Exception.__subclasses__()`:

```
>>> Exception.__subclasses__()
[<class 'TypeError'>, <class 'StopAsyncIteration'>, <class 'StopIteration'>, <class 'ImportError'>, <class 'OSError'>, <class 'EOFError'>, <class 'RuntimeError'>, <class 'NameError'>, <class 'AttributeError'>, <class 'SyntaxError'>, <class 'LookupError'>, <class 'ValueError'>, <class 'AssertionError'>, <class 'ArithmeticError'>, <class 'SystemError'>, <class 'ReferenceError'>, <class 'MemoryError'>, <class 'BufferError'>, <class 'Warning'>, <class 'locale.Error'>, <class 're.error'>, <class 'sre_parse.Verbose'>]
```

Let's dig a little deeper into the inheritance struction here:

```
>>> Exception.__bases__
(<class 'BaseException'>,)
>>> BaseException.__bases__
(<class 'object'>,)
>>> BaseException.__subclasses__()
[<class 'Exception'>, <class 'GeneratorExit'>, <class 'SystemExit'>, <class 'KeyboardInterrupt'>]
```

Since `BaseException` only inherits from `object` it is essentially the parent of all errors, but we really won't ever use it.

### Raising an Exception

Now that we know how to create an exception, let's go ahead and create and raise an exception from a new script called `using_exceptions.py`:

`~/exception_handling/using_exceptions.py`

```
import sys

if len(sys.argv) < 2:
    raise Exception('not enough arguments')

name = sys.argv[1]
print(f"Name is {name}")
```

Now, if we run into the situation where not enough arguments are provided when the script is run we can create and raise an exception with the message that we want. This puts us back to having a not great user experience for our script, but it's great for showcasing how to use exceptions.

Let's put this to the test:

```
$ python3.7 using_exceptions.py
Traceback (most recent call last):
  File "using_exceptions.py", line 4, in <module>
    raise Exception("not enough arguments")
Exception: not enough arguments
$ python3.7 using_exceptions.py Keith
Name is Keith
```

## 46.4. Creating Custom Exception Types

Specific error types make it easier to tailor exception handling to handle different potential error cases, and sometimes we want to build something that could benefit from having a more detailed error type that doesn't exist.

In this lesson, we'll learn how to create custom exception types.

### Documentation 

- [Python Errors and Exceptions Tutorial](https://docs.python.org/3.7/tutorial/errors.html)
- [Python Exceptions Documentation](https://docs.python.org/3/library/exceptions.html)

### Creating a Custom Exception Type

Custom exception types are things that we'll use more often when we're building larger libraries that have different types of contextual errors. These custom exceptions can be caught by the code using our modules so that they only catch our exception and not more generic exceptions. We won't be creating a large library to showcase custom exceptions, but we can create a simple package that has an `errors` module, and then we can raise those errors in the code provided by our package. To begin, let's create a package called `cli`:

```
$ mkdir cli
$ touch cli/__init__.py
$ touch cli/errors.py
```

To follow what we've been doing around exceptions related to script arguments, let's create an `ArgumentError` class in our `errors` module:

`~/exception_handling/cli/errors.py`

```
class ArgumentError(Exception):
    pass
```

That's it! Now we have an identifier for our custom exception scenario, but exceptions all need to do the same things, and the `Exception` class defines all of that. Let's create a `main` function in our package's `__init__.py` file, and we can run that function from a new script.

`~/exception_handling/cli/__init__.py`

```
import sys

from .errors import ArgumentError

def main():
    if len(sys.argv) < 2:
        raise ArgumentError('too few arguments')
    print(f"Name is {sys.argv[1]}")
```

From `using_exceptions.py`, let's import our `main` function and use exception handling to catch our new `ArgumentError`:

`~/exception_handling/using_exceptions.py`

```
import sys

from cli import main
from cli.errors import ArgumentError

try:
    main()
except ArgumentError as err:
    print(f"Error: {err}")
    sys.exit(1)
```

Finally, let's run `using_exceptions.py` a few more times:

```
$ python3.7 using_exceptions.py
Error: too few arguments
$ python3.7 using_exceptions.py Keith
Name is Keith
```

## 46.5. Using Assertions


When we've raised exceptions to this point, we've done so because some criteria wasn't met. When developing and debugging code, this is something that can be done using the built-in `assert` keyword, and in this lesson, we'll give that a try.

### Documentation 
- [Python Errors and Exceptions Tutorial](https://docs.python.org/3.7/tutorial/errors.html)
- [Python Exceptions Documentation](https://docs.python.org/3/library/exceptions.html)
- [The assert statement](https://docs.python.org/3/reference/simple_stmts.html#assert)
- [The -O Python Flag](https://docs.python.org/3/using/cmdline.html#cmdoption-o)

### What is an Assertion?

Assertions are statements that raise an `AssertionError` if the passed in expression returns a `False` value (or something that would convert to `False` via the `bool` constructor). This is what we've been doing when we use code like this:

```
if len(sys.argv) < 2:
    raise ArgumentError('too few arguments')
```

We can achieve this same thing using an `assert` statement, except it will raise an `AssertionError` instead of our custom `ArgumentError`. Here's what this would look like in our `main` function in the `cli/__init__.py` file:

`~/exception_handling/cli/__init__.py`

```
import sys

from .errors import ArgumentError

def main():
    # if len(sys.argv) < 2:
    #     raise ArgumentError("too few arguments")
    assert len(sys.argv) >= 2, "too few arguments"
    print(f"Name is {sys.argv[1]}")
```

We will need to change our `using_exceptions.py` file to except the `AssertionError` type to not break our program:

`~/exception_handling/using_exceptions.py`

```
import sys

from cli import main
from cli.errors import ArgumentError

try:
    main()
except (ArgumentError, AssertionError) as err:
    print(f"Error: {err}")
    sys.exit(1)
Let's run our script once again:

$ python3.7 using_exceptions.py
Error: too few arguments
$ python3.7 using_exceptions.py Keith
Name is Keith
```

### Assertion is a debugging Tool

This isn't a great use of `assert` because assertions are a tool specifically designed for developing and debugging code. The Python parser can remove `assert` statements when our script is run with the `-O` or `-OO` flags (capital 'o' for "optimize").

```
$ python3.7 using_exceptions.py
Error: too few arguments
$ python3.7 -O using_exceptions.py
Traceback (most recent call last):
  File "using_exceptions.py", line 4, in <module>
    main()
  File "/home/cloud_user/exception_handling/cli/__init__.py", line 10, in main
    print(f"Name is {sys.argv[1]}")
IndexError: list index out of range
```

When we use the `-O` or `-OO` flags, we optimize our code to remove assertions (and docstrings with `-OO`), so we can't reliably use asserts to determine if we're going to raise errors.

{% include links.html %}
