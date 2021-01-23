---
title: 21. Hands-on Lab Processing Collections in Python Using Lambdas
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_21.html
folder: handson
---
# Introduction

Being able to perform actions on a collection is incredibly useful in any type of programming, and it is pretty common to need to perform a single action on each item. We could do this by using a loop, but there are built-in collection functions that can take a collection and a function or lambda to run each item through. In this hands-on lab, we utilize higher-order functions to process some existing lists by using lambdas.

The `map`, `filter`, `sorted`, and `reversed` functions are great examples of higher-order functions that can receive a function (or lambda) as an argument and do things accordingly. In this hands-on lab, we're going to leverage these functions and lambdas to process some pre-created lists within the `collection_processing.py` script.

# Log In Using VS Code in the Browser

1. Navigate to the provided public IP address on port 8080 (e.g. http://PUBLIC_IP_ADDRESS:8080).

# Create the sorted_by_name List by Sorting the people List of Dictionaries

1. Under the File menu, select Open File....

2. Select the `collection_processing.py` file from the list that appears.

3. Under the Terminal menu, select New Terminal.

4. In the terminal, run the script and observe the error.

```
python3.7 collection_processing.py
```

5. In the `collection_processing.py` file, change line 13 from `sorted_by_name = None` to the following.

```
sorted_by_name = sorted(people, key=lambda d: d['name'].lower())
```

6. In the terminal, run the script and note the error has moved to a different line.

```
python3.7 collection_processing.py
```

# Create the name_declarations List by Mapping over sorted_by_name

1. In the `collection_processing.py` file, change line 28 from `name_declarations = None` to the following.

```
name_declarations = list(
    map(lambda d: f"{d['name']} is {d['age']} years old", sorted_by_name)
)
```

2. In the terminal, run the script and note the error has moved to a different line.

```
python3.7 collection_processing.py
```

# Create the under_seventy List by Filtering and Sorting on the sorted_by_name List

1. In the `collection_processing.py` file, change line 44 from `under_seventy = None` to the following.

```
under_seventy = sorted(
    filter(lambda d: d['age'] < 70, sorted_by_name), key=lambda d: d['age']
)
```

2. In the terminal, run the script and note there are no more errors.

```
python3.7 collection_processing.py
```
