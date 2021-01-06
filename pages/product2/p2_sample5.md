---
title: Input and Output Operations
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: p2_sample5.html
simple_map: true
map_name: usermap
box_number: 5
folder: product2
---

## Typecasting


Up to this point, we've worked with a lot of different types, but before we can start taking user input and do interesting things with it we'll need to convert from one type to another. This process is called "typecasting".

### Documentation For This Video

[Typecasting: int](https://docs.python.org/3/library/functions.html#int)
[Typecasting: float](https://docs.python.org/3/library/functions.html#float)
[Typecasting: str](https://docs.python.org/3/library/functions.html#str)
[Typecasting: bool](https://docs.python.org/3/library/functions.html#bool)
[Trust Value Testing](https://docs.python.org/3/library/stdtypes.html#truth-value-testing)

### Converting from a Number Type to a Number Type

We've already seen some typecasting happen behind the scenes when we performed some of the mathematical operations. For instance, performing "true division" (using the / operator) will always return a float even if we provide two integer operands. How do we go about converting from an integer to a float ourselves though?

The answer is by using the float initializer.

```cmd
>>> float(1)
1.0
```

We can do the same thing going from a float to an integer using the int initializer:

```cmd
>>> int(1.3)
1
>>> int(2.6)
2
```

Notice that the result from converting 2.6 to an integer doesn't round, it truncates. It's as though the decimal point value doesn't exist.

Converting between number types is pretty straight forward because they're both numbers, but what happens if we try to convert to and from a string?

### Converting to and from a String

Converting to a string is done by using the str initializer and the results are what you would expect:

```cmd
>>> str(1)
'1'
>>> str(2.6)
'2.6'
>>> str(False)
'False'
```

As we see, even booleans can be typecast to strings. More interesting than converting to strings is trying to convert strings into other usable types, like integers and floats:

```cmd
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

```cmd
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

```cmd
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

```cmd
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

```cmd
>>> not ""
True
>>> not 1
False
```

### The `input` Function


With an understanding of the basic types in Python, we're finally ready to start writing some programs. In this lesson, we'll take a look at the input function that allows us to write command-line scripts that take in user input.

### Documentation For This Video

[The input function](https://docs.python.org/3/library/functions.html#input)

### Prompting for User Input

Computer programs aren't that interesting until they can be more dynamic. Over the next few short lessons, we'll be learning about how we can receive input from a user who's running our program from the command-line, and then how we can manage to present information back to the screen.

Before we dig into the input function, let's talk a little bit about functions in general. Functions allow us to package up bits of code to be able to run them more than once. Additionally, functions specify expected inputs and can also return information. If we take a look at a function from mathematics, we can see the same thing:

```cmd
f(x) = x + 2
```

In this case, the name of the function is f, the input is x, and the code that will be executed is x + 2. We can provide a variety of values for x and get a different return value. So f(1) would return 3. In Python, we can reference functions by name, allowing us to pass them around like variables. But a function won't be executed unless we "call it" by using parenthesis. We can see this in the REPL by typing in input without any parenthesis:

```cmd
>>> input
<built-in function input>
```

The input function is the easiest way that we can make our programs request user interaction. This function is simple in that it only takes one optional argument to be the prompt that we present the user. Whatever the user types will be returned by the input function as a string, and that means we can store it in a variable. Let's try this out in the REPL now:

```cmd
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

```
~/code/bio.py
```

```cmd
name = input("What is your name? ")
color = input("What is your favorite color? ")
age = input("How old are you today? ")
```

Both name and color make sense to be strings, but age should be a number. Let's cast the value returned from the age prompt to be an int before assigning it to the variable. We can do this by placing the parenthesis for the int function around the entire input function call:

```
~/code/bio.py
```

```cmd
name = input("What is your name? ")
color = input("What is your favorite color? ")
age = int(input("How old are you today? "))
```

Now that we've written our script, let's run it:

```cmd
$ python3.7 bio.py
What is your name? Kevin Bacon
What is your favorite color? Orange
How old are you today? 61
$
```

We didn't do anything with the values that were returned, but since we were returned to our shell without an error we know that everything executed properly. If we were to give an invalid answer for the age question (something that wasn't an int) Python will raise an error. We need to keep that in mind.




{% include links.html %}
