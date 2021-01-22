---
title: 14. Hands-on Lab Creating Graphs with Matplotlib
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_14.html
folder: handson
---

# Introduction

Matplotlib is a popular and powerful library for plotting out information using Python. Since Python often works with datasets, and visually representing data can help demonstrate points within data, it makes sense that there is a useful Python library for just that. In this hands-on lab, we'll utilize matplotlib to create graphs to display various pieces of information about Target stores opened in the United States.

Warning: This is a lab designed as part of a professional-level course and is difficult. The lab asks you to accomplish something using methods and functionality of the matplotlib library that might not have been covered in lessons.

To feel comfortable completing this lab, you'll want to know how to do the following:

* Use Matplotlib. Watch the lessons in the "Using Matplotlib" section from this course.
* Be comfortable reading the matplotlib documentation to find new functions and methods to use to accomplish your goal.

# Solution

Open a new tab in your browser and navigate to the public IP address provided on the hands-on lab, specifying port 9090:

`http://PUBLIC_IP:9090`

Provide the password:
`24bdf4febea54a8579305316`

Note: This password is system generated. If this has changed, you may need to log in to the server using SSH and display the password in the config.yaml file:

```
cat ~/.config/code-server/config.yaml
```

## Install matplotlib

1. At the Welcome page, click the dropdown menu in the top-left of the page. It will look like three lines and can be found directly to the left of the tab with the filename Welcome.
2. Hover your mouse over Terminal and then select New Terminal in the sub-menu.
3. A new terminal window will open in the bottom of your screen.
4. Check your Python version:

```
python -V
```

5. Install matplotlib using pip:

```
python -m pip install matplotlib
```

# Create a Bar Graph Showing Number of Stores by State

1. On the Welcome page, click Open folder....
2. In the selection box, click target_graphs.py.
3. Navigate to the bottom of the file and paste the following code in the # 1) Create Bar Graph Showing Number of Stores by State/Subdivision section:

```
# %%
import matplotlib.pyplot as plt
import numpy as np
from itertools import groupby

subdivision_counts = {}
for subdiv, group in groupby(targets, lambda t: t["Address.Subdivision"]):
    if not subdivision_counts.get(subdiv):
        subdivision_counts[subdiv] = sum(1 for _ in group)
    else:
        subdivision_counts[subdiv] += sum(1 for _ in group)

subdivisions = sorted(subdivision_counts.keys())
values = [subdivision_counts[key] for key in subdivisions]

fig, ax = plt.subplots()
ax.barh(subdivisions, values)
ax.set_xlabel("Number of Stores")
ax.set_ylabel("State")
ax.set_yticklabels(subdivisions, fontsize=4)
ax.invert_yaxis()
ax.set_title("Stores by State")
fig.show()
```

4. At the top of the file, add a new line and enter the following on line 1:

```
# %%
```

5. Click Run Cell when the option appears above line 1. You will need to hit Enter when Jupyter Notebooks prompts for a password.

6. Once that has finished running, navigate back to the code we entered at the bottom of the file and click Run Cell above the code we entered in the # 1) section.

# Create a Line Graph Showing New Stores Opened Each Year

1. Add a new line in the # 2) section and paste in the following code:

```
# %%

stores_open_by_year = {}
for year, group in groupby(targets, lambda t: t["LocationMilestones.OpenDate"].year):
    if not stores_open_by_year.get(year):
        stores_open_by_year[year] = sum(1 for _ in group)
    else:
        stores_open_by_year[year] += sum(1 for _ in group)

years = sorted(stores_open_by_year.keys())
values = [stores_open_by_year[year] for year in years]

fig2, ax = plt.subplots()
ax.plot(years, values)
ax.set_xlabel("Year")
ax.set_ylabel("Number of New Stores")
ax.set_title("New Stores Opened by Year")
fig2.show()
```

2. Click Run Cell when the option appears above the code we just entered.

# Create a Line Graph Showing the Total Number of Target Stores Over Time

1. Add a new line in the # 3) section and paste in the following code:

```
# %%
total = 0
total_by_year = []
for year in years:
    stores_opened = stores_open_by_year[year]
    total += stores_opened
    total_by_year.append(total)

fig3, ax = plt.subplots()
ax.plot(years, total_by_year)
ax.set_xlabel("Year")
ax.set_ylabel("Number of Stores")
ax.set_title("Number of Stores Over Time")
fig3.show()
```

2. Click Run Cell when the option appears above the code we just entered