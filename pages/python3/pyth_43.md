---
title: 43. Modules and Packages
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: pyth_43.html
folder: python3
---
vcbcv 


## 43.1. Creating and Using Python Modules

To have truly reusable code, we need to access functions, variables, and objects that have already been written. Thus we need to have a way to share our code. This is where modules and packages are useful. In this lesson, we demonstrate how to create our first Python module and access its contents from a different Python program.

Documentation 
- [Python Modules Documentation](https://docs.python.org/3/tutorial/modules.html)
- [The import Statement](https://docs.python.org/3/reference/simple_stmts.html#import)

### What Is a Module?

Working with Python it's very easy to define new functions and assign values to variables that we would like to use multiple times. It would be great if we could write these useful pieces of code once and then use them whenever we need them. Thankfully, we can do just that because of modules. In Python, a module is just a Python file. This means that we can use modules to divide our code into logical groupings by putting them into separate modules and then pulling those modules into our scripts or applications when we need them.

### Creating Our First Module
To demonstrate how to create and use modules, let's create a new directory called ```using_modules```. Within it, we'll define our first module by creating the ```using_modules/helpers.py``` file.

```
$ mkdir ~/using_modules
$ cd ~/using_modules
$ touch helpers.py
```

Within ```helpers.py```, we're placing some functions that we think will be generally useful and likely to be used in other files. Let's write a few functions that can manipulate strings. ```~/using_modules/helpers.py```

```
def extract_upper(phrase):
    return list(filter(str.isupper, phrase))

def extract_lower(phrase):
    return list(filter(str.islower, phrase))
```

Now we have two functions defined and we'd like to use them in other scripts and modules.

### Using Our Module from Another Script

For this section of the course, we're going to be putting our example code into a script called main.py. Let's create that script now and look at what we can do to pull in these functions so that we can use them.

The key to working with modules is the [import statement](https://docs.python.org/3/reference/simple_stmts.html#import) . We're going to dig deeper into all that we can do while importing modules in the next lesson. But for now, we're going to leverage the fact that we can import modules in the same directory as our script by referencing them by their file name minus the extension. In our case, this will ```be helpers```.

```
~/using_modules/main.py
```

```
import helpers
```

Before we use our functions, let's make sure that this file is valid by running it.

```
$ python3.7 main.py
$
No output is a good sign. To utilize the functions defined in our module, we'll add a period to the end of our module name (i.e. the file name) and then type the name of our function to call it as we otherwise would.

~/using_modules/main.py

import helpers

name = "Keith Thompson"
print(f"Lowercase letters: {helpers.extract_lower(name)}")
print(f"Uppercase letters: {helpers.extract_upper(name)}")
Let's run this and verify it works as expected.

$ python3.7 main.py
Lowercase letters: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Uppercase letters: ['K', 'T']

```

Perfect! Now we know the simplest way to define and use modules. In the next lesson, we'll dig deeper into the various ways and places that we can import modules.

## 43.2. Importing Modules

Python provides a few different ways to import modules and packages. In this lesson, we'll take a look at how importing works and the various ways we can import definitions from a module.

### Documentation 
- [Python Modules Documentation](https://docs.python.org/3/tutorial/modules.html)
- [The import Statement](https://docs.python.org/3/reference/simple_stmts.html#import)

## The Standard import Statement

When we learned how to create a module, we also learned how to import the module as a singular entity into other Python files. To reiterate this, we use the following format to import an entire module under its namespace.

```
import my_module_name
```

By doing this, we're able to access anything exposed by the module by chaining off of the module's name. Occasionally, we might have a naming conflict when importing a module. In those cases, we can also use the keyword ```as``` in the ```import``` statement to change the identifier that we use to represent the module. Let's change our ```using_modules/main.py``` so that the ```helpers``` module is accessed using the h name.

```
~/using_modules/helpers.py
```

```
import helpers as h

name = "Keith Thompson"
print(f"Lowercase letters: {h.extract_lower(name)}")
print(f"Uppercase letters: {h.extract_upper(name)}")
```

The name of ```h``` isn't great, but it does demonstrate that we can change the name of modules when we import them. If we run this script, we will see there's no difference in the output.

```
$ python3.7 main.py
Lowercase letters: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Uppercase letters: ['K', 'T']
```

### Importing from

More often than not, we don't need to use everything provided by a module. In these cases, we can leverage the ```from``` version of an ```import``` statement to import only the definitions we need from the module, and then we can access them directly. To demonstrate how to do this for multiple functions, let's directly import the functions from our ```helpers``` module. The ```from``` statement works like this:

```
from <MODULE_NAME> import <definition>, <definition>, <etc.>
```

Here's what it looks like in `main.py`:

`~/using_modules/main.py`

```
from helpers import extract_lower, extract_upper

name = "Keith Thompson"
print(f"Lowercase letters: {extract_lower(name)}")
print(f"Uppercase letters: {extract_upper(name)}")
```

It's worth noting that now we don't have access to the ```helpers``` name in our code at all. If we change our ```extract_upper``` line to be chained off of ```helpers``` name it will cause an error.

```
$ python3.7 main.py
Lowercase letters: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Traceback (most recent call last):
  File "using_modules/main.py", line 5, in <module>
    print(f"Uppercase letters: {helpers.extract_upper(name)}")
NameError: name 'helpers' is not defined
```

Lastly, we can also combine the ```as``` keyword with each definition that we're importing to explicitly rename that definition.

`~/using_modules/main.py`

```
from helpers import extract_lower as e_low, extract_upper

name = "Keith Thompson"
print(f"Lowercase letters: {e_low(name)}")
print(f"Uppercase letters: {extract_upper(name)}")
```

### Importing Everything from a Module

The final way we can import definitions from a module is to import all of them at once by using `*`. This is generally not the recommended way of importing things, but sometimes a module provides a lot of functions that we'll be using, and we don't want to explicitly import them one at a time.

Let's utilize the `*` to import our two functions from the `helpers` module without explicitly naming them.

`~/using_modules/main.py`

```
from helpers import *

name = "Keith Thompson"
print(f"Lowercase letters: {extract_lower(name)}")
print(f"Uppercase letters: {extract_upper(name)}")
```

Once again, if we run this, it will work just as it did before.

```
$ python3.7 main.py
Lowercase letters: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Uppercase letters: ['K', 'T']
```


## 43.3. Executing Modules as Scripts


## 43.4. Hiding Module Entities


## 43.5. The Module Search Path


## 43.6. Creating and Using Python Packages


## 43.7. Distributing and Installing Packages


## 43.8. Docstrings, Doctests, and Shebangs









{% include links.html %}
