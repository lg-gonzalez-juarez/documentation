---
title: 24. Using Pandas
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: pyth_04.html
folder: python2
---

[link](https://linuxacademy.com/cp/modules/view/id/621)

## 24.1. Creating and Using DataFrame

[pandas](https://pandas.pydata.org/pandas-docs/stable/index.html) is a Python package that bundles easy-to-use data structures with data analysis tools. The primary data structure for `pandas` is the [dataframe](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html?highlight=dataframe#pandas.DataFrame). We will be using dataframes throughout this section. A dataframe contains rows and columns and is very similar to a spreadsheet.

`pandas` is very important to data scientists and other operations that involve math, science, and engineering. In this lesson, we focus on dataframes, how we create one, and what information can be determined from the dataframe.

### Install pandas

```powershell
python -m pip install pandas
```

### Creating Dataframes

Dataframes can be made directly from databases, from python lists, and from data files. For this lesson, we will use a python list.

```powershell
>>> import pandas as pd
>>> 
>>> # define the data as a list; made up data for an imaginary vet service
>>> data = [
     ("Dexter","Johnsons","dog","shiba inu","red sesame",1.5,35,"m",False,"both",True),
     ("Alfred","Johnsons","cat","mix","tuxedo",4,12,"m",True,"indoor",True),
     ("Petra","Smith","cat","ragdoll","calico",None,10,"f",False,"both",True),
     ("Ava","Smith","dog","mix","blk/wht",12,32,"f",True,"both",False),
     ("Schroder","Brown","cat","mix","orange",13,15,"m",False,"indoor",True),
     ("Blackbeard","Brown","bird","parrot","multi",5,3,"f",False,"indoor",),
 ]
>>> 
>>> # define the labels
>>> labels = ["name","owner","type","breed","color","age","weight","gender","health issues","indoor/outboor","vaccinated"]
>>> 
>>> # create dataframe
>>> vet_records = pd.DataFrame.from_records(data, columns=labels)
>>> print(vet_records)
         name     owner  type      breed       color   age  weight gender  health issues indoor/outboor vaccinated
0      Dexter  Johnsons   dog  shiba inu  red sesame   1.5      35      m          False           both       True
1      Alfred  Johnsons   cat        mix      tuxedo   4.0      12      m           True         indoor       True
2       Petra     Smith   cat    ragdoll      calico   NaN      10      f          False           both       True
3         Ava     Smith   dog        mix     blk/wht  12.0      32      f           True           both      False
4    Schroder     Brown   cat        mix      orange  13.0      15      m          False         indoor       True
5  Blackbeard     Brown  bird     parrot       multi   5.0       3      f          False         indoor       None
>>>
```

### A Note of Caution

Changes and updates to a dataframe are only permanent if saved to the dataframe. So for example we might say `vet_records = ...` to permanently change the dataframe vet_records. In many cases keeping a reference dataframe is a good practice. For example, `vet_records_dogs = vet_records[vet_records.type=="dog"]` instead of `vet_records = vet_records[vet_records.type=="dog"]`. This will leave you with a dataframe to reference that contains the unaltered data.

### Examining Dataframes

You may often create a dataframe with little to no idea of what the data actually looks like. Enter `head()` and `tail()`.

```powershell
>>> vet_records.head()
       name     owner type      breed       color   age  weight gender  health issues indoor/outdoor vaccinated
0    Dexter  Johnsons  dog  shiba inu  red sesame   1.5      35      m          False           both       True
1    Alfred  Johnsons  cat        mix      tuxedo   4.0      12      m           True         indoor       True
2     Petra     Smith  cat    ragdoll      calico   NaN      10      f          False           both       True
3       Ava     Smith  dog        mix     blk/wht  12.0      32      f           True           both      False
4  Schroder     Brown  cat        mix      orange  13.0      15      m          False         indoor       True
>>> vet_records.tail()
         name     owner  type    breed    color   age  weight gender  health issues indoor/outdoor vaccinated
1      Alfred  Johnsons   cat      mix   tuxedo   4.0      12      m           True         indoor       True
2       Petra     Smith   cat  ragdoll   calico   NaN      10      f          False           both       True
3         Ava     Smith   dog      mix  blk/wht  12.0      32      f           True           both      False
4    Schroder     Brown   cat      mix   orange  13.0      15      m          False         indoor       True
5  Blackbeard     Brown  bird   parrot    multi   5.0       3      f          False         indoor       None
>>>
```

### dtypes

dtypes show you the types of data in the dataframe by column. If the `dtype` is `object`, this indicates that `pandas` is seeing that data as more than one type.

```powershell
>>> vet_records.dtypes
name               object
owner              object
type               object
breed              object
color              object
age               float64
weight              int64
gender             object
health issues        bool
indoor/outdoor     object
vaccinated         object
dtype: object
>>>
```

Notice all the string columns are listed as an object. This is because a string type takes a maximum length argument; during imports, that information is not available, so they are imported as an object so they can be variable length.

### Grouping and Counting Data

Using counting and grouping can help you get a better grasp of the data.

We can count how many records we have for a specific column.

```powershell
>>> vet_records.type.count()
6
>>>
```

However, it is important to remember that pandas ignores missing data. For example, we have a missing age and a missing vaccinated value.

```powershell
>>> vet_records.vaccinated
0     True
1     True
2     True
3    False
4     True
5     None
Name: vaccinated, dtype: object
>>> vet_records.vaccinated.count()
5
>>> vet_records.age.count()
5
>>>
```

We will understand why `pandas` ignores missing values later.

### groupby()

[groupby()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.groupby.html?highlight=groupby#pandas.DataFrame.groupby) can be used to aggregate data based on a column; in this case, we are going to use `type` to aggregate and then count.

```powershell
>>> vet_records.groupby('type').count()
      name  owner  breed  color  age  weight  gender  health issues  indoor/outboor  vaccinated
type                                                                                           
bird     1      1      1      1    1       1       1              1               1           0
cat      3      3      3      3    2       3       3              3               3           3
dog      2      2      2      2    2       2       2              2               2           2
>>>
```

Notice that `count()` counted each value based on based on `type`. Most times, you just want a simple count; `value_counts()` does just that.

```powershell
>>> vet_records.type.value_counts()
cat     3
dog     2
bird    1
Name: type, dtype: int64
>>> 
```


## 24.2. Slicing and Dicing DataFrame

## 24.3. Creating Pivot Tables

## 24.4. Stats With Dataframes


## Hands on 24-
https://app.linuxacademy.com/hands-on-labs/fc56cb34-866b-4f0c-9841-b119b59b97d1?redirect_uri=https:%2F%2Flinuxacademy.com%2Fcp%2Fmodules%2Fview%2Fid%2F621

{% include links.html %}
