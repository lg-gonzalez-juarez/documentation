---
title: 13. Hands-on Lab Using Pandas Data Frames and Pivot Tables in Python
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_13.html
folder: handson
---

## Introduction

In this hands-on lab, we'll use data frames and pivot tables to analyze some employee information and provide some insight to others on your team.

## Solution

To get started, we need to open our VS Code server, which we will use in this guide: Navigate to our public IP on port 8080: <PublicIP >:8080

## Install Pandas

Before we can use pandas to analyze our employee data, we'll need to make sure that it is installed:

1. Check our version of Python and make sure it is at least 3.8:

```
 python -V
```

2. Download `pandas` using this `pip` command:

```
 python -m pip install pandas
```

## Create a Data Frame

Now that we have pandas installed, we're ready to start using it in our `pay_analysis.py` script. Our pay_analysis.py script already sets up a list of dictionary objects with our employee information named `employee_info`. We need to use this list to create a `pandas.DataFrame` for us to be able to perform our analysis. Let's get the column names from an item in the list and create a new data frame called `employee_frame`:

1. From the Open File Or Folder section, find and open `pay_analysis.py`:

```
 /home/cloud_user/pay_analysis.py
```

2. Add this line at the top of the document:

```
 import pandas as pd
```

3. Add the following lines of code to the end of the document:

```
 columns = employee_info[0].keys()
 employee_frame = pd.DataFrame.from_records(employee_info, columns=columns)

 print(f"Number of Unique Job Titles: {employee_frame.job_title.value_counts().count()}")
```

4. Running the script by using the following:

```
 python pay_analysis.py
```

We get back a message that reads `Number of Unique Job Titles: 183`.

## Use a Pivot Table to Determine the Salary Difference Depending on Gender

To determine the average pay difference between men and women with the same job title, we'll first need to determine which jobs have both men and women doing them:

1. Enter the following code at the end of our `pay_analysis.py` document to create our groups:

```
 job_title_unique_gender_count = employee_frame.groupby('job_title')['gender'].nunique()
```

2. Under this line, we'll enter another line that uses `job_title_unique_gender_count`, then we're going to take all of the items that have a value of 2, drop the items that will be adjusted to a NaN (because they aren't a 2) and then get a `pandas.Index` object with just the names by accessing the `index` of our pandas.Series:

```
 job_titles_with_two_genders = job_title_unique_gender_count.where(job_title_unique_gender_count == 2).dropna().index
```

3. Next, we're going to create a new data frame from our employee_frame data that only contains employees in a job that includes both genders:

```
 job_title_gender_frame = employee_frame[employee_frame.job_title.isin(job_titles_with_two_genders)]
```

4. The last bit of code we use creates a column for each gender in our table, and also adds a column to the table to hold the pay difference between female and male employees:

```python
gender_difference_table = pd.pivot_table(job_title_gender_frame, columns='gender', values=['salary'], index=['job_title'])
gender_difference_table[('salary', 'difference')] = gender_difference_table[('salary', 'Female')] - gender_difference_table[('salary', 'Male')]
print(gender_difference_table)
```

Run our script and see what the table outputs:

```
 python pay_analysis.py
```

We get back a table that looks like this:

```
 Number of Unique Job Titles: 183
                                    salary
 gender                             Female      Male    difference
 job_title
 Account Coordinator          75666.666667   89000.0 -13333.333333
 Account Executive            80333.333333   71500.0   8833.333333
 Account Representative III   50500.000000  100500.0 -50000.000000
 Accountant IV                60500.000000  112000.0 -51500.000000
 Accounting Assistant I      121000.000000   38000.0  83000.000000
 ...                                   ...       ...           ...
 Web Designer II              97333.333333   74000.0  23333.333333
 Web Designer III             82500.000000   60000.0  22500.000000
 Web Designer IV             102000.000000  121000.0 -19000.000000
 Web Developer I             125000.000000   66000.0  59000.000000
 Web Developer II             68666.666667   74000.0  -5333.333333

 [129 rows x 3 columns]
```

## Use a Pivot Table to Determine the Salary Differences Depending on Age

Our final code will make our table categorize each of our employees into an age range. To do this, we'll use the pandas.cut function and add the resulting series as a new column on our employee_frame object, calling it age_range. There are 2 possible categories for each employee to fall under "18 - 40" and "41 - 80". We're going to also add a third, unused category to the list of categories for this column so that we can add a column to our pivot table later:

1. Add our final column:

```
 employee_frame['age_range'] = pd.cut(employee_frame.age, [18, 41, 80], labels=['18 - 40', '41 - 80'])
 employee_frame.age_range.cat.add_categories(['difference'], inplace=True)
```

2. Next, we need to determine while job titles have at least one employee from each of the age ranges:

```
 job_title_unique_age_range_count = employee_frame.groupby('job_title')['age_range'].nunique()
 job_titles_with_two_age_ranges = job_title_unique_age_range_count.where(job_title_unique_age_range_count == 2).dropna().index
 job_title_age_range_frame = employee_frame[employee_frame.job_title.isin(job_titles_with_two_age_ranges)]
```

3. Now that we have a new data frame, we're ready to create our pivot table and populate a new difference column:

```
 age_difference_table = pd.pivot_table(job_title_age_range_frame, columns='age_range', values=['salary'], index=['job_title'])
 age_difference_table[('salary', 'difference')] = age_difference_table[('salary', '18 - 40')] - age_difference_table[('salary', '41 - 80')]
 print(age_difference_table)
```

4. Run the script:

```
 python pay_analysis.py
```

We produce this table:

```
 Number of Unique Job Titles: 183
                                    salary
 gender                             Female      Male    difference
 job_title
 Account Coordinator          75666.666667   89000.0 -13333.333333
 Account Executive            80333.333333   71500.0   8833.333333
 Account Representative III   50500.000000  100500.0 -50000.000000
 Accountant IV                60500.000000  112000.0 -51500.000000
 Accounting Assistant I      121000.000000   38000.0  83000.000000
 ...                                   ...       ...           ...
 Web Designer II              97333.333333   74000.0  23333.333333
 Web Designer III             82500.000000   60000.0  22500.000000
 Web Designer IV             102000.000000  121000.0 -19000.000000
 Web Developer I             125000.000000   66000.0  59000.000000
 Web Developer II             68666.666667   74000.0  -5333.333333

 [129 rows x 3 columns]
                                    salary
 age_range                         18 - 40        41 - 80    difference
 job_title
 Account Coordinator          76800.000000   86285.714286  -9485.714286
 Account Representative I     82000.000000   66000.000000  16000.000000
 Account Representative II   117000.000000   91000.000000  26000.000000
 Account Representative III   38000.000000   88000.000000 -50000.000000
 Accountant I                 99000.000000   80000.000000  19000.000000
 ...                                   ...            ...           ...
 Web Designer II              88666.666667   87000.000000   1666.666667
 Web Designer III             97000.000000   64000.000000  33000.000000
 Web Developer I              66000.000000  125000.000000 -59000.000000
 Web Developer II             43000.000000   89333.333333 -46333.333333
 Web Developer III           118000.000000   58500.000000  59500.000000

 [131 rows x 3 columns]
```