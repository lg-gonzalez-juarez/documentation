---
title: 24. Hands-on Lab Creating a Python Package
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_24.html
folder: handson
---

# Introduction

Modules are the main way we share code in Python, but modules are almost always shared as a part of a package. In this hands-on lab, we'll create an installable package that contains a module and exposes some functions directly through the package itself. To feel comfortable completing this lab, you'll want to know how to create and use packages (watch the "Creating and Using Packages" video from the Certified Associate in Python Programming Certification course), as well as how to make an installable package and install packages (watch the "Distributing and Installing Packages" video from the Certified Associate in Python Programming Certification course).

# Solution

To work through the lab, you can either log in via a terminal on your local machine and use a text editor in the terminal, or you can use VS Code in the browser. This lab guide will go through the steps using VS Code in the browser.

In order to use VS Code in the browser, navigate to the public IP address of the workstation server (provided on the lab page) on port 8080 (e.g., http://<PUBLIC_IP>:8080).

# Create the Folder Structure for the words Package within the ~/packages Directory

1. In the menu at the top, click **Terminal** > **New Terminal**.

2. In the terminal section, create the `~/packages/words/src/` directory:

```
mkdir -p ~/packages/words/src/words
```

3. Move the `~/generator.py` file to the newly created directory:

```
mv ~/generator.py ~/packages/words/src/words/
```

4. Create the `setup.py` file:

```
touch ~/packages/words/setup.py
```

5. Create the __init__.py file:

```
touch ~/packages/words/src/words/__init__.py
```

# Write the random_word and random_words Functions within the words.generator Module

1. Click Open Folder.

2. Open the `~/packages/words/` folder.

3. Click to expand `src`.

4. Click to open the `generator.py` file.

5. Add the following lines to the bottom:

```
def random_word():
    return random_words(1)[0]

def random_words(length):
    return sample(WORD_LIST, length)
```

# Customize ~/packages/words/src/words/__init__.py to Provide the random_words Function

1. Click to open the ~/packages/words/src/words/\_\_init\_\_.py file.

2. Add the following to the file:

```
__all__ = ["random_words"]
from .generator import *
```

# Write the setup.py, Build a Wheel, and Install the Package Using pip

1. Click to open the `~/packages/words/setup.py` file.

2. Add the following to the file:

```
from setuptools import find_packages, setup

setup(
    name="words",
    version="1.0.0",
    description="Helper library for working with random words",
    package_dir={"": "src"},
    packages=find_packages(where="src"),
)
```

3. In the terminal section, if you aren't already in the `~/packages/words` directory, change to it:

```
cd ~/packages/words
```

4. Install wheel:

```
pip3.7 install --user --upgrade wheel
```

5. Build a wheel for our package:

```
python3.7 setup.py bdist_wheel
```

6. Install our package using `pip`:

```
pip3.7 install --user ~/packages/words/dist/words-1.0.0-py3-none-any.whl
```

7. Change to the root directory:

```
cd ~
```

8. Run the `~/using_packages.py` script:

```
python3.7 using_packages.py
```

You should then see a list of random words.
