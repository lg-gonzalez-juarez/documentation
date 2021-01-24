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

I think it is important to remind you of the caution from the previous lesson:

Changes and updates to a DataFrame is only permanent if saved to the DataFrame. For example, we might say `vet_records = ...` to permanently change the DataFrame `vet_records`. In many cases, keeping a reference DataFrame is a good practice. For example, `vet_records_dogs = vet_records[vet_records.type=="dog"]` instead of `vet_records = vet_records[vet_records.type=="dog"]`, leaves you with a DataFrame to reference the unaltered data.

I encourage you to always leave a copy of the unaltered DataFrame that does not get used. There are times when I have made changes and then wished I had the original data.

With that remark, let's make a copy of `vet_records` that will be an archive.

```powershell
>>> vet_records_archive = vet_records
>>> vet_records_archive
         name     owner  type      breed       color   age  weight gender  health issues indoor/outdoor vaccinated
0      Dexter  Johnsons   dog  shiba inu  red sesame   1.5      35      m          False           both       True
1      Alfred  Johnsons   cat        mix      tuxedo   4.0      12      m           True         indoor       True
2       Petra     Smith   cat    ragdoll      calico   NaN      10      f          False           both       True
3         Ava     Smith   dog        mix     blk/wht  12.0      32      f           True           both      False
4    Schroder     Brown   cat        mix      orange  13.0      15      m          False         indoor       True
5  Blackbeard     Brown  bird     parrot       multi   5.0       3      f          False         indoor       None
>>> 
```

### Slicing (Filtering) Data

Slicing data, that is, filtering parts of the DataFrame is easy with pandas. It functions very similar to slicing lists in Python. The benefit is that you can use named columns.

Let's get the weight column:

```powershell
>>> # Create a pandas series from the DataFrame
>>> weight = vet_records['weight']
>>> weight
0    35
1    12
2    10
3    32
4    15
5     3
Name: weight, dtype: int64
>>> 
```

That was easy to do! However, we have a list of weights with no context of who they belong to. That is fine if we are doing research on just weight values, but you usually need more context. We can get specific data, such as the weight of a dog.

```powershell
### Boolean Filter
>>> # Collect the dog weights only using a boolean filter
>>> dog_weight = vet_records.weight[vet_records.type=='dog']
>>> dog_weight
0    35
3    32
Name: weight, dtype: int64
>>> 
```

Notice how I used boolean to filter this for just the dog weights. In this case, it evaluated if the weight was associated with the type "dog"; if that evaluated to `True`, then the weight was included.

We can get all the data for dogs:

```powershell
>>> dogs = vet_records[vet_records.type=='dog']
>>> dogs
     name     owner type      breed       color   age  weight gender  health issues indoor/outdoor vaccinated
0  Dexter  Johnsons  dog  shiba inu  red sesame   1.5      35      m          False           both       True
3     Ava     Smith  dog        mix     blk/wht  12.0      32      f           True           both      False
>>> 
```

Notice this is still a boolean filter, `vet_records.type=='dog'` returns a `True` or `False`.

### loc and iloc

* `loc` allows you to use column names to slice data
* `iloc` requires the use of index numbers. (Example: `.iloc[row, column]`) 
  Remember: Python indexes starting at 0.

We can use `loc` to get the name and owner of each pet.

```powershell
>>> vet_records.loc[:,["name", "owner"]]
         name     owner
0      Dexter  Johnsons
1      Alfred  Johnsons
2       Petra     Smith
3         Ava     Smith
4    Schroder     Brown
5  Blackbeard     Brown
>>> 
```

We can also get just the third and fourth record.

```powershell
>>> vet_records.loc[2:3,["name", "owner"]]
    name  owner
2  Petra  Smith
3    Ava  Smith
>>> 
```

Using `iloc` means we use indexes to filter our data. Let's get the color and age of the third and fourth pet. The third pet (Petra) will be a row index of 2, and the fourth pet (Ava) has a row index of 3. If we examine the `vet_records` DataFrame, we will see that the color index is 4, and the age index is 5.

```powershell
>>> vet_records.iloc[[2,3],[4,5]]
     color   age
2   calico   NaN
3  blk/wht  12.0
>>>
```

### isin

`.isin` can be used to gather data about a list of items. For example, let's get the data for "Dexter" and "Blackbeard".

```powershell
>>> vet_records[vet_records.name.isin(['Dexter','Blackbeard'])]
         name     owner  type      breed       color  age  weight gender  health issues indoor/outdoor vaccinated
0      Dexter  Johnsons   dog  shiba inu  red sesame  1.5      35      m          False           both       True
5  Blackbeard     Brown  bird     parrot       multi  5.0       3      f          False         indoor       None
>>> 
```

The tilde symbol `(~)` can be used as the logical NOT operator. This means we ask for all pets excluding Dexter or Blackbeard:

```powershell
>>> vet_records[~vet_records.name.isin(['Dexter','Blackbeard'])]
       name     owner type    breed    color   age  weight gender  health issues indoor/outdoor vaccinated
1    Alfred  Johnsons  cat      mix   tuxedo   4.0      12      m           True         indoor       True
2     Petra     Smith  cat  ragdoll   calico   NaN      10      f          False           both       True
3       Ava     Smith  dog      mix  blk/wht  12.0      32      f           True           both      False
4  Schroder     Brown  cat      mix   orange  13.0      15      m          False         indoor       True
>>> 
```

## 24.3. Creating Pivot Tables

## 24.4. Stats With Dataframes


## Hands on 24-
https://app.linuxacademy.com/hands-on-labs/fc56cb34-866b-4f0c-9841-b119b59b97d1?redirect_uri=https:%2F%2Flinuxacademy.com%2Fcp%2Fmodules%2Fview%2Fid%2F621

{% include links.html %}
