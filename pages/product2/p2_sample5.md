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

{% include links.html %}
