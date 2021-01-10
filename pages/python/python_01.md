---
title: Fundamental Concepts
keywords: sample
tags: [special_layouts]
summary: "This is just a sample topic..."
sidebar: product2_sidebar
permalink: python_01.html
# simple_map: true
# map_name: usermap
# box_number: 1
folder: python
---

## Compilers and Interpreters

[LunixAcademy](https://linuxacademy.com/cp/courses/lesson/course/5262/lesson/1/module/413)

The compiler would be something that produces machine code. So at its core, what a compiler does is it takes code from one type, transfers it into a different type. So most of the time, this is going to be going from a high-level language like Python or something else down to something that is lower level and can run on the machine directly, or it can run in a virtual machine. So that's what a compiler does; it just translates code from one type of code to another type of code. That's the simplified version of this, and there are many different types of compilers that can exist, and we're not going to cover all of them.We just need to loosely know what a compiler does,but the compilation process consist of five basic steps here.

## Lexing, Syntax, and Semantics
[LinuxAcademy](https://linuxacademy.com/cp/courses/lesson/course/5262/lesson/2/module/413)

In this secction is covered some of the steps involved in the compilation and interpreting process:

* Lexical Analysis
* Syntactic Analysis
* Semantic Analysis

## Python Specifics: Keywords and Instructions
[LinuxAcademy](https://linuxacademy.com/cp/courses/lesson/course/5262/lesson/3/module/413)

In this lesson, we'll cover some more foundational concepts of programming languages:

* Keywords
* Bytecode Instructions

## Using the REPL
[LinuxAcademy](https://linuxacademy.com/cp/courses/lesson/course/5262/lesson/4/module/413)

Python is an interpreted language, and code is evaluated in a line-by-line fashion. Since each line can be evaluated by itself, the time between evaluating each line doesn't matter, and this allows us to have a REPL.

### Documentation
[Python Interpreter](https://docs.python.org/3/tutorial/interpreter.html)

What is a REPL?
REPL stands for: Read, Evaluate, Print, Loop

Each line is read and evaluated, the return value is printed to the screen, and then the process repeats.

Python ships with a REPL and you can access it by running `python3.7` from your terminal.

The `>>>` indicates that you can type on that line. Later on, you'll also see a `...` which means that you are currently in a scoped area and will need to enter a blank line (no spaces) before it will evaluate the entire code block.

The simplest use of this would be to do some math:
```cmd
$ 1 + 1
2
>>>
```

`2` is the return value of the expression and it is then printed to the screen. If something doesn't have a return value, then nothing will be printed to the screen and you'll see the next prompt immediately. We'll cover this later, but an example would be None:
```cmd
$ None
>>>
```

To exit the REPL, you can either type `exit()` (the parentheses are important) or you can hit `Ctrl+d` on your keyboard.

## Creating a Python File
[info](https://linuxacademy.com/cp/courses/lesson/course/5262/lesson/5/module/413)

Since this is a course about Python scripting, we will be writing the majority of our code in scripts instead of using the REPL. To create a Python script we can create a file ending with the file extension of `.py`.

### Creating Our First Python Script
Let's create our first script to write our obligatory "Hello, 
World!" program, calling it `hello.py`.

```cmd
$ touch hello.py
```
From inside this file, we can enter the lines of Python that we need. For the "Hello, World!" example we only need

```powershell
~/code/hello.py
print("Hello, World!")
```

There are a few different pays that we can run this file. The first is by passing it to the `python3.7` CLI.

```bash
$ python3.7 hello.py
Hello, World!
```
### Setting a Shebang
We'll most likely want our scripts to be:

1. Executable from anywhere (in our $PATH)
2. Executable without explicitly using the `python3.7` CLI

Thankfully, we can set the process to interpret our scripts by setting a shebang at the top of the file:

`hello.py:`

```cmd
#!/usr/bin/env python3.7
print("Hello, World")
```
We're not quite done. Now we need to make the file executable using `chmod:`

```dos
$ chmod u+x hello.py
```
Run the script now by using `./hello.py` and we'll see the same result. If we'd rather not have a file extension on our script, we can remove it since we've put a shebang in the file. Running `mv hello.py` hello then performing `./hello` will still result in the same thing.


{% include links.html %}
