---
title: Operators and Bindings
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: p2_sample4.html
simple_map: true
map_name: usermap
box_number: 4
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

{% include links.html %}
