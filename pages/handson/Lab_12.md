---
title: 12. Hands-on Lab Creating a Matrix Using NumPy Arrays
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_12.html
folder: handson
---

## Introduction

In this lab, we're writing a small script that can calculate the revenue numbers for a chain of stores in our local area. Each store sells the same 4 products at the same price. We keep track of the number of sales of each product from each store, and we'd like to use those sales numbers to calculate the total revenue of the business for the month. Thankfully, we can use multi-dimensional arrays and matrices to calculate our values.

## Solution

There are a couple of ways to get in and work with the code. One is to use the credentials provided in the hands-on lab overview page, log in with SSH, and use a text editor in the terminal.

The other is using VS Code in the browser. If you'd like to go this route, you will need to navigate the workstation server's public IP address (provided in the hands-on lab overview page) on port 8080 (example: http://PUBLIC_IP:8080). Your password will be the same password that you'd use to connect over SSH.

## Install Numpy

Before we can start working with NumPy, we'll need to make sure that we have it installed:

1. First, check which Python version we have, making sure it is 3.8.2 or higher:

```
 python -V
```

2. Install NumPy:

```
 pip3.8 install numpy
```

## Creating NumPy Arrays for Each Store's Sales and Item Prices

Since we have the sales numbers for each item from each store, we can create an array for each store's sales that can later be used to make calculations:

1. To get started, we need to create a file to view our revenue:

```
 touch revenue.py
```

2. Using the VS Code Open File or Folder command, open the `revenue.py` file we just created.

3. In here, enter the following to create our array:

```
 import numpy as np

 # Item Positions: Pen, Notebook, Stapler, Backpack
 north_sales = np.array([14, 12, 3, 20])
 east_sales = np.array([9, 5, 23, 10])
 south_sales = np.array([60, 42, 36, 90])
 west_sales = np.array([23, 28, 91, 73])
```

## Create the Sales and Prices Matrix

Because we have 4 different items, each store's sales are stored as a 4-item, one-dimensional array, or a 1x4 matrix. Combine all of our sales variables into a single 4x4 matrix so that we can calculate the revenue for all of the stores at the same time, and create a 4x1 prices matrix that has the `prices` list from top to bottom for `pen`, `notebook`, `stapler`, and `backpack`.

1. Under the code we created in the last step, add the following:

```
 sales = np.vstack([
     north_sales,
     east_sales,
     south_sales,
     west_sales,
 ])

 prices = np.array([
   [1.5],
   [4.25],
   [6.0],
   [25.99]
 ])
 ```

## Calculate Store Revenues and Total Revenue

Calculate the dot product of these two matrices to get the revenue for each store and then utilize those values to calculate the total revenue.

1. Enter in the following code under the code we already created:

```
 revenues = sales @ Prices
 print(f"Revenues: {revenues}")
 print(f"Total Revenue: {sum(revenues)}")
```

2. With the code complete, we need to run it with Python:

```
 python revenue.py
```

3. Review the information that appears.