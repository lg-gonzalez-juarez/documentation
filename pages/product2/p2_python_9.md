---
title: String
keywords: sample
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: p2_python9.html
# simple_map: true
# map_name: usermap
# box_number: 4
folder: product2
---

## String Encodings and Functions

Strings hold onto characters and those characters don't need to be alphanumeric. Depending on how a string is encoded, some characters might not be valid. Before we can dig into string encodings, we need to take a look at some of the functions that allow us to interact with Unicode code points (the numbers behind characters). In this video, we'll delve into the ord and chr functions.

### Documentation For This Video

- [The ord Function](https://docs.python.org/3/library/functions.html#ord)
- [The chr Function](https://docs.python.org/3/library/functions.html#chr)

### What are Unicode Code Points?

In Python 3, strings are Unicode by default (specifically UTF-8 encoded). Behind the scenes, each character is stored as its Unicode code point, but what does that mean? Unicode is an encoding standard that allows all sorts of unique characters across different languages to have consistent, unique numeric values. For instance, the code point for the letter a is 97, but the character that isn't commonly typed out like the trademark symbol ™ has a code point of 8482. Unicode is a standard, but there are different encodings, one of the most commonly used being UTF-8. UTF-8 stands for "Unicode Transformation Format," with the "8" meaning that values are 8-bits in length. 1,112,064 valid Unicode code points can be encoded with UTF-8.

Up to this point, we've been working with strings that use standard ASCII characters (letters, numbers, and common punctuation). ASCII is an older specification with 256 named characters. Their corresponding code points and the first 128 are also valid UTF-8 values. The trademark symbol is in the ASCII specification under the extended characters table, so it has an ASCII numeric value between 128 - 255, but a completely different Unicode code point.

To make things even more confusing, Unicode code points are sometimes represented in decimal form and other times by using a 'U+' with the hexadecimal form of the same number. So '™' is 8482, but if you search the internet, you'll usually see it written as U+2122.

### Going from Code Point to String and Vice Versa

Now that we have an idea of what code points are and how encodings work let's see how we can work with them in Python. If we want to see the code point for a character that we know how to type, then we can use the ord function. This function takes a single character and will return the decimal code point. Let's see what this looks like for the letter l:

```cmd
>>> ord('l')
108
```

If we try to use ord with more than one character, then it will raise an error:

```cmd
>>> ord('la')
Traceback (most recent call last):
  File "<input>", line 1, in <module>
    ord('la')
TypeError: ord() expected a character, but string of length 2 found
```

If we already know the Unicode code point for a character that is more difficult to type, like the trademark symbol, then we can type it out using the hexadecimal notation if we prefix the number with \u:

```cmd
>>> ord('\u2122')
8482
```

Notice that ord took a single character as the argument, but didn't give us an error when we escaped the Unicode code point by using the \u. This is because a Python string is UTF-8 encoded by default, and although it looks like more than one character to us, that is a single character in UTF-8.

It's also worth noting that when the string \u2122 is evaluated in Python, it will print the character that we're expecting:

```cmd
>>> '\u2122'
'™'
>>> '\u2124'
'?'
```

Say we want to take a decimal code point and convert it back into a string. To do that we'll need to use the chr function:

```cmd
>>> chr(8482)
'™'
```

Because we can write integers in hexadecimal notation using the 0x prefix, and those numbers then get converted into the decimal value, we are also able to use that form with the chr function:

```cmd
>>> chr(0x2122)
'™'
```

## Useful String Methods, Part 1

{% include links.html %}
