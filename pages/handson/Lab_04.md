---
title: 04. Hands-on Lab 04
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_04.html
folder: python2
---

# Using Python Dictionaries

## Introduction

Dictionaries are one of the fundamental data types that we use in Python to solve real problems. These are handy when we don't need a sequential list of items, and it is more useful to have unique identifiers for looking up values. Being able to manipulate dictionaries and access items is necessary for effective programming. In this hands-on lab, we'll be working through some exercises demonstrating that we understand how to add, remove, modify, and read items from dictionaries in Python. We'll be asked to perform actions on a dictionary to meet some checkpoint requirements provided to us within a Python file.

To feel comfortable completing this lab you'll want to know how to do the following:

Working with dictionary literals. Watch the "Dictionaries" video from the Certified Entry-Level Python Programmer Certification course.
Using Dictionary functions and methods. Watch the "Dictionary Methods" video from the Certified Entry-Level Python Programmer Certification course.

## The Scenario

From within the `using-dictionaries.py` file, we'll be modifying the `users` list so that the assertions throughout the file all succeed eventually. As we're working through the tasks we can run the file. Whenever Python gets to a line that starts with `assert`, it will raise an error and stop executing if we haven't met the criteria. The first error will look like this:

```
$ python3.7 using-dictionaries.py
Traceback (most recent call last):
  File "s9-lists/using-dictionaries-starter.py", line 3, in <module>
    assert users == [], f"Expected `users` to be [] but got: {repr(users)}"
NameError: name 'users' is not defined
```

This process will show us the line where the issue was encountered, and show us the differences between our expected and actual values.

## Logging In

There are a couple of ways to get in and work with the code. One is to use the credentials provided in the hands-on lab overview page, log in with SSH, and use a text editor in the terminal.

The other is using VS Code in the browser. If you'd like to go this route, then you will need to navigate to the public IP address of the workstation server (provided in the hands-on lab overview page) on port `8080` (example: `http://PUBLIC_IP:8080`).

Once we are in the server, open up `using-dictionaries.py` (with either VS Code or a command line text editor) and we can continue.

## Create the emails Dictionary and Add Initial Items

Our first few tasks require us to create the emails variable that we're going to work with throughout the lab and then add some information to it. Here's how we complete the first task:

**using-dictionaries.py** (partial)

```python
# 1) Set the emails variable to be an empty dictionary
emails = {}assert emails == {}, f"Expected `emails` to be {{}} but got: {repr(users)}"
```

Now if we run the file (python3.7 using-dictionaries.py), we should see the error for the second task:

```python
$ python3.7 using-dictionaries.py
Traceback (most recent call last):
  File "using-dictionaries-final.py", line 12, in <module>
    }, f"Expected `emails` to be {{'ashley': 'ashley@example.com', 'craig': 'craig@example.com', 'elizabeth': 'elizabeth@example.com'}} but got: {repr(emails)}"
AssertionError: Expected `emails` to be {'ashley': 'ashley@example.com', 'craig': 'craig@example.com', 'elizabeth': 'elizabeth@example.com'} but got: {}
```

This shows us that we need to add values to the dictionary before we can continue. The task also specifies that we shouldn't just reassign the emails variable. Here's an example solution to this:

**using-dictionaries.py** (partial)

```python
# 2) Add 'ashley', 'craig', and 'elizabeth' to the emails dictionary without reassigning the variable.

emails['ashley'] = 'ashley@example.com'
emails['craig'] = 'craig@example.com'
emails['elizabeth'] = 'elizabeth@example.com'

assert emails == {
    'ashley': 'ashley@example.com',
    'craig': 'craig@example.com',
    'elizabeth': 'elizabeth@example.com'
}, f"Expected `emails` to be {{'ashley': 'ashley@example.com', 'craig': 'craig@example.com', 'elizabeth': 'elizabeth@example.com'}} but got: {repr(emails)}"
```

Now when we run `python3.7 using-dictionaries.py` again, we'll get a little farther down the script before we get an error.

## Remove craig and Add dalton

For tasks 3 and 4, we need to remove the `craig` key/value pair and add one called `dalton`. Here's an example solution for getting rid of `craig`:

**using-dictionaries.py** (partial)

```python
# 3) Remove 'craig' from the emails dictionary without reassigning the variable.
del emails["craig"]

assert emails == {
    "ashley": "ashley@example.com",
    "elizabeth": "elizabeth@example.com",
}, f"Expected `emails` to be {{'ashley': 'ashley@example.com', 'elizabeth': 'elizabeth@example.com'}} but got: {repr(emails)}"
```

When we run the script again, we'll get an error about it expecting a `dalton`. To fix that, we need to add it in. Here's how:

```python
# 4) Add 'dalton' to the emails dictionary without reassigning the variable.
emails["dalton"] = "dalton@example.com"
assert emails == {
    "ashley": "ashley@example.com",
    "elizabeth": "elizabeth@example.com",
    "dalton": "dalton@example.com",
}, f"Expected `emails` to be {{'ashley': 'ashley@example.com', 'elizabeth': 'elizabeth@example.com', 'dalton': 'dalton@example.com'}} but got: {repr(emails)}"
```

The `del` statement will allow us to remove an item with the specified key to complete task three. For task four, we've just added add another key/value pair.

## Return a List of Keys and a List of Values from the emails Dictionary

For tasks 5 and 6, we'll be extracting information from the `emails` dictionary to populate new lists for `users` and `email_list`. The `users` list will contain all of the keys from `emails` and the `email_list` will include all of the values.

**using-dictionaries.py** (partial)

```python
# 5) Return a list of keys from the emails dictionary as `users`
users = list(emails.keys())

assert users == [
    "ashley",
    "elizabeth",
    "dalton",
], f"Expected `users` to be ['ashley', 'elizabeth', 'dalton'] but got: {repr(users)}"

# 6) Return a list of values from the emails dictionary as `email_list`
email_list = list(emails.values())

assert email_list == [
    "ashley@example.com",
    "elizabeth@example.com",
    "dalton@example.com",
], f"Expected `email_list` to be ['ashely@example.com', 'elizabeth@example.com', 'dalton@example.com'] but got: {repr(email_list)}"
```

Running the script now will get us almost to the end.

## Return a List of Tuples Called pairs Representing the Key/Value Pairs in emails

For the final task, we'll extract a new list called `pairs` from emails that will include a 2-tuple for each key/value pair in the `emails` dictionary.

**using-dictionaries.py** (partial)

```python
# 7) Return a list of tuples called `pairs` representing the key/value pairs in `emails`.
pairs = list(emails.items())

assert pairs == [
    ("ashley", "ashley@example.com"),
    ("elizabeth", "elizabeth@example.com"),
    ("dalton", "dalton@example.com"),
], f"Expected `pairs` to be [('ashley', 'ashley@example.com'), ('elizabeth', 'elizabeth@example.com'), ('dalton', 'dalton@example.com')] but got: {repr(pairs)}"
```
