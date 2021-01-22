---
title: 11. Hands-on 11 Calculating Circular Values with Python's Math Modules
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_11.html
folder: handson
---

# Calculating Circular Values with Python's Math Modules

In this lab, we are writing a few simple functions to calculate the circumference and area of some shapes, specifically, circles. We'll need to use a few different things from Python's math module to calculate these values and ensure that the result is accurate given that we're working with PI and our starting measurements can be floats. We want our calculations to be accurate to the 1/100th of a unit.

## Before We Begin
Using the provided credentials, log in to Visual Studio Code. To do so, you will need to navigate to the public IP address of the workstation server (provided in the hands-on lab overview page) on port 8080 (example: http://PUBLIC_IP:8080).

If you would prefer to use your own terminal and log in with SSH, you can do so with the provided credentials.

Important: This guide is written with the use of the Visual Studio Code in mind.

## Implement the circle_circumference Function

Once logged in to our preferred terminal, we can begin by implementing the `circle_circumference` function by completing the following:

1. We need to view our documents with ls and make sure we have the calcs.ph and test_calcs.py documents.
2. Use python -V to make sure our python version is 3.8.2 or higher.
3. Run automated tests with Python on our `test_calcs.py` doc:

```
python test_calcs.py
```

We find that both of our tests fail.

4. Enter Command + O to open up our folders in Visual Studio Code, and change it to `/home/cloud_user/calcs.py` to open the document.

5. Inside the file, change the file to read as follows:

```
python from math import pi

def circle_circumference(radius):
  return 2 * pi * radius

def circle_area(radius):
  pass
```

6. Again, run the test field:

```
python test_calcs.py
```

We are told that our tests are still failing due to our return number being too specific.

7. Change the overly specific number by editing the `calcs.py` file as follows:

```
python from math import pi, ceil

def circle_circumference(radius):
  initial = 2 * pi * radius
  return ceil(initial * 100) / 100


def circle_area(radius):
  pass
```

8. Run our test:

```
python test_calcs.py
```

Now we only see the failure for `the test_area` function.

## Implement the circle_area Function

With our circle_circumference function set, we need to set our circle_area function:

1. While still in our `calcs.py` document, update it to read as follows:

```
`python from math import pi, ceil

def circle_circumference(radius):
  initial = 2 * pi * radius
  return ceil(initial * 100) / 100


def circle_area(radius):
  initial = pi * radius ** 2
  return ceil(initial * 100) / 100
```

2. Run the test again:

```
$ python3.8 test_calcs.py
```

All tests will now show as passed.