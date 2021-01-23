---
title: 26. Hands-on Lab  Using Inheritance in Python
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_26.html
folder: handson
---

# Introduction

Modeling problems using objects is incredibly powerful, and having more specific classifications can make modeling complex problems even easier. Inheritance allows us to do this with our classes. In this hands-on lab, we'll expand the classifications we have for employees in our codebase by adding a subclass with more functionality. To feel comfortable completing this lab, you'll want to know how to create and use Python classes (watch the "Creating and Using Python Classes" video from the Certified Associate in Python Programming Certification course) and use inheritance and super (watch the "Inheritance and Super" video from the Certified Associate in Python Programming Certification course).

# Solution

To work through the lab, you can either log in via a terminal on your local machine and use a text editor in the terminal, or you can use VS Code in the browser. This lab guide will go through the steps using VS Code in the browser.

In order to use VS Code in the browser, navigate to the public IP address of the workstation server (provided on the lab page) on port 8080 (e.g., http://<PUBLIC_IP>:8080).

# Create the Manager Class in a New manager Module

1. In the menu at the top, click **Terminal** > **New Terminal**.

2. Run the `using_inheritance.py` module:

```
python3.7 using_inheritance.py
```

We'll see there's no manager module.

3. Create `manager.py`:

```
touch manager.py
```

4. In the menu at the top, click **File** > **Open**.


5. Select manager.py.

6. Add the following to the file:

```
from employee import Employee

class Manager(Employee):
    pass
```

7. Run `using_inheritance.py` again:

```
python3.7 using_inheritance.py
```

Now, we'll see an error saying the `Manager` object has no `meetings` attribute.

# Add a New meetings Attribute That Defaults to an Empty List

1. Edit `manager.py` to match the following:

```
from employee import Employee

class Manager(Employee):
    def __init__(self, name, email_address, title, phone_number=None):
        super().__init__(name, email_address, title, phone_number)
        self.meetings = []
```

Run `using_inheritance.py` again:

```
python3.7 using_inheritance.py
```

Now, we'll see an error saying the `Manager` object has no `schedule_meeting` attribute.

# Add a schedule_meeting Method to the Manager Class

1. Add the following to the end of the manager.py file:

```
    def schedule_meeting(self, invitees, time):
        self.meetings.append({"invitees": invitees, "time": time})
        self.meetings.sort(key=lambda m: m["time"])
```

2. Run `using_inheritance.py` again:

```
python3.7 using_inheritance.py
```

Now, we'll see an error saying the `Manager` object has no `run_next_meeting` attribute.

# Add a run_next_meeting Method to the Manager Class

1. Add the following to the end of the ´manager.py´ file:

```
    def run_next_meeting(self):
        return self.meetings.pop(0)
```

2. Run `using_inheritance.py` one last time:

```
python3.7 using_inheritance.py
```

We should see no output if we've implemented the method correctly.

