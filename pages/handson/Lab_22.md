---
title: 22. Hands-on Lab Using Python Conditional Expressions
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_22.html
folder: handson
---

# Introduction

We need to constantly evaluate a condition of some kind to determine what action to take or what value to assign to a variable we'll use later in our program. In the situation where we only have an `if` and an `else`, and the body of each branch contains only one expression, then we're able to use a conditional expression. Conditional expressions can be used to succinctly express a simple conditional. In this hands-on lab, we'll be refactoring an existing script by rewriting the simple conditional statements as conditional expressions.

# Scenario

Because we're refactoring an existing script, our goal is to not change what happens when we run the script. To run `process_name.py`, we'll pass it to our Python interpreter and then answer a few questions.

```
$ python3.7 processing_items.py
What is your first name? Keith
Your name is shorter than the average first name in the United States
The first letter of your name is not among the five most common
K is a consonant
e is a vowel
i is a vowel
t is a consonant
h is a consonant
```

We're going to rewrite the conditional statements that are used in the `process_name.py` script to be conditional expressions instead. We're able to do this only because each branch in the conditionals has just one expression.

# Log In Using VS Code in the Browser

1. Navigate to the provided public IP address on port 8080 (e.g. http://PUBLIC_IP_ADDRESS:8080).

# Call print with a Different String Using a Single Conditional Expression

1. Under the File menu, select Open File....

2. Select the `process_name.py` file from the list that appears.

3. Under the Terminal menu, select New Terminal.

4. In the terminal, run the script.

```
python3.7 process_name.py
```

5. Enter your name and examine the results.

6. Change the code under the first task description to the following.

```
print(
    "Your name is as long or longer than the average first name in the United States"
) if len(name) >= 6 else print (
    "Your name is shorter than the average first name in the United States"
)
```

7. Save the changes.

8. Rerun the script in the terminal and verify the results using names of various length.

```
python3.7 process_name.py
```

# Assign a Value to the message Variable Based on a Conditional Expression

1. Change the code under the second task description to the following.

```
message = (
    "The first letter in your name is among the five most common"
    if name[0].lower() in ["a", "j", "m", "e", "l"]
    else "The first letter of your name is not among the five most common"
)
```

2. Save the changes.

3. Rerun the script in the terminal and verify the results using different names.

```
python3.7 process_name.py
```

# Change the String Passed to the print Function Using a Conditional Expression

1. Change the code under the third task description to the following.

```
for letter in name:
    print(
        f"{letter} {'is a vowel' if letter.lower() in ['a', 'e', 'i', 'o', 'u'] else 'is a consonant'}"
    )
```

2. Save the changes.

3. Rerun the script in the terminal and verify the results using different names.

```
python3.7 process_name.py
```