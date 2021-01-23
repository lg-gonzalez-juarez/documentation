---
title: 05. Input and Output Operations
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: python_05.html
folder: python
---

## 5.1. Typecasting


Up to this point, we've worked with a lot of different types, but before we can start taking user input and do interesting things with it we'll need to convert from one type to another. This process is called "typecasting".

### Documentation

- [Typecasting: int](https://docs.python.org/3/library/functions.html#int)
- [Typecasting: float](https://docs.python.org/3/library/functions.html#float)
- [Typecasting: str](https://docs.python.org/3/library/functions.html#str)
- [Typecasting: bool](https://docs.python.org/3/library/functions.html#bool)
- [Trust Value Testing](https://docs.python.org/3/library/stdtypes.html#truth-value-testing)

### Converting from a Number Type to a Number Type

We've already seen some typecasting happen behind the scenes when we performed some of the mathematical operations. For instance, performing "true division" (using the / operator) will always return a float even if we provide two integer operands. How do we go about converting from an integer to a float ourselves though?

The answer is by using the float initializer.

```powershell
>>> float(1)
1.0
```

We can do the same thing going from a float to an integer using the int initializer:

```powershell
>>> int(1.3)
1
>>> int(2.6)
2
```

Notice that the result from converting 2.6 to an integer doesn't round, it truncates. It's as though the decimal point value doesn't exist.

Converting between number types is pretty straight forward because they're both numbers, but what happens if we try to convert to and from a string?

### Converting to and from a String

Converting to a string is done by using the str initializer and the results are what you would expect:

```powershell
>>> str(1)
'1'
>>> str(2.6)
'2.6'
>>> str(False)
'False'
```

As we see, even booleans can be typecast to strings. More interesting than converting to strings is trying to convert strings into other usable types, like integers and floats:

```powershell
>>> int('1')
1
>>> float('1')
1.0
>>> float('1.2')
1.2
>>> int('1.2')
### Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: invalid literal for int() with base 10: '1.2'
```

If the string contains something that would be a valid int or float if we typed it into the interpreter, then we're able to typecast it. But as soon as the type doesn't match, or we try to convert something that's not a number to a float or int, then we'll run into issues.

### Converting to a Boolean

One of the more important, and subtle type, conversions that we use in programming is casting to a boolean. We can cast anything to a boolean in Python by using the bool function.

```powershell
>>> bool(1)
True
>>> bool(2.4)
True
>>> bool('Tada')
True
>>> bool('Tada'.lower)
True
>>> bool(0)
False
>>> bool(0.0)
False
>>> bool("")
False
```

There are a select few items that convert into False. These are detailed in the Python truth value testing documentation, but can be summed up as False, None, any 0 value, and any empty sequence (an empty string for instance).

### Boolean Operators with Non-Boolean Objects

Now that we know that every object has a boolean representation, we're ready to revisit the boolean operators of and, or, and not. These operators will operate on any objects by using their boolean representations automatically.

These operations get a little more complicated as we use non-boolean operands:

```powershell
>>> 1 and 0
0
>>> 'This' and 'That'
'That'
>>> 'This' and 0 and 'That'
0
>>> 0.0 and 1
0.0
```

Remember that and requires both operands to be true in order to return true, and this means that it will automatically return the first falsy value that it finds or the rightmost operand if they're both true.

The or operator works in the opposite way. It will return the first object that would evaluate to true, or the rightmost falsy value.

```powershell
>>> 1 or 0
1
>>> 0 or 1
1
>>> 0 or ""
""
>>> 0 or 1 or 'This'
1
```

Lastly, the not operator will simply return the opposite boolean value for whatever we pass to it:

```powershell
>>> not ""
True
>>> not 1
False
```

## 5.2. The `input` Function


With an understanding of the basic types in Python, we're finally ready to start writing some programs. In this lesson, we'll take a look at the input function that allows us to write command-line scripts that take in user input.

### Documentation 

[The input function](https://docs.python.org/3/library/functions.html#input)

### Prompting for User Input

Computer programs aren't that interesting until they can be more dynamic. Over the next few short lessons, we'll be learning about how we can receive input from a user who's running our program from the command-line, and then how we can manage to present information back to the screen.

Before we dig into the input function, let's talk a little bit about functions in general. Functions allow us to package up bits of code to be able to run them more than once. Additionally, functions specify expected inputs and can also return information. If we take a look at a function from mathematics, we can see the same thing:

```powershell
f(x) = x + 2
```

In this case, the name of the function is f, the input is x, and the code that will be executed is x + 2. We can provide a variety of values for x and get a different return value. So f(1) would return 3. In Python, we can reference functions by name, allowing us to pass them around like variables. But a function won't be executed unless we "call it" by using parenthesis. We can see this in the REPL by typing in input without any parenthesis:

```powershell
>>> input
<built-in function input>
```

The input function is the easiest way that we can make our programs request user interaction. This function is simple in that it only takes one optional argument to be the prompt that we present the user. Whatever the user types will be returned by the input function as a string, and that means we can store it in a variable. Let's try this out in the REPL now:

```powershell
>>> favorite = input("Favorite Color: ")
Favorite Color:
```

Now we're left in a new prompt and we can type our answer. When we hit Enter/Return it will submit all of what we wrote and store it in the variable favorite. Note that the prompt argument is optional, so we can simply run input() without an argument and it will leave us at an empty prompt waiting once again for us to hit Enter/Return before then returning that value.

### Prompting for Multiple Values

Now that we know how the input function works, let's create our first real script. In this script, we're going to ask the user to answer a series of questions, and store those answers in variables. In the next lesson, we'll then use these values.

Let's call our script bio.py, and in this script, we'll ask for the following:

- The user's name
- The user's favorite color
- The user's age

Create and open bio.py in your text editor and call input three different times, once for each piece of information that we want:

```powershell
~/code/bio.py
```

```powershell
name = input("What is your name? ")
color = input("What is your favorite color? ")
age = input("How old are you today? ")
```

Both name and color make sense to be strings, but age should be a number. Let's cast the value returned from the age prompt to be an int before assigning it to the variable. We can do this by placing the parenthesis for the int function around the entire input function call:

```powershell
~/code/bio.py
```

```powershell
name = input("What is your name? ")
color = input("What is your favorite color? ")
age = int(input("How old are you today? "))
```

Now that we've written our script, let's run it:

```powershell
$ python3.7 bio.py
What is your name? Kevin Bacon
What is your favorite color? Orange
How old are you today? 61
$
```

We didn't do anything with the values that were returned, but since we were returned to our shell without an error we know that everything executed properly. If we were to give an invalid answer for the age question (something that wasn't an int) Python will raise an error. We need to keep that in mind.

## 5.3. The `print` Function

Now that we've taken in some user input, we're going to look at how we can customize some information and write it out to the screen. In this lesson, we're going to dig into how the print function works, and see how we can place variable values into strings.

### Documentation 

[The print function](https://docs.python.org/3/library/functions.html#print)

### Printing to the Screen

In the first program that we wrote, we printed "Hello, World!" out to the screen using the print function. That's as simple as it gets, but printing in Python is incredibly easy. Now that our bio.py script is taking in some input from a user, we're ready to write some code to print information back out. Our goal is to take the information from the user for their name, color, and age and print out this sentence with the variables substituted in:

```powershell
NAME is AGE years old and loves the color COLOR.
```

We're going to take a look at a few different ways to do this using the print function.

### The print Function

As with most things in programming, there's more than one way for us to achieve our goal of printing the user's information in the proper format. For the exam, we need to understand how to use the sep and end optional arguments to the print function.

Let's take a quick look at how the print function works by default and also when we set the sep and end arguments.

```powershell
~/code/bio.py

name = input("What is your name? ")
color = input("What is your favorite color? ")
age = int(input("How old are you today? "))

print(name)
print("is " + str(age) + " years old")
print("and loves the color " + color + ".")
```

If we run this now we'll see this:


```powershell
$ python3.7 bio.py
What is your name? Kevin Bacon
What is your favorite color? Orange
How old are you today? 61
Kevin Bacon
is 61 years old
and loves the color Orange.
```

Every time we call print, the string will be printed to the screen with a trailing newline, so the next print will always be on the next line. We can change this by setting the end value using a keyword argument. The end argument is set to '\n' by default, but if we change it to ' ' then it should print the three lines as one. When a function takes multiple arguments, then we separate them using commas. And for keyword arguments, we use the argument's name = the value that we want it to use. We'll learn more about how arguments work for functions later, but this is enough for now.

Let's modify our script to set the end value:

```powershell
~/code/bio.py

name = input("What is your name? ")
color = input("What is your favorite color? ")
age = int(input("How old are you today? "))

print(name, end=" ")
print("is " + str(age) + " years old", end=" ")
print("and loves the color " + color + ".", end=" ")
```

Running it again shows this:

```powershell
$ python3.7 bio.py
What is your name? Kevin Bacon
What is your favorite color? Orange
How old are you today? 61
Kevin Bacon is 61 years old and loves the color Orange.
```

We've successfully printed out what we needed to, but it feels a little tedious. The print function can take any number of arguments before we use keyword arguments like sep and end. It will then print each argument separated by the sep character which is '' by default. If we set this to a single space then we should be able to use a single print call to print the sentence properly.

Let's see what this looks like:

```powershell
~/code/bio.py

name = input("What is your name? ")
color = input("What is your favorite color? ")
age = int(input("How old are you today? "))

print(name, 'is', age, 'years old and loves the color', color, '.', sep=" ")
```

Running it again shows this:

```powershell
$ python3.7 bio.py
What is your name? Kevin Bacon
What is your favorite color? Orange
How old are you today? 61
Kevin Bacon is 61 years old and loves the color Orange .
```

We're so close, but there's an extra space between the color and the period. We'll need to combine those into a single string instead.

```powershell
~/code/bio.py

name = input("What is your name? ")
color = input("What is your favorite color? ")
age = int(input("How old are you today? "))

print(name, 'is', age, 'years old and loves the color', color + '.', sep=" ")
```
