---
title: 13. Function Basics, Generators and Scoping
tags: [python]
keywords: sample
summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: python_13.html
folder: python
---

## 13.1. Function Basics

### Defining and Using Functions

Being able to write code that we can call multiple times without repeating ourselves is one of the most powerful things that we can do when programming. Let's learn how to define functions in Python.

### Documentation 

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

```powershell
>>> def hello_world():
...     print("Hello, World!")
...
>>> hello_world()
Hello, World!
>>>
```

If we want to define a parameter, we will put the variable name we want it to have within the parentheses:

```powershell
>>> def print_name(name):
...     print(f"Name is {name}")
...
>>> print_name("Keith")
Name is Keith
```

Let's try to assign the value from print_name to a variable called output:

```powershell
>>> output = print_name("Keith")
Name is Keith
>>> output
>>>
```

Neither of these examples has a return value, but we will usually want to have a return value unless the function is our "main" function or carries out a "side-effect" like printing. If we don't explicitly declare a return value, then the result will be None (as you saw when our body used print).

We can declare what we're returning from a function using the return keyword:

```powershell
>>> def add_two(num):
...     return num + 2
...
>>> result = add_two(2)
>>> result
4
```
### Working with Multiple Parameters

When we have a function that takes multiple parameters, we need to separate them using commas and give them unique names:

```powershell
>>> def add(num1, num2):
...     return num1 + num2
...
>>> result = add(1, 5)
>>> result
6
```

## 13.2. Parameters vs. Arguments

When talking about functions, the words "parameter" and "argument" are often used interchangeably. But they represent two different things. In this lesson, we'll look at the differences between parameters and arguments, and the different ways we can use arguments when calling functions.

### Documentation 

[Defining Functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)

### Parameters VS Aruguments

The difference between a parameter and an argument is all about timing. When we're working with the definition of a function, then the variables defined in the function declaration are the "parameters." When we're calling the function, the data that we provide for each parameter is the "argument." Accidentally using these words interchangeably in practice isn't an issue, because other programmers will know exactly what you're talking about. But it is good to know that there is a distinction.

With the semantic differences covered, we're ready to move onto the more interesting topic of the various types of arguments that we can use: position and keyword arguments.

### Using Keyword Arguments

Every function call we've made up to this point has used what are known as positional arguments. But if we know the name of the parameters, and not necessarily the positions, we can all them all using keyword arguments like so:

```powershell
>>> def contact_card(name, age, car_model):
...     return f"{name} is {age} and drives a {car_model}"
...
>>> contact_card("Keith", 29, "Honda Civic")
'Keith is 29 and drives a Honda Civic'
>>> contact_card(age=29, car_model="Civic", name="Keith")
'Keith is 29 and drives a Civic'
>>> contact_card("Keith", car_model="Civic", age="29")
'Keith is 29 and drives a Civic'
>>> contact_card(age="29", "Keith", car_model="Civic")
  File "<stdin>", line 1
SyntaxError: positional argument follows keyword argument
```

When we're using position and keyword arguments, every argument after the first keyword argument must also be a keyword argument. It's sometimes useful to mix them, but oftentimes we'll use either all positional or all keyword.

### Defining Parameters with Default Arguments

Along with being able to use keyword arguments when we're calling a function, we're able to define default values for parameters to make them optional when the information is commonly known and the same. To do this, we use the assignment operator (=) when we're defining the parameter:

```powershell
>>> def can_drive(age, driving_age=16):
...     return age >= driving_age
...
>>> can_drive(16)
True
>>> can_drive(16, driving_age=18)
False
```

Parameters with default arguments need to go at the end of the parameters list when defining the function so that positional arguments can still be used to call the function.

## 13.3. Recursion

It might not seem immediately obvious, but we're capable of calling a function from within itself. This practice is called recursion. In this lesson, we'll learn how we can use recursion and some of the pitfalls that surround it.

### Documentation 

- [Defining Functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)
- [The sys.getrecursionlimit Function](https://docs.python.org/3.7/library/sys.html#sys.getrecursionlimit)

### Solving Problems with Recursion

Recursion is the practice of calling a function from within itself. This might not seem like something that you'd ever do at first, but occasionally the best way to solve a problem is to break it up into smaller versions of the same problem. The canonical example of this is calculating the Fibonacci Sequence (1, 1, 2, 3, 5, 8, etc.). In the Fibonacci sequence, the next number is always the sum of the previous two numbers in the sequence. If we write this out as a mathematical function, then calculating the nth item in the Fibonacci sequence would look something like this:

```powershell
f(n) = f(n-2) + f(n-1)
```

So, for the 5th item in the sequence (which coincidently is also 5), we would expand it like this:

```powershell
f(5) = f(3) + f(4)
f(5) = f(1) + f(2) + f(2) + f(3)
f(5) = 1 + f(0) + f(1) + f(0) + f(1) + f(1) + f(2)
f(5) = 1 + 0 + 1 + 0 + 1 + 1 + f(0) + f(1)
f(5) = 1 + 0 + 1 + 0 + 1 + 1 + 0 + 1
f(5) = 5
```

For recursion to work, there has to be what is called a "base case," where something is returned other than the result of the function calling itself. In the case of our Fibonacci sequence function, the base case(s) are that f(0) will return 0, and f(1) will return 1. Now that we can visualize exactly what is going on, let's write this function in Python:

```powershell
~/fib.py

def fib(n):
    if n == 0:
        return 0
    elif n == 1:
        return 1

    return fib(n - 2) + fib(n - 1)

item_to_calculate = int(input("What Fibonnaci item would you like to calculate? "))

print(fib(item_to_calculate))
```

In writing our function, we needed to remember a few things:

1. We need to handle the base cases first.
2. We return what we would normally consider the implementation of the function. This return allows us to essentially gather all of the results at the end.

Let's run our script:

```powershell
$ python3.7 fib.py
What Fibonacci item would you like to calculate? 15
610
```

That was pretty fast, but as we increase the number from 15 to 30, we should see it take significantly longer to return. This is because the number of recursive function calls that happen as we try to calculate higher and higher terms gets excessively large. Trying to calculate the 50th term using our implementation might not ever return.

### The Limits of Recursion

We've run into the main issue with recursion, every time we recurse it, we're adding more and more function calls to the stack of calls that need to be completed. Some languages are optimized to handle this by implementing something called "tail-call optimization," but Python is not one of those languages. Recursion is a useful tool at times, but it does require being delicate and layering in some manual optimization (which we won't be covering here).

