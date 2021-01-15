---
title: 25. Using Matplotlib
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: pyth_05.html
folder: python
---


# Using Matplotlib

## 25.1. What Makes a Good Chart?

### What Makes a Good Chart

Perhaps this section should have been called "Misleading People with Charts".

### Rules for Good Charting
1. Title: Make the title meaningful to the chart and to what the chart shows.
2. Axes: Make sure they do not distort the data.
3. Axes Labels: Should indicate what they show by stating the units. For example, years or miles per hour.
4. Legend: If the chart shows information for more than one data sequence, make sure a legend is provided that shows the differentiation.

Many of these seem like common sense, but representational mistakes can and do happen. Let's look at some examples, as shown in the article by National Geographic, ["A Quick Guide to Spotting Graphics That Lie"](https://www.nationalgeographic.com/news/2015/06/150619-data-points-five-ways-to-lie-with-charts/).


## 25.2. Bar Plots, Histograms, and Scatter Plots

Creating an exceptional chart takes practice. In this lesson, we're going to practice creating a bar plot, a histogram, and a scatter plot! We will be using a dataset that has data appropriate for these types of charts.

### Setup Jupyter Notebooks on Server

Jupyter Notebooks allows you to create and share documents that contain live code, equations, visualizations, and narrative text. We need to set up Jupyter within a code-server by downloading a file:

```
sudo curl -O https://raw.githubusercontent.com/linuxacademy/content-using-pythons-maths-science-and-engineering-libraries/master/jupyter-setup/setup.sh
source setup.sh
```

Check that the server is running Jupyter:

```
systemctl | grep jupyter
```

If it's active and running, it will say so:

```
jupyter.service                                                         
loaded active running   Jupyter Notebook
```

If you don't see that it is, try enabling the service:

```
sudo systemctl enable --now jupyter.service
```

### Matplotlib Setup

```
python -m pip install matplotlib
```

Displaying charts and general operations inside of Jupyter Notebooks requires HTTP rather than an HTTPS protocol. This is a function of using code-server over a remote server.

To enable this function:

```
sudo systemctl enable code-server-http --now 
```

Reload your code server using ```http://<remote-server>:9090```. Please note it must be HTTP, not HTTPS. If you are having trouble loading code-server, please check to make sure you are using ```http``` in the URL.

### Bar Plots

Bar plots are relatively simple and are easy to demonstrate with a few data points.

### Scenario

You are teaching five periods (classes) of Chemistry, and you are curious to see if there appears to be a discrepancy in the classes. So, you decide to use Matplotlib to look at the score averages for the last test by gender.

```
~/chart.py

# %% 
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# create a list for the periods, this is the "x" axis
labels = ["1", "2", "3", "5", "6"]

# create list of the scores you want to plot
boyscores = [32, 67, 90, 100, 92]
girlscores = [40, 74, 90, 92, 100]

# set the width of the bars
width = 0.3

# set the data to be plotted
plt.figure(figsize=(10,5))
y_pos = np.arange(len(labels))
plt.title('Boys and Girls Scores By Period')
plt.xlabel('Periods')
plt.ylabel('Score')
plt.xticks(y_pos, labels)
plt.bar(y_pos, boyscores, width=width, label='boys', color='green', align='center')
plt.bar(y_pos+width, girlscores, width=width, label="girls", color='blue', align='center')
plt.legend(loc='best')
plt.show()
```

## Dataset

Scatter plots and histograms require more data. As a result, we are going to use a dataset we have used before. Information about this dataset is below.

Dataset obtained from Kaggle and created by [Rusty](https://www.kaggle.com/russellyates88).

These datasets were developed from:

- United Nations Development Program (2018): Human development index (HDI) ([Source](http://hdr.undp.org/en/indicators/137506))
- World Bank (2018): World development indicators: GDP (current US$) by country: 1985 to 2016 ([Source](http://hdr.undp.org/en/indicators/137506))
- Szamil from Kaggle (2017): Suicide in the Twenty-First Century dataset ([Source](https://www.kaggle.com/szamil/suicide-in-the-twenty-first-century/notebook))
-World Health Organization (2018): Suicide prevention ([Source](http://www.who.int/mental_health/suicide-prevention/en/))

Download the data file from the repo:

```
! curl -O https://raw.githubusercontent.com/linuxacademy/content-using-pythons-maths-science-and-engineering-libraries/master/hdi_master.csv
```

## Setting Up the Data

To create the environment we need, we should import pandas, NumPy, and Matplotlib from within the Python REPL:

```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

NumPy and pandas can help you isolate the data you want to chart but are not necessary. However, they are usually used to prepare data for charting.

## Histogram

In this example, we create a histogram of the Human Development Index (HDI) for a specific year. We will also examine how to put some statistical information in the plot.

Let's load and read the data, then set the DataFrame:

```
df = pd.read_csv('hdi_master.csv')
```

We are not going to spend time looking at the data as we have seen how to do that in a previous lesson.

```
# pick the year you are interested in looking at
year_of_interest = 2010

# get the data
df_year_interest = df[df['year']==year_of_interest]
# There are null values in the column 'HDI for year', these can be safely ignored
missing_values = df['HDI for year'].isnull()
# filter returns truw for null values, need to negate that to get values
hdi = df_year_interest['HDI for year'][~missing_values]

plt.figure(figsize=(15, 5))
plt.hist(hdi, facecolor='orange', alpha=0.5)
# add mean
plt.axvline(hdi.mean(), color='b', linestyle='solid', linewidth=2, label='mean')
# +1 sd
plt.axvline(hdi.mean() + hdi.std(), color='b', linestyle='dashed', linewidth=2, label='+1 standard deviation')
# -1 sd
plt.axvline(hdi.mean() - hdi.std(), color='b', linestyle='dashed', linewidth=2, label='-1 standard deviation')

plt.title(f'HDI for {year_of_interest}')
plt.xlabel('HDI value')
plt.ylabel('count of specific HDI values')
plt.legend(loc='upper left')
plt.show()
```

## Line Plot and Scatter Plot

In this example, we look at the suicides/100k population using a line plot. Afterward, we look at how easy it is to change the plot by just renaming the plot type to a scatter plot.

```
# create dataframe for male and female
df_male = df[df['sex']=='male'].copy()
df_female = df[df['sex']=='female'].copy()

# Comparison on same graph
suicides_by_male = df_male['suicides/100k pop'].groupby(df['year']).mean().reset_index(level=0)
suicides_by_female = df_female['suicides/100k pop'].groupby(df['year']).mean().reset_index(level=0)
plt.figure(figsize=(15, 5))
# plt.subplot(1,1,1)
plt.plot(suicides_by_male['year'], suicides_by_male['suicides/100k pop'], color='red', alpha=0.5, label='male')
plt.plot(suicides_by_female['year'], suicides_by_female['suicides/100k pop'], color='blue', alpha=0.5, label='female')
plt.title(f'Male and Female Suicide Rates')
plt.xlabel('year')
plt.xticks(rotation=90)
ax = plt.gca()
ax.set_ylim([0, 30])
plt.ylabel('suicides/100k pop')
plt.legend(loc='best')
plt.show()

# group suicide rates by year and plot

suicides_by_male = df_male['suicides/100k pop'].groupby(df['year']).mean().reset_index(level=0) 
suicides_by_female = df_female['suicides/100k pop'].groupby(df['year']).mean().reset_index(level=0)


plt.figure(figsize=(15,5))

plt.subplot(1,2,1)
plt.plot(suicides_by_male['year'], suicides_by_male['suicides/100k pop'], color='blue', alpha=0.5)
plt.title(f'Male Suicide Rates')
plt.xlabel('year')
plt.xticks(rotation=90)
plt.ylabel('suicides/100k pop')
plt.ylim([0, 30])

plt.subplot(1,2,2)
plt.plot(suicides_by_female['year'], suicides_by_female['suicides/100k pop'], color='red', alpha=0.5)
plt.title(f'Female Suicide Rates')
plt.xlabel('year')
plt.xticks(rotation=90)
plt.ylabel('suicides/100k pop')
plt.ylim([0, 30])

plt.show()
```