---
title: 07. Hands-on Lab 07
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_07.html
folder: handson
---

# Utilizing Python Loops

## Introduction

One of the great strengths of computer programs is that they can process an incredible amount of information far faster than we could do it manually. To achieve this we need to be able to loop through collections and sequences. In this hands-on lab, we'll work through the popular interviewing Fizz-Buzz problem by creating a script that will prompt the user for the number of items to process, and then print out either the number, "Fizz", "Buzz", or "FizzBuzz" for each number between 1 and the user-provided number.

To feel comfortable completing this lab you'll want to know how to do the following:

Utilize for loops. Watch "The for Loop" video from the Certified Entry-Level Python Programmer Certification course.
Nest conditionals and loops. Watch the "Nesting Loops and Conditionals" video from the Certified Entry-Level Python Programmer Certification course.
Utilize the range type. Watch "Using range" video from the Certified Entry-Level Python Programmer Certification course.

## The Scenario

A typical Fizz-Buzz problem goes like this:

Write a program that prints the numbers from 1 - 100. For each multiple of three print "Fizz" instead of the number. For multiples of five print "Buzz" instead of the number. If a number is a multiple of three and five then print "FizzBuzz". Solving this problem requires two key components: looping and conditionals.

We're going to write a script that prompts the user for the number of items to process (starting with 1). For each number, we'll print either "Fizz", "Buzz", "FizzBuzz", or the number. The criteria for what to print is:

* Print "FizzBuzz" if the number is divisible by 3 and 5.
* Print "Fizz" if the number is divisible by 3.
* Print "Buzz" if the number is divisible by 5.
* Otherwise print the number.

Here's how the final script should work:

```
$ ./fizz-buzz.py
How many values should we process: 20
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
16
17
Fizz
19
Buzz
```

## Logging In

There are a couple of ways to get in and work with the code. One is to use the credentials provided in the hands-on lab overview page, log in with SSH, and use a text editor in the terminal.

The other is using VS Code in the browser. If you'd like to go this route, then you will need to navigate to the public IP address of the workstation server (provided in the hands-on lab overview page) on port 8080 (example: http://PUBLIC_IP:8080).

Create the fizz-buzz.py Script, Make It Executable with python3.7, and Accept User Input
We're going to create fizz-buzz.py, placing it in our home directory (~), and we want to make sure that we can run it directly. To keep from being completely tied to the path of our python3.7 binary, we want to make sure that our shebang is set up properly.

Let's create the file (using either a terminal or VS Code) and set the shebang:

**~/fizz-buzz.py**

```
#!/usr/bin/env python3.7
# Python implementation here
```

With the file created, we need to also make sure that it's executable, and we can do this using `chmod`:

```
$ chmod u+x ~/fizz-buzz.py
```

Next, we'll prompt the user for a value, convert it to an int, and store it off in a variable.


**~/fizz-buzz.py**

```
#!/usr/bin/env python3.7

upper_number = int(input("How many values should we process: "))
```

## Create a Range from 1 to the User's Provided Number and Loop Through It

To print the number from `1` to the user's provided number (including that number), we'll want to utilize the `range` type and a `for` loop. Here's what our loop will look like:

**~/fizz-buzz.py**

```
#!/usr/bin/env python3.7

upper_number = int(input("How many values should we process: "))

for number in range(1, upper_number + 1):
    print(number)
```

If we run it again, and enter 10 at the prompt, we'll see the numbers 1-10 printed out to the terminal. For now, replace `print(number)` with `pass`, and we can move on to write the conditional logic to process each number.

## Print "FizzBuzz" if the Value Is a Multiple of Three and Five

Now that we have a `number` value to use, we can create our conditional. Since we have a case that should trigger if the value is a multiple of three and five, then we'll want that branch to be before the only multiple of three or only multiple of five branches, because either of those would also be true. Let's create our `if` statement and print "FizzBuzz"if the condition is met, then add an `else` to just print the value otherwise:

**~/fizz-buzz.py**

```
#!/usr/bin/env python3.7

upper_number = int(input("How many values should we process: "))

for number in range(1, upper_number + 1):
  if number % 3 == 0 and number % 5 == 0:
      print("FizzBuzz")
  else:
      print(number)
```

Now we can run the script to make sure that what we've written up to this point is working properly:

```
$ ./fizz-buzz.py
How many values should we process: 20
...
12
13
14
FizzBuzz
16
...
$
```

15 is replaced by FizzBuzz, because it's evenly divisible by 3 and 5, and the rest of the numbers print out normally.

## Print "Fizz" if the Number Is a Multiple of Three and "Buzz" if It's a Multiple of Five

To handle the other two cases of the Fizz-Buzz problem, we'll need to utilize `elif` statements for each of the individual comparisons that we used in our `if` statement. Let's add those now:

**~/fizz-buzz.py**

```
#!/usr/bin/env python3.7

upper_number = int(input("How many values should we process: "))

for number in range(1, upper_number + 1):
  if number % 3 == 0 and number % 5 == 0:
      print("FizzBuzz")
  elif value % 3 == 0:
      print("Fizz")
  elif value % 5 == 0:
      print("Buzz")
  else:
      print(number)
```

Now we can run the script to make sure that what we've written up to this point is working properly:

```
$ ./fizz-buzz.py
How many values should we process: 30
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
16
17
...
$
```