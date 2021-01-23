---
title: 25. Hands-on Lab Creating and Using Python Classes
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_25.html
folder: handson
---

# Introduction

As we work on more and more complex problems, we need to start creating custom types to have manageable models for the data we're working with. Python is an object-oriented programming language, and creating classes is something we will do frequently to solve problems using Python. In this hands-on lab, we'll define a custom class with some functionality and attributes that will allow us to model an `Employee` in our code. The `using_classes.py` script includes code that will utilize this class and provide us with some feedback to know if we've created a class that meets our requirements. To feel comfortable completing this lab, you'll want to know how to create and use Python classes (watch the "Creating and Using Python Classes" video from the Certified Associate in Python Programming Certification course).

# Solution

To work through the lab, you can either log in via a terminal on your local machine and use a text editor in the terminal, or you can use VS Code in the browser. This lab guide will go through the steps using VS Code in the browser.

In order to use VS Code in the browser, navigate to the public IP address of the workstation server (provided on the lab page) on port 8080 (e.g., http://<PUBLIC_IP>:8080).

# Create the employee Module with an Empty Employee Class

1. In the menu at the top, click Terminal > New Terminal.

2. Run `using_classes.py`:

``` 
python3.7 using_classes.py
```
We'll receive an error.

3. Create an empty class:

```
touch employee.py
```

4. In the menu at the top, click **File** > **Open**.

5. Select **employee.py**.

6. Add the following to the file:

```
class Employee:
    pass
```

7. Run `using_classes.py` again:

```
python3.7 using_classes.py
```

This time, we'll see a new error.

# Implement the Employee.__init__ Method

1. Edit the `employee.py` file to match the following:

```
class Employee:
    def __init__(self, name, email_address, title, phone_number=None):
        self.name = name
        self.email_address = email_address
        self.title = title
        self.phone_number = phone_number
```

2. Run `using_classes.py` again:

```
python3.7 using_classes.py
```

3. This time, we'll see an attribute error related to email signature.

# Implement the Employee.email_signature Method

1. Add the following to the end of the `employee.py` file:

```
    def email_signature(self, include_phone=False):
        signature = f"{self.name} - {self.title}\n{self.email_address}"
        if include_phone and self.phone_number:
            signature += f" ({self.phone_number})"
        return signature
```

2. Run `using_classes.py` one last time:

```
python3.7 using_classes.py
```

We should see no output if we've implemented the method correctly.

