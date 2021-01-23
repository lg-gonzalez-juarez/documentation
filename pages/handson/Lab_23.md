---
title: 23. Hands-on Lab Creating a Python Module
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_23.html
folder: handson
---

# Introduction

Being able to reuse code is incredibly useful, but to make our code even more useful, we need to bundle it up so that it can be used from other programs. The primary way this is done in Python is by using modules. In this hands-on lab, we'll define and use our custom module and built-in modules to ensure the using_modules.py file can execute properly.

# Scenario

We already have a file called `using_modules.py` that we need to add imports to so that we can run it without error by running the following:

```
$ python3.7 using_modules.py
$
```

We need to use the built-in `math` module and create the `strhelpers` module that contains a few different functions. By running the `using_modules.py` file, we'll see the errors preventing the file from running and that can guide us towards the changes we need to make. To implement the functions in `strhelpers`, we'll want to use the `random.shuffle` function.

# Log In Using VS Code in the Browser

Navigate to the provided public IP address on port 8080 (e.g. http://PUBLIC_IP_ADDRESS:8080).

# Import the math Module within using_modules.py

1. Under the **File** menu, select **Open File**....

2. Select the `using_modules.py` file from the list that appears.

3. Under the **Terminal** menu, select **New Terminal**.

4. In the terminal, run the script and observe the error.

```
python3.7 using_modules.py
```

5. Add the following to the code under the comment to import the `math` module.

```
import math
```
6. Save the changes.

7. Rerun the script in the terminal and observe the new error.

```
python3.7 using_modules.py
```

# Create the `strhelpers` Module and Implement the `reverse` Function

1. Under the File menu, select New File.

2. Save the file as `strhelpers.py`.

3. Add the following code to the file.

```
def reverse (str_value):
    return str_value[::-1]
```

4. Save the changes.

5. Navigate back to the `using_modules.py` file.

6. Add the following code under the comment describing the second task and before the `name` variable is assigned.

```
from strhelpers import reverse
```

7. Save the changes.

8. Rerun the script in the terminal and observe the new error.

```
python3.7 using_modules.py
```

# Implement str_shuffle and Import It As shuffle

1. Navigate back to the `strhelpers.py` file.

2. Add the following code to the top of the file.

```
from random import shuffle as l_shuffle
```

3. Add the following code to the bottom of the file.

```
def str_shuffle(str_value):
    str_list = list(str_value)
    l_shuffle(str_list)
    return "".join(str_list)
```
4. Save the changes.

5. Navigate back to the `using_modules.py` file.

6. Change the line added in the previous task (`from strhelpers import reverse`) to the following.

```
from strhelpers import reverse, str_shuffle as shuffle
```

7. Save the changes.

8. Rerun the script in the terminal and verify there are no errors.

```
python3.7 using_modules.py
```

