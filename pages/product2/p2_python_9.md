---
title: Operators and Bindings
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: p2_python9.html
# simple_map: true
# map_name: usermap
# box_number: 4
folder: product2
---

## Unary and Bitwise Operators

Before we start using the types that we've learned to write larger scripts with, we're going to want to know about the operators that we have access to. In this lesson, we'll be defining unary and bitwise operators.

### Documentation For This Video

- [Python Bitwise Operator Documentation](https://wiki.python.org/moin/BitwiseOperators)
- [Python Operators](https://docs.python.org/3/library/operator.html#mapping-operators-to-functions)

### What is a Unary Operator?

A unary operator is an operator that only has one operand. Where the + operation is a binary operator, because we need to provide an operand to the right and left of the operator, a unary operator only takes a right-side operand.

### What are Bitwise Operators?

Bitwise operators are operators that work off of the bit information (binary notation) for numbers. These aren't used that often, but it's good to have an understanding of what they do.

Positions in binary numbers are known as "bits" and they can either be 0 or 1. Bitwise operations do various things based on the values of these bits.

### A Brief Aside About Truth Tables

One tool from logic (from philosophy) that is used at every level of computer science is the idea of truth tables. Truth tables describe how various operations in boolean algebra work, and can show us all of the available options. Bitwise operators are boolean algebra operations because they deal with 0 and 1, which will equate to false and true. We won't go too deep into truth tables, but if you'd like to have a better understanding of boolean logic then I would encourage you to research them.

### Operators: Bitwise Complement

The first bitwise operator that we're going to talk about is probably the most confusing one: the bitwise complement operator ~. This is the only unary operator that we're going to talk about in this lesson. It takes a number that we're going to call x, and returns the result of -x - 1. To show what this looks like in binary we'll also use the bin function to show our integers as binary numbers:

```cmd
>>> a = 0b010
2
>>> bin(a)
'0b10'
>>> ~a
-3
>>> bin(~a)
'-0b11'
```

### Bitwise OR
The remainder of the bitwise operators make a lot more sense and require two numbers as the operands. The bitwise OR operation will take two numbers, and if one of them has a 1 in a bit position then it will return a 1 at that position in the final result. To use the bitwise OR we'll use a single pipe characters |:

```cmd
>>> a = 0b1001
>>> b = 0b1100
>>> bin(a | b)
'0b1101'
```

### Bitwise AND

Where bitwise OR will return a 1 for a bit position if that position is a 1 in either number, bitwise AND requires that both have a 1 at that position, otherwise it will have a 0 at that position in the final result. The bitwise AND operator is a single ampersand &:

```cmd
>>> a = 0b1001
>>> b = 0b1100
>>> bin(a & b)
'0b1000'
```

### Bitwise XOR

Bitwise XOR (exclusive or) is an interesting operator where the position in the final result will have a 1 if exactly one of the operands has a 1 in that position. The bitwise XOR operator is a caret ^:

```cmd
>>> a = 0b1001
>>> b = 0b1100
>>> bin(a ^ b)
'0b101'
```

### Bitwise Right Shift

The final two operators allow us to shift our bit values directly sideways by a certain number of positions. To shift our bits to the right we'll use the bitwise right shift operator which is >>. Our initial values are on the left-hand side and the number of positions to shift is on the right:

```cmd
>>> a = 0b110
>>> bin(a >> 2)
'0b1'
>>> bin(a >> 4)
'0b0'
```

Notice that if we shift beyond the number of bits in our number then we simply get 0 as the result.

### Bitwise Left Shift

Bitwise left shift uses the << operator with the same rules as the right shift operator. For each position that we shift then we'll add a new 0 bit to the right.

```cmd
>>> a = 0b110
>>> bin(a << 2)
'0b11000'
>>> bin(a << 4)
'0b1100000''
```

## Boolean

Believe it or not, now that we understand bitwise operators we've learned the basics of doing boolean logic. We're in a great spot to learn about boolean operators.

### Python Documentation For This Video

[Boolean Operators](https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not)

The `not` Operation
Sometimes we want to know the opposite boolean value for something. To do this, we use the unary operators not:

```cmd
>>> not True
False
>>> not False
True
```

The `or` Operation

The boolean or operator works the same way that the bitwise OR operator did if we are only considering one bit. The bit of 1 is equivalent to True and 0 is equivalent to False

```cmd
>>> True or True
True
>>> True or False
True
>>> False or False
False
>>> False or True
True
```

The `and` Operation

The and operator is the opposite of or, and both of the operands need to be true.

```cmd
>>> True and True
True
>>> True and False
False
>>> False and False
False
>>> False and True
False
```

## Comparison Operators

The last operators that we need to learn about are the comparison operators. These operators allow us to know if two items are equivalent, or if one is great than the other.

## Documentation For This Video

- [Comparisons](https://docs.python.org/3/library/stdtypes.html#comparisons)
- [The ord function](https://docs.python.org/3/library/functions.html#ord)


### The Greater Than and Less Than Operators

We're going to work our way through the comparison operators by starting with the ones that will feel most familiar from mathematics. The four greater than and less than operators work exactly as you'd expect:

```cmd
>>> 1 < 2
True
>>> 2 > 1
True
>>> 2 < 1
False
>>> 1 <= 1
True
>>> 2.0 >= 3
False
```

A few things to note are that we can compare numeric types to one other, so it's not hard to compare floats with integers.

Another thing to notice is that these comparison operators always return a boolean value.

Remember that individual types dictate whether or not they work with specific operands. And strings, for instance, work with these comparison operators too:

```cmd
>>> 'a' > 'b'
False
>>> 'b' > 'a'
True
>>> 'bb' >= 'ba'
True
>>> 'a' <= 'c'
True
```

When comparing strings, each character is compared with the character at the same index in the other string to determine which one is larger. Behind the scenes, each character as a numeric value that we can find using the [ord] function, and these are used to do the comparisons.

Once again, if we try to compare types that aren't comparable, then we'll receive an error indicating such:

```cmd
>>> 'a' <= 1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: '<=' not supported between instances of 'str' and 'int'
```

### The Equals Operators

The equals operators are a little different than you might expect, because we already use a single equals sign for variable assignment operations. Because of this, to see if two things are equal we use a double equals sign ==:

```cmd
>>> 1 == 1
True
>>> 1.0 == 1
True
>>> 2 == 1.0
False
>>> 'a' == 2
False
>>> 'a' == 'a'
True
```

Notice that this checks equivalence, so comparing an equivalent float and integer will return True. Additionally, we're able to compare two completely different types without receiving an error because they're not equivalent.

If we want to know if two objects aren't equivalent, then we can use the not equal operators !=. This will return True only if the items aren't equivalent:

```cmd
>>> 1 != 1
False
>>> 1.0 != 1
False
>>> 2 != 1.0
True
>>> 'a' != 2
True
>>> 'a' != 'a'
False
```

### The Identity Operators

If we want to know if two objects are or are not exactly the same object, then we can use the identity operators. The identity operator is the keyword is and the opposite is is not (with a space).

```cmd
>>> 1 is 1
True
>>> 1 is 1.0
False
>>> 'a' is 'a'
True
>>> 'a' is not 'b'
True
>>> 'a' is not 'a'
False
```

The identity operators work based on the id of the object, and most of the basic types in Python are immutable (meaning they cannot be changed), so every time that we reference a specific literal it will point to the same item in memory. We can check the id of an object by using the id function (your return values will be different):

```cmd
>>> id('a')
4444195248
>>> id('a')
4444195248
>>> id('a') == id('a')
True
```

We'll discuss immutability later, but not all objects are immutable, so you'll run into situations where you can compare two objects that look the same using is and have False returned. Here are two list literals (which aren't immutable):

```
>>> [] is []
False
```

## Operator Priority (Binding)

Now that we've learned about quite a few operators, we're ready to learn how Python determines the order to run them if there are multiple in a single expression.

### Documentation For This Video
[Operator precedence](https://docs.python.org/3/reference/expressions.html#operator-precedence)

### Operator Precedence

In mathematics, we have the order of operations that tell us how we're going perform our calculations, and in Python, we have operator precedence. We haven't covered all of the contents of this table just yet, but we can look at how everything that we have used so far will be processed.

For whatever reason, the Python documentation shows the least binding operators first, but we'll talk about them from most binding to least. We'll leave the ones that we won't cover in this course out of the list though:

- Parenthesis and List/Dictionary/Set literals
- Accessing attributes (subscription, slicing, function/method call, attribute reference)
- Exponentiation (**)
- Positive, Negative, and bitwise complement
- Multiplication *, Division /, Floor Division //, Modulo %
- Addition +, Subtraction -
- Bitwise Shifts << & >>
- Bitwise AND &
- Bitwise XOR ^
- Bitwise OR |
- Comparison operators (in, not in, is, is not, <, >, <=, >=, ==, !=)
- Boolean NOT not
- Boolean AND and
- Boolean OR or
- Conditions if


Let's look at some examples:

```cmd
>>> 14 & 3 * 2 + 4
10
>>> 14 & 3 * (2 + 4)
2
>>> (14 & 3) * 2 + 4
8
>>> 14 & (3 * 2) + 4
10
```

{% include links.html %}
