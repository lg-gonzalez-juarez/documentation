---
title: 03. Hands-on Lab 03
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_03.html
folder: handson
---

# Using Python Lists

## Introduction

Lists are one of the fundamental data types that we use in Python for solving real problems. Being able to manipulate lists and access items is necessary for effective programming. In this hands-on lab, we'll be working through some exercises demonstrating that we understand how to add, remove, modify, and read items from lists in Python. We'll perform actions on a list to meet some checkpoint requirements provided to us within a Python file.

To feel comfortable completing this lab we'll want to know how to do the following:

Working with list literals: Watch the "Lists" video from the Certified Entry-Level Python Programmer Certification course.
Using list functions and methods: Watch the "List Functions and Methods" video from the Certified Entry-Level Python Programmer Certification course.

## The Scenario

From within the `using-lists.py` file, we'll be modifying the `users` list so that the assertions throughout the file all succeed eventually. As we're working through the tasks, we can run the file. Whenever Python gets to a line that starts with `assert`, it will raise an error and stop executing if we haven't met the criteria. The first error will look like this:

Note: The `using-lists.py` file exists in the /home/cloud_user/ directory. If you do not see the file, please give the lab another minute to finish provisioning.

```
$ python3.7 using-lists.py
Traceback (most recent call last):
  File "s9-lists/using-lists-starter.py", line 3, in <module>
    assert users == [], f"Expected `users` to be [] but got: {repr(users)}"
NameError: name 'users' is not defined
```

This process will show us the line where the the script encountered an issue, and show us the differences between our expected and actual values.

## Logging In

There are a couple of ways to get in and work with the code. One is to use the credentials provided in the hands-on lab overview page, log in with SSH, and use a text editor in the terminal.

The other is using VS Code in the browser. If you'd like to go this route, then you will need to navigate to the public IP address of the workstation server (provided in the hands-on lab overview page) on port 8080 (example: http://PUBLIC_IP:8080).

Once we are in the server, open up using-lists.py (with either VS Code or a command line text editor) and we can continue.

## Create a users List and Add Initial Items

If we run the script before making any changes (and we run it with `python3.7 using-lists.py`), we'll get an error right off because we have not defined the `users` variable. Since we're going to be working with this variable throughout the lab, we've got to create it first (by adding `users = []` between the existing `# 1`)... and `assert users`... lines):

**using-lists.py** (partial):
```
# 1) Set the users variable to be an empty list
users = []

assert users == [], f"Expected `users` to be [] but got: {repr(users)}"
```

Now if we run the script we should see the error leading us to the second task:

```
$ python3.7 using-lists.py
Traceback (most recent call last):
  File "./using-lists.py", line 8, in <module>
    assert users == ['kevin', 'bob', 'alice'], f"Expected `users` to be ['kevin', 'bob', 'alice'] but got: {repr(users)}"
AssertionError: Expected `users` to be ['kevin', 'bob', 'alice'] but got: []
```

This second error shows us that we need to add values to the list before we can continue. The task also specifies that we shouldn't just reassign the `users` variable. One way to solve this is to append the users to the list (by adding the `users.append` lines between the `# 2`)... and `assert users == ['kevin', 'bob', 'alice']...` lines) like this:

**using-lists.py** (partial):

```
# 2) Add 'kevin', 'bob', and 'alice' to the users list in that order without reassigning the variable.
users.append('kevin')
users.append('bob')
users.append('alice')

assert users == ['kevin', 'bob', 'alice'], f"Expected `users` to be ['kevin', 'bob', 'alice'] but got: {repr(users)}"
```

## Remove bob and Create rev_users List

If we run the script again, we'll see that it's expecting just the `kevin` and `alice` users, but it's also getting `bob`. For the third task, we need to remove that bob value. Here's an example solution that accomplishes this, by using the `del` statement to delete an item in the `users` list (which we'll insert right after the `# 3)...` line):

**using-lists.py** (partial):

```
# 3) Remove 'bob' from the `users` list without reassigning the variable.
del users[1]

assert users == ['kevin', 'alice'], f"Expected `users` to be ['kevin', 'alice'] but got: {repr(users)}"
```

If we run the script again, we'll make is past that error, but get a NameError saying 'rev_users' is not defined. We can correct that by using the `reversed` function and then casting the result of that back to a list using the `list` function. We'll add another variable, `rev_users` (right below the # 4)... line) and incorporate those functions:

```
# 4) Reverse the users list and assign the result to `rev_users`
rev_users = list(reversed(users))

assert rev_users == ['alice', 'kevin'], f"Expected `rev_users` to be ['alice', 'kevin'] but got: {repr(rev_users)}"
```

Now if we run the script again (using `python3.7 using-lists.py`) we get through those errors. But we're greeted with another caused by what's on line 25 of the script.

## Insert melody to users and Concatenate Lists

For tasks five and six we'll be adding more information to our users list. The script is expecting a melody user, so we'll need to add it. To add a single item at the first index we'll use the insert method, and we'll put it in the script right after the # 5)... line:

**using-lists.py** (partial)

```
# 5) Add the user 'melody' to users where 'bob' used to be.
users.insert(1, 'melody')

assert users == ['kevin', 'melody', 'alice'], f"Expected `users` to be ['kevin', 'melody', 'alice'] but got: {repr(users)}"
```

Run the script again, and we'll make it a little bit farther this time. The newest AssertionError says that the script is expecting six users, and we're only giving it three. To add three new items to the end of the list we'll use list concatenation and reassign the `users` variable. We'll do this right after the `# 6)...` line in the script:

```
# 6) Add the users 'andy', 'wanda', and 'jim' to the users list using a single command
users += ['andy', 'wanda', 'jim']

assert users == ['kevin', 'melody', 'alice', 'andy', 'wanda', 'jim'], f"Expected `users` to be ['kevin', 'melody', 'alice', 'andy', 'wanda', 'jim'] but got: {repr(users)}"
```

If we run the script again, we'll see that we've solved that problem, but there's one more error. It's referencing line 35 in the script, and saying that 'center_users' is not defined.

## Slice users to Return 3rd and 4th Elements

For the final task, we'll extract a subsection from the `users` list to create the new `center_users` list. We can extract the third and fourth items from the list by slicing from `2` to `4`. We'll define center_users and make that happen just below the `# 7)...` line:

**using-lists.py (partial)**
```
# 7) Slice the users lists to return the 3rd and 4th items and assign the result to `center_users`
center_users = users[2:4]

assert center_users == ['alice', 'andy'], f"Expected `users` to be ['alice', 'andy'] but got: {repr(center_users)}"
```