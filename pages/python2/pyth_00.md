---
title: Math Functions
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: pyth_00.html
folder: python2
---

Course: Using Python's Math, Science, and Engineering Libraries

[link Linux Academy](https://linuxacademy.com/cp/modules/view/id/621)


## Common `math` Functions and Constants

Python's [math library](https://docs.python.org/3/library/math.html) has a number of functions and constants that are used in everyday math applications. These include trigonometric functions, common math operations, and math constants.

Applications involving relatively simple math operations are a great use for the math package.

## Overview of Math Library and Operations

### Common math Constants

First, we must import the math package

```
import math
>>> math.pi
3.141592653589793
>>>
>>> math.e
2.718281828459045
>>>
>>> math.tau
6.283185307179586
>>>
```
Many math operations behave differently for "floats" versus "ints". Let's take a look at some examples.

### Modulo (%)

A simple explanation of modulo is the remainder when two numbers are divided:

```
>>> 3 % 2
1
>>> 75 % 3
0
>>>
```

A common use is to determine if a number is even or odd. In some applications, it is important to do one thing if a number is even and another if it is odd. An easy way to determine this is to modulo the number by 2. If it is even, the modulo is 0, and if it's odd, then the modulo is 1.

Given the list [5, 6, 4, 2, 8, 9, 4, 6, 7], determine how many odd and even numbers there are. From looking at each number, you can tell there are three odd numbers and six even numbers.

Let's write a Python program to do that calculation for us:

```
int_list = [5, 6, 4, 2, 8, 9, 4, 6, 7]

odd = 0
even = 0
for num in int_list:
    if num % 2 == 0:
        even += 1
    else:
        odd += 1

print(f"There were {even} even numbers and {odd} odd numbers.")
There were 6 even numbers and 3 odd numbers.
```

That was a simple example and may have taken more time to write the program than to count them by hand. So given the list below, determine the number of odd and even numbers. Not quite as trivial!

```
int_list = [1297, 603, 1071, 539, 1222, 1424, 986, 397, 970, 1102, 499, 533, 908, 559, 386, 1183, 595, 69, 1141, 76, 1156, 249, 1005, 1340, 570, 1459, 863, 1343, 185, 895, 1312, 50, 918, 677, 394, 629, 1317, 944, 466, 751, 1050, 301, 415, 784, 19, 1395, 1223, 979, 252, 1155, 59, 107, 632, 995, 972, 867, 332, 751, 810, 50, 55, 218, 997, 1085, 475, 1494, 372, 648, 428, 673, 629, 445, 392, 504, 288, 626, 707, 1302, 1449, 83, 1441, 1274, 271, 1151, 101, 657, 1381, 1384, 1102, 21, 298, 1131, 540, 720, 333, 251, 35, 1239, 1071, 313, 784, 381, 311, 1241, 1377, 996, 1342, 329, 380, 874, 1431, 1489, 922, 939, 501, 1208, 356, 1111, 828, 204, 3, 86, 262, 362, 669, 618, 1272, 889, 991, 620, 449, 1044, 774, 707, 1425, 904, 217, 870, 43, 1430, 1321, 1379, 1175, 622, 1445, 730, 672, 1376, 779, 15, 1170, 1199, 1278, 1482, 17, 227, 1363, 441, 1309, 550, 657, 485, 725, 865, 267, 991, 294, 1375, 1479, 905, 1229, 1023, 323, 657, 1409, 451, 1456, 964, 263, 1388, 735, 1304, 499, 238, 992, 384, 34, 208, 1253, 1011, 362, 350, 1267, 377, 639, 167, 857, 895, 1220, 577, 652, 200, 1475, 375, 1440, 11, 1285, 1371, 370, 314, 658, 411, 616, 699, 830, 682, 472, 121, 916, 167, 1243, 1211, 1490, 252, 1147, 1462, 1499, 667, 566, 1268, 687, 1370, 1063, 65, 335, 1183, 354, 1483, 1090, 139, 959, 603, 1303, 1019, 1237, 760, 1382, 33, 118, 176, 978, 657, 1127, 33, 704, 585, 1128, 990, 284, 344, 100, 160, 67, 397, 1306, 1316, 124, 99, 22, 1040, 25, 1312, 39, 886, 1430, 89, 350, 1105, 439, 1026, 130, 908, 719, 1001, 571, 280, 310, 242, 1168, 249, 1422, 7, 1373, 1401, 800, 777, 737, 1109, 1040, 1226, 547, 816, 579, 971, 151, 269, 108, 663, 1213, 300, 299, 458, 1024, 970, 868, 942, 1043, 365, 1438, 240, 608, 1391, 791, 378, 286, 1309, 1090, 70, 116, 390, 465, 428, 125, 953, 75, 261, 553, 294, 569, 1406, 175, 1472, 425, 584, 1285, 1359, 231, 553, 215, 406, 1007, 1294, 1276, 944, 201, 94, 605, 212, 508, 814, 564, 1403, 262, 1012, 92, 109, 585, 264, 260, 123, 1136, 643, 73, 966, 1180, 281, 1291, 1267, 1293, 988, 814, 930, 1050, 43, 1402, 1113, 181, 379, 951, 52, 668, 54, 881, 249, 1428, 1500, 8, 1289, 640, 95, 559, 1303, 52, 243, 604, 461, 81, 1449, 106, 1127, 78, 740, 1204, 1374, 1197, 1230, 176, 61, 403, 25, 1115, 603, 1119, 27, 316, 106, 1260, 1132, 29, 523, 1094, 987, 1065, 562, 664, 897, 821, 383, 612, 261, 239, 1062, 1236, 1374, 337, 288, 104, 163, 451, 1223, 208, 663, 1066, 737, 803, 1040, 90, 1490, 735, 155, 1389, 222, 512, 591, 321, 35, 377, 153, 981, 838, 1420, 1071, 1300, 867, 11, 259, 1161, 339, 564, 1439, 1056, 1475, 337, 288, 238, 242, 525, 1353, 885, 1417, 127, 677, 16, 1300, 1408, 604, 9, 1071, 175, 964]

There were 227 even numbers and 273 odd numbers.
```

The modulo operator works great for this case and with many integers. However, the math library has a modulo function: ```math.fmod(x, y)```. These actually work a little differently:

```
>>> # fmod_neg_first_number
>>> math.fmod(-67.1, 7.5)
-7.099999999999994
>>> # fmod_neg_second_number
>>> math.fmod(67.1, -7.5)
7.099999999999994
>>> # mod_neg_first_number
>>> -67.1 % 7.5
0.4000000000000057
>>> # mod_neg_second_number
>>> 67.1 % -7.5
-0.4000000000000057
>>>
```

The ```fmod``` function is based on the platform C library. I can't honestly tell you what that means or why it functions in this fashion. But for Python programming, use ```%``` for integers and ```math.fmod``` for floats.

### x raised to y

There are three ways to raise one number to the power of another:


1. x ** y
2. pow(x, y)
3. math.pow(x, y)

As with other functions we have looked at in the math library, there are some idiosyncrasies:

```
>>> # exponentials using **
>>> 2**2
4
>>> # pow() function to achieve exponentials
>>> pow(2, 2)
4
>>> # math.pow() pow function in math package
>>> math.pow(2, 2)
4.0
>>>
```

That all seems to work as we would expect. However, math.pow() does not behave as the other the other two. It always returns a float, while the other two will return a int, if that is what they are given:

```
>>> type(2 ** 2)
<class 'int'>
>>> type(pow(2, 2))
<class 'int'>
>>> type(math.pow(2, 2))
<class 'float'>
>>>
```

Also, it cannot compute a negative number raised to the power of a non-integer:

```
>>> -2 ** 1.3
-2.4622888266898326
>>> pow(-2, 1.3)
(-1.4472970592128211-1.992033505851624j)
>>> math.pow(-2, 1.3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: math domain error
>>>
```

### ceil(x) and floor(y)

```math.ceil(x)``` returns the smallest integer greater than or equal to x. (If x is already an integer, the same number is returned.)

```math.floor(x)``` returns the largest integer less than or equal to x. (If x is already an integer, the same number is returned.)

```
>>> math.ceil(math.pi)
4
>>> math.floor(math.pi)
3
>>>
```

### math.fsum(iterable)

```float ``` math by computers is not precise, but it is usually precise enough. This is just an artifact of the way computers handle float math:

```
import math

sum_list = [0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1]

# sum list using the `+` operand
addition_total = 0
for num in sum_list:
    addition_total += num

# sum using python's sum function
sum_total = sum(sum_list)

# sum using python's math library fsum
fsum_total = math.fsum(sum_list)

print(f"addtion: {addition_total}\nsum: {sum_total}\nfsum: {fsum_total}")
addtion: 0.9999999999999999
sum: 0.9999999999999999
fsum: 1.0
```

You can see the lack of precision in the first two; however, fsum implementation more precisely sums floats when that extra precision is needed.

### Log and Trig functions

This library also functions to calculate the log, natural log, sin, cos, tan, and many other types of common math calculations.