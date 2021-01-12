---
title: Conditionals
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: python_12.html
folder: python
---

## Looping

### The `while` Loop

We work with collections of data and sequence a lot in programming, and it is common for us to want to perform the same action on each item or a subset of items in the content. To handle this, we need iteration and looping. In this lesson, we'll learn about one type of loop that we can use: the while loop.

### Documentation For This Video

[while statement](https://docs.python.org/3/tutorial/introduction.html#first-steps-towards-programming)

### The while Loop

The most basic type of loop that we have at our disposal is the while loop. This type of loop repeats itself based on a condition that we pass to it. Here's the general structure of a while loop:

```cmd
while CONDITION:
    pass
```

The CONDITION in this statement works the same way that it does for an if statement. When we demonstrated the if statement, we first tried it by simply passing in True as the condition. Let's see when we try that same condition with a while loop:

```cmd
>>> while True:
...     print("looping")
...
looping
looping
looping
looping
```

That loop will continue forever, we've created an infinite loop. To stop the loop, press Ctrl-C. Infinite loops are one of the potential problems with while loops. If we don't use a condition that we can change from within the loop, then it will continue forever if it's initially true. Here's how we'll normally approach using a while loop, where we modify something about the condition on each iteration:

```cmd
>>> count = 1
>>> while count <= 4:
...     print("looping")
...     count += 1
...
looping
looping
looping
looping
>>>
```

 ## The `for` Loop

We work with collections of data and sequence a lot in programming, and it is common for us to want to perform the same action on each item or a subset of items in the content. To handle this we need iteration and looping. In this lesson, we'll learn about the most common type of loop that we will use: the for loop.

### Documentation For This Video
[The for statement](https://docs.python.org/3/tutorial/controlflow.html#for-statements)

### The for Loop
The most common use we have for looping is when we want to execute some code for each item in a sequence. For this type of looping or iteration, we'll use the for loop. The general structure for a for loop is:

```cmd
for TEMP_VAR in SEQUENCE:
    pass
```
The TEMP_VAR will be populated with each item as we iterate through the SEQUENCE, and it will be available to us in the context of the loop. After the loop finishes one iteration, then the TEMP_VAR will be populated with the next item in the SEQUENCE, and the loop's body will execute again. This process continues until we either hit a break statement or we've iterated over every item in the SEQUENCE. Here's an example that loops over a list of colors:

```cmd
>>> colors = ['blue', 'green', 'red', 'purple']
>>> for color in colors:
...     print(color)
...
blue
green
red
purple
>>> color
'purple'
```

### Other Iterable Types

Lists will be the most common type that we iterate over using a for loop, but we can also iterate over other sequence types. Of the types we already know, we can iterate over strings, dictionaries, and tuples.

Here's a tuple example:

```cmd
>>> point = (2.1, 3.2, 7.6)
>>> for value in point:
...     print(value)
...
2.1
3.2
7.6
>>>
```

In this dictionary example, by default, will first unpack each key:

```cmd
>>> ages = {'kevin': 59, 'bob': 40, 'kayla': 21}
>>> for key in ages:
...     print(key)
...
kevin
bob
kayla
```

If we leverage what we've learned about dictionaries, we can actually get the key and value on each iteration by using dict.items and unpacking the tuple in each iteration:

```cmd
>>> for key, value in ages.items():
...     print(key, value)
...
kevin 59
bob 40
kayla 21
```

A string example:

```cmd
>>> for letter in "my_string":
...     print(letter)
...
m
y
_
s
t
r
i
n
g
>>>
```
## Nesting Loops and Conditionals

Now that we've learned how to use loops and conditionals, we can do a lot more with our programs. We can do even more when we combine them by nesting loops within conditionals or conditionals within loops.

### Nesting Conditionals within Loops

We've seen two of the most common types of code contexts in Python: the body of a conditional and the body of a loop. To signify code contexts in Python, we use indentation. If we need to nest contexts, like conditionals or loops, then we can add more indentation. Let's say we're looping through a list of numbers, and we only want to print the number if it's a multiple of 4. In this case, we can add a conditional check within our loop:

```cmd
>>> counter = 1
>>> while counter <= 25:
...     if counter % 4 == 0:
...         print(counter)
...     counter += 1
...
4
8
12
16
20
24
```

For each nested context, we'll need to indent an extra 4 spaces. When we're done doing what we need to do in a nested context, then we go back to the previous indentation level to continue at that level. This is how we're able to continue past the if statement to increment the counter, all still within the while loop.

###  Controlling Loop Execution with `break` and `continue`

There are times while working with loops, that we want to skip a single iteration, or even completely stop a loop before it is finished. We can accomplish these two things by using the continue and break statements.

### Documentation For This Video

[The break and continue statements](https://docs.python.org/3/tutorial/controlflow.html#break-and-continue-statements-and-else-clauses-on-loops)

### The continue and break Statements

If we want to continue to the next iteration in a nested context or stop the loop entirely, we have access to the continue and break keywords:

```cmd
>>> count = 0
>>> while count < 10:
...     if count % 2 == 0:
...         count += 1
...         continue
...     print(f"We're counting odd numbers: {count}")
...     count += 1
...
We're counting odd numbers: 1
We're counting odd numbers: 3
We're counting odd numbers: 5
We're counting odd numbers: 7
We're counting odd numbers: 9
>>>
```

The continue statement will cause the nearest loop (if we have nested loops) to go directly to the next iteration. This means that we will not execute any of the remaining lines of the loop for the current iteration. This can be an issue if we continue without incrementing the count value in our example loop's conditional.

We're demonstrating "string interpolation" in Python 3 by prefixing a string literal with an f and then using curly braces to substitute in variables or expressions (in this case, the count value).

The break statement works similarly to the continue statement in that it keeps our current iteration from executing the remaining lines in the loop, but it also causes the entire loop to stop.

Here's an example using the break statement:

```
>>> count = 1
>>> while count < 10:
...     if count % 2 == 0:
...         break
...     print(f"We're counting odd numbers: {count}")
...     count += 1
...
We're counting odd numbers: 1
```

### Using break and continue with a for Loop

The break and continue statements work with for loops as well. If we didn't want to print out certain colors, we could utilize the continue or break statements again. Let's say we want to skip the string 'blue' and terminate the loop if we see the string 'red':

```cmd
>>> colors = ['blue', 'green', 'red', 'purple']
>>> for color in colors:
...     if color == 'blue':
...         continue
...     elif color == 'red':
...         break
...     print(color)
...
green
>>>
```

## Integrating `else` with Loops

Unlike many languages, loops in Python have an additional clause that we can use: the else clause. In this lesson, we'll take a look at why and when we might want to use this additional Python feature.

### Documentation For This Video 

- [The break and continue statements and the else clause](https://docs.python.org/3/tutorial/controlflow.html#break-and-continue-statements-and-else-clauses-on-loops)

## The else Clause

The else clause for loops in Python allows us to define an additional code context that will execute when the loop has naturally finished its iteration. In a for loop, this means that we've reached the end of our iteration, and in a while loop it means the conditional has evaluated to False. Here's an example for each of these:

```cmd
>>> counter = 1
>>> while counter <= 4:
...     print(counter)
...     counter += 1
... else:
...     print("While loop completed")
...
1
2
3
4
While loop completed
```

```
>>> for i in [1, 2, 3, 4, 5]:
...     print(i)
... else:
...     print("For loop completed")
...
1
2
3
4
5
For loop completed
>>>
```

This might seem a little useless because we could have just as easily written these additional print statements on the line directly following the loop and achieved the same result. That's true. The else clause isn't that valuable unless we utilize it in conjunction with the break statement. The else clause's body will execute if the break statement is not hit. We can leverage this when we're iterating through a list:

```
>>> colors = ['red', 'pink', 'blue', 'orange', 'green']
>>> for color in colors:
...     if color == 'orange':
...         print("Orange is in the list")
...         break
... else:
...     print("Orange is not in the list")
```

### Orange is in the list
This is not the most efficient way to search through a list, but it's a good example of when the else clause of a loop has an effect besides just being the expression run after the loop.

## Using `range`

Sometimes we want to iterate a set number of times, but we don't necessarily have a collection to work with. An easy way to achieve this is by creating a range object and iterating over it.

### Python Documentation For This Video

- [Sequence Types](https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range)
- [Ranges](https://docs.python.org/3/library/stdtypes.html#range)

### Ranges

A range is an immutable sequence type that defines a start, a stop, and a step value. The values within the range start with the beginning value and are incremented until the last value in the range is reached. This allows for ranges to be used in place of sequential lists while taking less memory and including more items.

```cmd
>>> my_range = range(10)
>>> my_range
range(0, 10)
>>> list(my_range)
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> list(range(1, 14, 2))
[1, 3, 5, 7, 9, 11, 13]
```

Notice that the "stop" value (in this example, 10) is not included in the range.

By using a range with a for loop, we can specify the number of times we would like to iterate without needing to manually worry about incrementing a counter like we had to do with a while loop. Here's a previous example where we printed "looping" four times using a while loop:


```
>>> count = 1
>>> while count <= 4:
...     print("looping")
...     count += 1
looping
looping
looping
looping
>>>
```

We could achieve this same thing using for and range like this:

```
>>> for _ in range(1, 5):
...     print("looping")
...
looping
looping
looping
looping
>>>
```

## List Comprehensions

Iterating over a sequence is great, but needing to transform a list into a different list is fairly common. Python has a special feature to make doing this concise, called "list comprehensions".

## Documentation For This Video

[List Comprehensions](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions)

### List Comprehensions

If we want to loop through a list, modify each item, and have a new list with the modified items, then we could do something like this:

```
>>> colors = ['red', 'blue', 'orange', 'green', 'yellow']
>>> uppercase_colors = []
>>> for color in colors:
...     uppercase_colors.append(color.upper())
...
>>> uppercase_colors
['RED', 'BLUE', 'ORANGE', 'GREEN', 'YELLOW']
```

This procedure is common enough that Python provides a shorthand method for doing it in the form of "list comprehensions." These have a unique syntax where we essentially put the for loop within square brackets ([]). Here's the equivalent for the above, using a list comprehension:

```
>>> colors = ['red', 'blue', 'orange', 'green', 'yellow']
>>> uppercase_colors = [color.upper() for color in colors]
>>> uppercase_colors
['RED', 'BLUE', 'ORANGE', 'GREEN', 'YELLOW']
```

The biggest difference here is that we don't need to create an empty list and append to it. Whatever we place to the left of the for statement within the comprehension will be returned as part of the final list.

### List Comprehensions for Filtering

List comprehensions also have another feature that allows for filtering while iterating through the initial list by adding a trailing if statement within the square brackets ([]). If we wanted to iterate through our colors and only return "warm" colors (red, orange, yellow) then we could write this loop to achieve these results:

```
>>> colors = ['red', 'blue', 'orange', 'green', 'yellow']
>>> warm_colors = []
>>> for color in colors:
...     if color in ['red', 'orange', 'yellow']:
...         warm_colors.append(color.upper())
...
>>> warm_colors
['RED', 'ORANGE', 'YELLOW']
```

If we remove the concept of warm_colors being used within the loop, we can write it as a list comprehension:

```
>>> colors = ['red', 'blue', 'orange', 'green', 'yellow']
>>> warm_colors = [color.upper() for color in colors if color in ['red', 'orange', 'yellow']]
>>> warm_colors
['RED', 'ORANGE', 'YELLOW']
```

The syntax for list comprehensions are a little odd to get started with. But if you read it as a sentence, then it will start to make more sense and feel more useful. The sentence would read something like this: Uppercase each color in the colors variable if the colors are red, orange, and yellow.


{% include links.html %}
