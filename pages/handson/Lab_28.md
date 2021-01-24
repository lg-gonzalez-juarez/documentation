---
title: 28. Hands-on Lab Adding Exception Handling to a Python Script
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_28.html
folder: handson
---

## Introduction

Our code won't always be able to run without issue. So many things can go wrong when running code — network connectivity can fail, file system permissions can be wrong, bad inputs can be passed to our scripts. Thankfully, we can normally tell when these types of issues might happen in our code and we can handle them. In this hands-on lab, we'll add exception handling to an existing script that can run into many of these issues. To feel comfortable completing this lab, you'll want to know how to perform exception handling in Python (watch the "Handling Exceptions with try, except, else, and finally" video from the Certified Associate in Python Programming Certification course).

## Solution

To work through the lab, you can either log in via a terminal on your local machine and use a text editor in the terminal, or you can use VS Code in the browser. This lab guide will go through the steps using VS Code in the browser.

In order to use VS Code in the browser, navigate to the public IP address of the workstation server (provided on the lab page) on port 8080 (e.g., http://<PUBLIC_IP>:8080).

## Add Exception Handling Around Setting the name Variable

1. In the menu at the top, click **Terminal** > **New Terminal**.

2. Run `exception_handling.py`:

```
python3.7 exception_handling.py
```

We'll get an index error.

3. In the menu at the top, click **File** > **Open**.


4. Select **exception_handling.py**.

5. Edit the `name` variable section to match the following:

```
try:
    name = sys.argv[1]
except IndexError:
    print("Error: please provide a name and a repeat count to the script.")
    sys.exit(1)

# Remainder of file omitted
```

6. Run the script again without any arguments:

```
python3.7 exception_handling.py
```

We should see this error message:

```
Error: please provide a name and a repeat count to the script.
```

7. Run the script with an argument of `Kevin`:

```
python3.7 exception_handling.py Kevin
```

We should see this error message:

```
Traceback (most recent call last):
  File "exception_handling.py", line 16, in <module>
    repeat_count = int(sys.argv[2])
IndexError: list index out of range
```

## Handle Potential ValueError and IndexError When Setting repeat_count Variable

1. Edit the `repeat_count` variable section to match the following:

```
# previous code omitted

try:
    repeat_count = int(sys.argv[2])
except IndexError:
    print("Error: please provide a name and a repeat count to the script.")
    sys.exit(1)
except ValueError:
    print("Error: the repeat count needs to be a number.")
    sys.exit(1)

# remaining code omitted
```

2. Run the script with a new argument added:

```
python3.7 exception_handling.py Kevin bob
```

We'll get an error saying the repeat count needs to be a number.

3. Change `bob` to `10`:

```
python3.7 exception_handling.py Kevin 10
```

This time, we'll get a permissions error.

## Handle Potential File IO Errors When Writing to name_repeated.txt

1. Edit the last four lines in the file to match the following:

```
# previous code omitted

try:
    f = open("root_files/name_repeated.txt", "w")
except (OSError, IOError) as err:
    print("Error: unable to write file (", err, ")")
    for i in range(1, repeat_count + 1):
        print(i, "-", name)
else:
    names = [name + "\n" for i in range(1, repeat_count + 1)]
    f.writelines(names)
    f.close()
```

2. Re-run the same command as before:

```
python3.7 exception_handling.py Kevin 10
```

We'll see the same error, but it will also print the list.

3. Change the owner of the `root_files` directory:

```
sudo chown -R cloud_user:cloud_user ~/root_files/
```

4. Enter the `cloud_user` password at the prompt.

5. List the contents of `root_files`:

```
ls -al root_files/
```

We should see we now own it, so we should be able to write into it.

6. Re-run the command again:

```
python3.7 exception_handling.py Kevin 10
```

We shouldn't get any errors.

7. View the contents of `name_repeated.txt`:

```
cat root_files/name_repeated.txt
```

We should see the name repeated 10 times.
