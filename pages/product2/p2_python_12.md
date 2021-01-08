---
title: Function Basics, Generators and Scoping
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: p2_python12.html
# simple_map: true
# map_name: usermap
# box_number: 5
folder: product2
---

## Function Basics

### Defining and Using Functions

Being able to write code that we can call multiple times without repeating ourselves is one of the most powerful things that we can do when programming. Let's learn how to define functions in Python.

### Documentation For This Video

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

```
>>> def hello_world():
...     print("Hello, World!")
...
>>> hello_world()
Hello, World!
>>>
```

If we want to define a parameter, we will put the variable name we want it to have within the parentheses:

```
>>> def print_name(name):
...     print(f"Name is {name}")
...
>>> print_name("Keith")
Name is Keith
```

Let's try to assign the value from print_name to a variable called output:

```
>>> output = print_name("Keith")
Name is Keith
>>> output
>>>
```

Neither of these examples has a return value, but we will usually want to have a return value unless the function is our "main" function or carries out a "side-effect" like printing. If we don't explicitly declare a return value, then the result will be None (as you saw when our body used print).

We can declare what we're returning from a function using the return keyword:

```
>>> def add_two(num):
...     return num + 2
...
>>> result = add_two(2)
>>> result
4
```
### Working with Multiple Parameters

When we have a function that takes multiple parameters, we need to separate them using commas and give them unique names:

```
>>> def add(num1, num2):
...     return num1 + num2
...
>>> result = add(1, 5)
>>> result
6
```

## Parameters vs. Arguments

When talking about functions, the words "parameter" and "argument" are often used interchangeably. But they represent two different things. In this lesson, we'll look at the differences between parameters and arguments, and the different ways we can use arguments when calling functions.

### Documentation For This Video

[Defining Functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)

### Parameters VS Aruguments

The difference between a parameter and an argument is all about timing. When we're working with the definition of a function, then the variables defined in the function declaration are the "parameters." When we're calling the function, the data that we provide for each parameter is the "argument." Accidentally using these words interchangeably in practice isn't an issue, because other programmers will know exactly what you're talking about. But it is good to know that there is a distinction.

With the semantic differences covered, we're ready to move onto the more interesting topic of the various types of arguments that we can use: position and keyword arguments.

## Using Keyword Arguments

Every function call we've made up to this point has used what are known as positional arguments. But if we know the name of the parameters, and not necessarily the positions, we can all them all using keyword arguments like so:

```
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

```
>>> def can_drive(age, driving_age=16):
...     return age >= driving_age
...
>>> can_drive(16)
True
>>> can_drive(16, driving_age=18)
False
```

Parameters with default arguments need to go at the end of the parameters list when defining the function so that positional arguments can still be used to call the function.

## Recursion

It might not seem immediately obvious, but we're capable of calling a function from within itself. This practice is called recursion. In this lesson, we'll learn how we can use recursion and some of the pitfalls that surround it.

### Documentation For This Video

[Defining Functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)
[The sys.getrecursionlimit Function](https://docs.python.org/3.7/library/sys.html#sys.getrecursionlimit)

### Solving Problems with Recursion

Recursion is the practice of calling a function from within itself. This might not seem like something that you'd ever do at first, but occasionally the best way to solve a problem is to break it up into smaller versions of the same problem. The canonical example of this is calculating the Fibonacci Sequence (1, 1, 2, 3, 5, 8, etc.). In the Fibonacci sequence, the next number is always the sum of the previous two numbers in the sequence. If we write this out as a mathematical function, then calculating the nth item in the Fibonacci sequence would look something like this:

```
f(n) = f(n-2) + f(n-1)
```

So, for the 5th item in the sequence (which coincidently is also 5), we would expand it like this:

```
f(5) = f(3) + f(4)
f(5) = f(1) + f(2) + f(2) + f(3)
f(5) = 1 + f(0) + f(1) + f(0) + f(1) + f(1) + f(2)
f(5) = 1 + 0 + 1 + 0 + 1 + 1 + f(0) + f(1)
f(5) = 1 + 0 + 1 + 0 + 1 + 1 + 0 + 1
f(5) = 5
```

For recursion to work, there has to be what is called a "base case," where something is returned other than the result of the function calling itself. In the case of our Fibonacci sequence function, the base case(s) are that f(0) will return 0, and f(1) will return 1. Now that we can visualize exactly what is going on, let's write this function in Python:

```
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

```
$ python3.7 fib.py
What Fibonacci item would you like to calculate? 15
610
```

That was pretty fast, but as we increase the number from 15 to 30, we should see it take significantly longer to return. This is because the number of recursive function calls that happen as we try to calculate higher and higher terms gets excessively large. Trying to calculate the 50th term using our implementation might not ever return.

### The Limits of Recursion

We've run into the main issue with recursion, every time we recurse it, we're adding more and more function calls to the stack of calls that need to be completed. Some languages are optimized to handle this by implementing something called "tail-call optimization," but Python is not one of those languages. Recursion is a useful tool at times, but it does require being delicate and layering in some manual optimization (which we won't be covering here).


## Generators

## Creating and Using Generators

Normal functions are the primary way that we'll be bundling up logic that we want to use over and over, but Python also provides a way for us to define functions that behave like iterators. These functions are called "generators." In this lesson, we'll learn why we might want to use generators and how to create and use them.

### Documentation For This Video

[Python Wiki: Generators](https://wiki.python.org/moin/Generators)
[The Built-In next Function](https://docs.python.org/3.7/library/functions.html#next)

### What is a Generator?

A generator is a function that behaves like an iterator. This means that we can ask a generator function for its "next" value and it will calculate it, and return it to us. Similar to how a range doesn't calculate all of the values at once, a generator function essentially "pauses" its execution after returning a single result until the next result is requested.

To learn about generators, let's go ahead and implement a function that works like the built-in range type.

### Writing a Generator Function

Generator functions are defined the same way that traditional functions are, except that instead of using the return keyword to provide a result back to the caller, we use the keyword yield. When defining a generator, we will almost always include a loop in the body of the function, and then we'll yield from within the loop. Let's create a new file called gen.py to create our gen_range function.

```
def gen_range(stop, start=1, step=1):
    num = start
    while num <= stop:
        yield num
        num += step
```

Unlike the built-in range function, if we call this function with three arguments, they're in the order of stop, start, and step instead of starting with start. But this function effectively works the same way (although not as performant). Let's load our file into the REPL to test out this function:

```
$ python3.7 -i gen.py
>>> gen_range(10)
<generator object gen_range at 0x1054a8550>
>>>
```

The first thing to note, is that when we call the generator function, it returns a generator object to us instead of giving us the result. To get each result, we'll use the built-in next function to execute the generator until it hits a yield statement. Let's assign the generator object to a variable and pass it to next a few times:

```
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

```
>>> next(generator)
4
>>> next(generator)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

In practice, we won't normally be calling the next function on our generators. We'll be using them with for loops like this:

```
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

## Converting Generators to Lists

Generators are functions that behave like iterators, and that means that they can be used to dynamically calculate items in a loop. But that also means that they can be converted into lists. In this lesson, we'll take a look when and how we can convert a generator into a list.

### Documentation For This Video

[Python Wiki: Generators](https://wiki.python.org/moin/Generators)
[The Built-In next Function](https://docs.python.org/3.7/library/functions.html#next)

### Converting a Generator to a List

When we're working with generators, we'll often write them in such a way that eventually they won't have anything left to yield. And in that case, we can turn the generator into a list. This might sound like it would be difficult, but it's as easy as passing the generator object into the list function that we've used many times before, to convert things like dict_keys objects to be lists.

Let's load our gen.py file into the REPL again so that we can utilize the gen_range function that we wrote in the previous lecture:

```
$ python3.7 -i gen.py
>>> generator = gen_range(10)
>>> list(generator)
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

That was pretty simple. But, it is possible to run into issues with this. Let's say that we define an infinite generator that will always calculate the next item in the Fibonacci sequence we looked at in our recursion lesson.

```
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

```
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

```
>>> list(fib)
```

We'll see that the prompt hangs. That's because it's looping forever. This is the situation when you can't convert a generator to be a list because the list function will never return.

## Scoping

##  Python Scopes

We've lightly touched on this already, but when working with any programming language, the variables and objects that we're working with are only accessible within certain scopes. In this lesson, we'll take a closer look at how scopes work and when our variables might not be what we expect them to be.

### What is a Scope?

When we say that we're working in a different "scope" in Python, we mean that we're within the boundaries of a function or a class. This is important because while within the body of a function or class, the variables that we create are not automatically accessible outside of that context. Let's create a new file called scopes.py so that we can experiment with how scopes work. To start, let's see how variables work when dealing with conditionals and loops.

```
scopes.py

if 1 < 2:
    x = 5

while x < 6:
    print(x)
    x += 1

print(x)
```

Here we're creating a variable (x=5) within the body of a conditional (if 1 < 2:1). Afterward, we attempt to access that variable within the context of a loop (while x < 6:) and at the highest level of our script. Will this work? Let's find out by running this through the interpreter:

```
$ python3.7 scopes.py
5
6
$
```

We didn't run into an error because conditionals and loops do not create scopes. Now, let's change our conditional to be a function instead.

```
scopes.py

def set_x():
    x = 5

set_x()

while x < 6:
    print(x)
    x += 1

print(x)
```

Now if we run this we'll see the following:

```
$ python3.7 scopes.py
Traceback (most recent call last):
  File "scopes.py", line 7, in &lt;module>
    while x < 6:
NameError: name 'x' is not defined
$
```

We see this error because x is defined within the set_x function and only exists during the execution of the function.

## Name Hiding (Shadowing)

Now that we've looked at how scopes work initially, we're ready to look at what happens when we have a function parameter that is the same as a variable that exists at a higher level. This is sometimes called shadowing or name hiding.

### Name Hiding in Action

We know that functions create scopes. But, what happens when a parameter name is the same as a variable that has already been defined? Let's continue using scopes.py to see what happens when we set y before we define the set_x function, and then change our function to have a y parameter:

```
scopes.py

y = 5

def set_x(y):
    print("Inner y:", y)
    x = y
    y = x

set_x(10)
print("Outer y:", y)
```

Now if we run this, we'll see the following:

```
$ python3.7 scopes.py
Inner y: 10
Outer y: 5
```

Since our function defines the y parameter, it's as though the outer y variable doesn't exist within the set_x function. Name hiding makes it possible for us to be confident that our parameters won't be affected by values at a higher scope. That doesn't mean that name hiding is something that we should always use though because it can make our code a little harder for people to understand.

## The `global` Keyword

Occasionally, we want to be able to modify a global variable from within a more specific context. In this situation, Python provides us with the global keyword. In this lesson, we'll learn how to use the global keyword.

### Documentation For This Video
[The global Statement](https://docs.python.org/3/reference/simple_stmts.html?highlight=global#the-global-statement)

###  Modifying the Global State from a Nested Scope

If we would like one of our functions to have the side effect of changing or creating a global variable, we can utilize the global statement. This isn't something that we'll use all that often since it is better to keep global state to a minimum as we start working on larger and more complex programs. But it is useful now and then. Let's modify scopes.py so that we can change the global y variable from within our set_x function:

```
scopes.py

y = 5

def set_x(y):
    print("Inner y:", y)
    x = y
    global y
    y = x


set_x(10)
print("Outer y:", y)
```

If we run this, we should see the following:

```
python3.7 scopes.py
  File "scopes.py", line 7
    global y
    ^
SyntaxError: name 'y' is parameter and global
```

It's important to know that we can't utilize the global statement if we have a parameter with the same name. Let's change our parameter to be z before running this again:

```
scopes.py

y = 5

def set_x(z):
    x = z
    global y
    global a
    y = x
    a = 7

print("y Before set_x:", y)
set_x(10)
print("y After set_x:", y)
print("a After set_x:", a)
```

We've also created a global variable from within our set_x function called a. This variable won't be available before the first time that set_x is called, but we should be able to print it after we've called our function for the first time. Let's run scopes.py again:

```
$ python3.7 scopes.py
y Before set_x: 5
y After set_x: 10
a After set_x: 7
```

This example shows how potentially confusing using global can be. We have a function called set_x that will change the global state for the variable y. Someone who didn't write this code could be completely confused as to why the value of the variable y that they've been working with was changed right out from under them. Keep this in mind when considering whether or not it's a good idea to use the global statement.

{% include links.html %}

