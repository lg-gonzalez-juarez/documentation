---
title: 02. Hands-on Lab Lab Indexing and Slicing Python Strings
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_02.html
folder: handson
---

# Indexing and Slicing Python Strings

## Introduction

Accessing characters, whether they are single or multiple, is an essential skill for working with strings in any programming language. In Python, we do this by indexing and slicing the string. In this hands-on lab, we'll go through writing some code to demonstrate that we understand how to use indexing and slicing by printing out different pieces of information about a string back to the user. To feel comfortable completing this lab you'll want to be familiar with working with string literals, indexing and slicing strings, and printing information out to the screen.

## The Scenario

We're going to write a script that takes user input, so that we're not working with static content, and print out some information and permutations of the string that the user has entered. Our string-info.py script will print the following information about the user provided message:

* The first character
* The last character
* The middle character (for even length strings we'll return the integer just after the exact center).
* Every even index character
* Every odd index character
* The message in reverse

Here's our script in action:

```
$ string-info.py
Enter a message: Test Message
First character: T
Last character: e
Middle character: e
Even index characters: Ts esg
Odd index characters: etMsae
Reversed message: egasseM tseT
```

To feel comfortable completing this lab you'll want to be familiar with the following:

Working with string literals: Watch the "Strings and String Operators" video from the Certified Entry-Level Python Programmer Certification course.
Indexing and slicing strings: Watch the "String Indexing and Slicing" video from the Certified Entry-Level Python Programmer Certification course.
Printing to the screen: Watch the videos from the "Input and Output Operations" section of the Certified Entry-Level Python Programmer Certification course.

## Logging In

There are a couple of ways to get in and work with the code. One is to use the credentials provided in the hands-on lab overview page, log in with SSH, and use a text editor in the terminal.

The other is using VS Code in the browser. If you'd like to go this route, then you will need to navigate to the public IP address of the workstation server (provided in the hands-on lab overview page) on port 8080 (example: http://PUBLIC_IP:8080).

If you'd like to use VS Code in the browser then you will need to navigate to the public IP address of the workstation server on port 8080 (example: http://PUBLIC_IP:8080)

Create the **string-info.py** Script and Take User Input

We want to be able to execute our script, so to begin let's create an empty script with a shebang and make it executable:

```
$ echo '#!/usr/bin/env python3.7' > string-info.py
$ chmod +x string-info.py
```

Now we can either edit the file with something like something like vim (if we got into the environment via SSH) or edit it by using File > Open if we came in via the VS Code application.
Our goal here is to have the script take in some user input, then print a handful of lines to the screen. Let's take the user input now:

**string-info.py**

```
#!/usr/bin/env python3.7

message = input("Enter a message: ")
Print the First, Last, and Middle Characters from the User's Input
```

To print the first, last, and middle characters from a string, we need to index the message. The first and last characters will be straight forward so let's add those initially:

**string-info.py**

```
#!/usr/bin/env python3.7

message = input("Enter a message: ")

print("First character:", message[0])
print("Last character:", message[-1])
```

Getting the middle character is a little more complicated. It will have the same number of characters before and after it. There is a character in the middle of a string if it has an odd length (eg: abc has b in the middle), but for an even length string, then the middle is really between two indexes (eg: abcd where the middle is between bc).

We can calculate the middle by dividing the length of the string by 2 and truncating it to get the index value. We can truncate the value by casting the result of the division back to being an integer. Here's what our print function call looks like:

**string-info.py**

```
#!/usr/bin/env python3.7

message = input("Enter a message: ")

print("First character:", message[0])
print("Last character:", message[-1])
print("Middle character:", message[int(len(message) / 2)])
Print the Even Index Characters and Odd Index Characters
```

To print the even index characters and the odd index characters, we'll need to use slicing with the step option. The only thing that we need to change between these two lines will be the starting index, as long as we step by 2. Here's what it these lines look like:

**string-info.py**

```
#!/usr/bin/env python3.7

message = input("Enter a message: ")

print("First character:", message[0])
print("Last character:", message[-1])
print("Middle character:", message[int(len(message) / 2)])
print("Even index characters:", message[0::2])
print("Odd index characters:", message[1::2])
Print the String in Reverse
```

Reversing a string can be done by getting a little creative with how slicing works. If we don't provide a start or end index, and then set a -1 step value, then we'll reverse the string.

**string-info.py**

```
#!/usr/bin/env python3.7

message = input("Enter a message: ")

print("First character:", message[0])
print("Last character:", message[-1])
print("Middle character:", message[int(len(message) / 2)])
print("Even index characters:", message[0::2])
print("Odd index characters:", message[1::2])
print
```