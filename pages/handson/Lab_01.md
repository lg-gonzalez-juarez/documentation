---
title: 01. Hands-on Lab 01
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_01.html
folder: python2
---


# Making Calculations from User Input with Python

## Introduction

After learning about data structures, user input and output programming becomes a lot more powerful. There are many things that we can accomplish by simply taking user input, running it through a process, and returning some useful output. To put these skills to use, we'll write a simple tool to perform temperature conversions from Fahrenheit to Celsius. To feel comfortable completing this lab you'll want to know how to handle user input with the `input` function, be familiar with type casting from strings to floats, and understand the process of printing to the screen.

## The Scenario

We have international coworkers, and there's no topic of conversation more common than the weather. This simple script will be quite useful to us, providing a quick reference to check in the middle of any "How is the weather over there," types of conversations. Here is what the final process (running the script) will look like:

```
$ ./to-celsius.py
What temperature (in Fahrenheit) would you like converted to Celsius? 68.18
68.18 F is 20.1 C
$
```

For us to implement it, we'll need to do the following:

1. Prompt the user for the temperature in Fahrenheit.
2. Convert the string temperature to a float.
3. Process the Fahrenheit float value through the formula: `celsius = (temp - 32) * 5 / 9`
4. Print the original and converted values to the screen.

To feel comfortable completing this lab you'll want to know how to do the following:

* Handling user input using the input function. Watch the videos from the "Input and Output Operations" section of the Certified Entry-Level Python Programmer Certification course.
* Type casting from strings to floats. Watch the "Type Casting" video from the Certified Entry-Level Python Programmer Certification course.
* Printing to the screen. Watch the videos from the "Input and Output Operations" section of the Certified Entry-Level Python Programmer Certification course.

## Logging In

There are a couple of ways to get in and work with the code. One is to use the credentials provided in the hands-on lab overview page, log in with SSH, and use a text editor in the terminal.

The other is using VS Code in the browser. If you'd like to go this route, then you will need to navigate to the public IP address of the workstation server (provided in the hands-on lab overview page) on port `8080` (example: `http://PUBLIC_IP:8080`).

Create the `~/to-celsius.py` Script and Make It Executable with python3.7

For the time being, we're going to write our script in our home directory (~) and we want to be able to run it right away. To make sure that we're not completely tied to the path of our python3.7 binary, we need to we set up our shebang properly.

Let's create the file and set the shebang:

**~/to-celsius.py**

```
#!/usr/bin/env python3.7
# Python implementation here
```

Now that the file is created, we need to also make it executable by using `chmod`:

```
$ chmod u+x ~/to-celsius.py
```

Now we can run our script by running `./to-celsius.py` from our home directory.


## Prompt and Store Fahrenheit Value from User

When we run our script, we would like to prompt the user for a temperature value in Fahrenheit. Let's do this using the `input` function:

`~/to-celsius.py`

```
#!/usr/bin/env python3.7

# Python implementation here
fahrenheit = input("What temperature (in Fahrenheit) would you like converted to Celsius? ")
```

By default, this variable will be a string, so we'll need to cast it to be a float:

**~/to-celsius.py**

```
#!/usr/bin/env python3.7

# Python implementation here
fahrenheit = float(input("What temperature (in Fahrenheit) would you like converted to Celsius? "))
```

Now we're ready to use this value in our calculation.

## Calculating the Celsius Value

The Fahrenheit to Celsius formula is celsius = (temp - 32) * 5 / 9 and this converts almost perfectly to Python. We only need to change temp to be our variable fahrenheit.

```
~/to-celsius.py

#!/usr/bin/env python3.7

# Python implementation here
fahrenheit = float(input("What temperature (in Fahrenheit) would you like converted to Celsius? "))
celsius = (fahrenheit - 32) * 5 / 9
Print the Calculated Value to the Screen
```

Now that we have our final value we're ready to print it to the screen in the form of:

```
FAHRENHEIT F is CELSIUS C
```

We can do this by passing our values into the print function:

**~/to-celsius.py**

```
#!/usr/bin/env python3.7

# Python implementation here
fahrenheit = float(input("What temperature (in Fahrenheit) would you like converted to Celsius? "))
celsius = (fahrenheit - 32) * 5 / 9
print(fahrenheit, "F is", celsius, "C")
```


Now if we use our script we should see the following:

```
$ ./to-celsius.py
What temperature (in Fahrenheit) would you like converted to Celsius? 68.18
68.18 F is 20.100000000000005 C
```


We're showing more decimal places in our Celsius value than we might like, but we can hide these by using the round function to round to 2 decimal places like this: round(celsius, 2). The whole last line of the script would now read:

```
print(fahrenheit, "F is", round(celsius, 2), "C")
```


 -> Congratulations!