---
title: Number Systems and Numeric Operators
tags: [python]
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: python_03.html
folder: python
---

##  Numeric Operators

[link](https://linuxacademy.com/cp/courses/lesson/course/5264/lesson/1)

We've seen numbers in Python, but how do we go about using them? In this lesson, we'll learn about the various numeric operators that we'll use in our Python programs.

### Documentation For This Video
[Python Operators](https://docs.python.org/3/library/operator.html#mapping-operators-to-functions)

### The Numeric Operators
When we think about what we can do with numbers in math, there are quite a few things that come to mind such as addition, subtraction, multiplication, and division. All of those actions are carried out in our programs by using "operators", special characters we put between the two numbers that carry out a specific calculation. In Python, and in most programming languages, there are more operators than we would typically use when doing arithmetic. Here are the most common operators used in the REPL:

```cmd
>>> 2 + 2 # Addition
4
>>> 10 - 4 # Subtraction
6
>>> 3 * 9 # Multiplication
27
>>> 5 / 3 # Division, converts the result to a float even when evenly divided.
1.66666666666667
>>> 5 // 3 # Floor division, always returns a number without a remainder as an int
1
>>> 8 % 3 # Modulo division, returns the remainder as an int
2
>>> 2 ** 3 # Exponent
8
```

There are even more operators than this, but they don't all apply to numbers. We'll learn about some of the other operators in different lessons.

## Number Systems

In our day to day work, we almost always work with decimal numbers. These are not necessarily numbers with decimal points, but numbers derived from a base 10 number system. In this lesson, we'll take a look at how we could use other number systems in Python.

### Documentation For This Video

[Numeral Systems](https://en.wikipedia.org/wiki/Numeral_system)
[Bit Numbering](https://en.wikipedia.org/wiki/Bit_numbering)
[Download the Presentation](https://linuxacademy.com/cp/guides/download/refsheets/guides/refsheets/s5-number-systems-and-floating-point-accuracy_1568816995.pdf)

### What are Number Systems?
We normally count using the decimal number system, which means that for each digit in a number we will cycle between the numbers 0-9 before adding another digit. These same numbers can be represented using other numbering systems though, such as binary which only uses the number 0-1.

The decimal number of 15 is equivalent to 1111 in binary notation. To convert from decimal to binary we divide the decimal number (15) by the base of the other numbering system, in binary's case that's 2 and then we take the remainder as a digit in the binary number. We then take the part that divided cleanly and divide it by the base again. Here's the process for converting 15 to binary:

```cmd
15 / 2 => 7 w/ remainder of 1
7 / 2 => 3 w/ remainder of 1
3 / 2 => 1 w/ remainder of 1
1 / 2 => 0 w/ remainder of 1
```

If we do this with the number 12 we'll get something different:

```cmd
12 / 2 => 6 w/ remainder of 0
6 / 2 => 3 w/ remainder of 0
3 / 2 = 1 w/ remainder of 1
1 / 2 = 0 w/ remainder of 1
```

The bits go from least significant to most, so the remainders at the end of our division will be the most significant digits. 12 as binary is 1100.

Converting back to decimal requires us to multiply each bit from least to greatest by the base (2 in binary) to the power of it's position (starting with the 0 power) and then add those numbers together. Converting 1100 back to decimal looks like this:

```cmd
(1 * 2 ^ 3) + (1 * 2 ^ 2) + (0 * 2 ^ 1) + (0 * 2 ^ 0)
(1 * 8) + (1 * 4) + (0 * 2) + (0 * 1)
8 + 4 + 0 + 0
12
```

### Common Numeral Systems
The most common numbering systems are decimal (10), binary (2), octal (8), and hexadecimal (16). You might be asking yourself, "How do I represent a digit with 16 different numbers?". That's a reasonable question. The answer is to start using letters in addition to numbers. Hexadecimal digits go from 0-9, then from A-F. The binary number `12` is `C` in Hexadecimal.

Representing Binary, Octal, and Hexadecimal Numbers in Python
Now that we know how various and common number systems work let's go about actually using them in Python. To represent a number in a different number system in Python, we do this by prefixing the number with a 0 and the number system identifier:


- Binary uses `b`
- Octal uses `o`
- Hexadecimal uses `x`

Here are examples in the REPL:

```cmd
>>> 0b1001
9
>>> 0o7424
3860
>>> 0xFF012
1044498
```

The result printed out will be the decimal value. If we want to work in decimal values and represent them in a different numbering system we can use the bin, oct, and hex functions like so:

```cmd
>>> bin(10)
'0b1010'
>>> oct(59)
'0o73'
>>> hex(1024)
'0x400'
```

The value returned from these functions will always be a string.

## Floating-Point Accuracy

To complete our conversation about numbers in Python we do need to discuss how accurate floats are.

Documentation For This Video
[Floating Point Arithmetic: Issues and Limitations](https://docs.python.org/3/tutorial/floatingpoint.html#floating-point-arithmetic-issues-and-limitations)
[Download the Presentation](https://linuxacademy.com/cp/guides/download/refsheets/guides/refsheets/s5-number-systems-and-floating-point-accuracy_1568816995.pdf)

### Float Limitations
Not all decimal numbers that we write out can be represented by a computer as a float. The reason for this is that floats are stored on computer hardware as binary fractions, and not all decimal (base 10 numbers) can be represented as binary fractions. This leads to the floating-point numbers that we work with actually being approximations of the binary fraction representation.

An example of this is the decimal number `0.1` which has no binary fraction equivalent. Depending on the machine, the exact approximation used behind the scenes may be different. But since Python 3.1, the representation that is returned to the user is the clean number even though the number used behind the scenes is something like `0.1000000000000000055511151231257827021181583404541015625.`

All of this is to say that sometimes floating-point math doesn't work the way that we expect it to.

{% include links.html %}
