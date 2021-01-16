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

Python modules are just files, but sometimes we want them to behave slightly differently if they're being run directly. In this lesson, we'll learn about how modules are interpreted when imported and also how to only run code when a module is run directly by using the __name__ variable.

### Documentation 

- [Python Modules Documentation](https://docs.python.org/3/tutorial/modules.html)
- [The import Statement](https://docs.python.org/3/reference/simple_stmts.html#import)
- [The __name__ Variable](https://docs.python.org/3/library/__main__.html)

### Expressions in a Module

Since modules are just Python files, they can contain expressions and the file will be interpreted from top to bottom. So a few good questions to ask ourselves are:

1. When is a module interpreted?
2. Can a module be interpreted twice?

To test this, let's create another module that imports our `helpers` module and also import that new module into our `main.py`. We'll call this module `extras.py`.

`~/using_modules/extras.py`

```
print("Importing 'helpers' in 'extras'")
import helpers

name = "Keith Thompson"
```

In `main.py`, let's import extras.

`~/using_modules/main.py`

```
print("We're importing 'helpers' from 'main'")
from helpers import *

print("We're importing 'extras' from 'main'")
import extras

print(f"Lowercase letters: {extract_lower(extras.name)}")
print(f"Uppercase letters: {extract_upper(extras.name)}")
```

Finally, in `helpers.py` we'll add `print`, so that we can see when it is run and how many times it is run.

`~/using_modules/helpers.py`

```
def extract_upper(phrase):
    return list(filter(str.isupper, phrase))

def extract_lower(phrase):
    return list(filter(str.islower, phrase))

print("HELLO FROM HELPERS")
```

We now have enough print lines to helps us really see how `main.py` is processed and when our modules are interpreted. When we run it, this is what we see:

```
$ python3.7 main.py

We're importing 'helpers' from 'main'
HELLO FROM HELPERS
We're importing 'extras' from 'main'
We're import 'helpers' from 'extras'
Lowercase letters: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Uppercase letters: ['K', 'T']
```

As we can see, the code within the `helpers` module was only interpreted the first time that it was imported. So even though it was imported into two different modules, it was only ever run one time.

### Running a Module Directly

Ideally, we don't want to run this `print` line when our module is imported, but sometimes we do want a module to execute something if it is run directly. To handle this, we can access the `__name__` variable. The `__name__` variable is set in each module and can be used to determine if the module is being run directly as opposed to being imported. Let's change the various print lines from our previous lesson to help us understand the values set to `__name__` in each of our scripts.

`~/using_modules/main.py`

```
from helpers import *
import extras

print(f"__name__ in main.py: {__name__}")

print(f"Lowercase letters: {extract_lower(extras.name)}")
print(f"Uppercase letters: {extract_upper(extras.name)}")
```

`~/using_modules/helpers.py`

```
def extract_upper(phrase):
    return list(filter(str.isupper, phrase))

def extract_lower(phrase):
    return list(filter(str.islower, phrase))

print(f"__name__ in helpers.py: {__name__}")
print("HELLO FROM HELPERS")
```

`~/using_modules/extras.py`

```
import helpers

print(f"__name__ in extras.py: {__name__}")

name = "Keith Thompson"
Here's what we see when we run main.py:
```

`$ python3.7 main.py`

```
__name__ in helpers.py: helpers
HELLO FROM HELPERS
__name__ in extras.py: extras
__name__ in main.py: __main__
Lowercase letters: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Uppercase letters: ['K', 'T']
```

All of the modules that we imported have `__name__` set to the actual module name, but main.py is set to `__main__` because it is running in the main context. A common pattern is to add a condition like this if we want to add functionality to a module only if it is running in the main context:

```
if __name__ == "__main__":
    print("Something only when running in main scope")
```

To demonstrate this, let's remove all of these debugging lines, but move "HELLO FROM HELPERS" into this conditional in `helpers.py`.

(We're only showing the change to `helpers.py`, but we removed all of the `'__name__` in ...' output)

`~/using_modules/helpers.py`


```
def extract_upper(phrase):
    return list(filter(str.isupper, phrase))

def extract_lower(phrase):
    return list(filter(str.islower, phrase))

if __name__ == "__main__":
    print("HELLO FROM HELPERS")
```
If we now run `main.py` we should see the following:

```
$ python3.7 main.py
Lowercase letters: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Uppercase letters: ['K', 'T']
```

If we run `helpers.py` directly, we should see the print line being run.

```
$ python3.7 helpers.py
HELLO FROM HELPERS
```

## 43.4. Hiding Module Entities

Now that we know how to import our modules, we might want to restrict what is exposed. In this lesson, we'll look at how we can hide some of our module's contents from being imported by other modules and scripts.

### Documentation 

[Python Modules Documentation](https://docs.python.org/3/tutorial/modules.html)

### What Are Module Entities?

When we see `module entities`, we need to see `variables`, `functions`, and `classes` (we'll cover classes in the next section). A module entity is anything we provide with a name in our module. As we've seen, these things are importable by name when we used `from <module> import <name>`.

### Using `__all__`

If we want to prevent someone from importing an entity from our module, there aren't very many options. There are only two reasonable things we can do to restrict what is imported if someone uses from `<module> import *`. The first is by setting the `__all__` variable in our module. Let's test this out by setting `__all__` to a list including only `extract_upper` to see what happens in `main.py`.

`~/using_modules/helpers.py`

```
__all__ = ["extract_upper"]

def extract_upper(phrase):
    return list(filter(str.isupper, phrase))

def extract_lower(phrase):
    return list(filter(str.islower, phrase))

if __name__ == "__main__":
    print("HELLO FROM HELPERS")
```

In `main.py`, we had been using both of these functions after loading them with `from helpers import *`. Here's another look at what `main.py` currently looks like.

`~/using_modules/main.py`

```
from helpers import *
import extras

print(f"Lowercase letters: {extract_lower(extras.name)}")
print(f"Uppercase letters: {extract_upper(extras.name)}")
```

With `__all__` set in `helpers`, let's run `main.py` to see what happens.

```
$ python3.7 main.py
Traceback (most recent call last):
  File "main.py", line 4, in <module>
    print(f"Lowercase letters: {extract_lower(extras.name)}")
NameError: name 'extract_lower' is not defined
```

Although `name` exists within `helpers.py`, it is not available in other modules via `from helpers import *`. This does not mean that we can't explicitly import `extract_lower` though. Let's modify `main.py` to import `extract_lower` by name.

`~/using_modules/main.py`

```
from helpers import *
from helpers import extract_lower
import extras

print(f"Lowercase letters: {extract_lower(extras.name)}")
print(f"Uppercase letters: {extract_upper(extras.name)}")
```

Let's run this one more time.

```
$ python3.7 main.py
Lowercase letters: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Uppercase letters: ['K', 'T']
```

While it doesn't allow us to prevent an entity from ever being imported, using `__all__` does provide a way of sometimes restricting what is imported by modules and scripts consuming our modules and packages.

### Using Underscored Entities

The other way we can prevent an entity from being exported automatically when someone uses `from <module> import *` is by making the first character an underscore `(_)`. If we removed `__all__ `from `helpers.py` and created a variable called `_hidden_var = "test"`, we would not have access to `_hidden_var` after running `from helpers import *`.


## 43.5. The Module Search Path

We've seen how to create our modules, and we've been able to import them from scripts adjacent to them in the file system, but where else can we import modules from?

### Documentation 
- [Python Modules Documentation](https://docs.python.org/3/tutorial/modules.html)
- [Python Standard Libary](https://docs.python.org/3/library/)
- [Sys Module](https://docs.python.org/3/library/sys.html)

### Where Do Modules Come From?

Python is a language with a large and powerful [standard library](https://docs.python.org/3/library/) of modules. To use these modules, we need to import them the same way that we've been importing our local modules, but how does Python know where to find the code for these modules? To understand this we need to look at the module search path. When Python goes looking for a module it has a path that works very much like the `PATH` variable used by our shell to find executables. A few different things are combined to make this path:

- The directory containing the running script is automatically the first item in the search path. When running the REPL this will be the current directory.
- The values set in the `PYTHONPATH` environment variable (if it is set) will be next in the list.
- Finally, a list of directories configured when Python was installed. This list contains paths to directories that have the standard library modules and other packages we've installed.

If we want to see the module search path, we can import the [sys](https://docs.python.org/3/library/sys.html) module and view the `path` variable. Let's do this from a REPL.

```
$ python3.7
Python 3.7.6 (default, Jan 29 2020, 21:20:26)
[GCC 4.8.5 20150623 (Red Hat 4.8.5-39)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> sys.path
['', '/home/cloud_user/.pyenv/versions/3.7.6/lib/python37.zip', '/home/cloud_user/.pyenv/versions/3.7.6/lib/python3.7', '/home/cloud_user/.pyenv/versions/3.7.6/lib/python3.7/lib-dynload', '/home/cloud_user/.pyenv/versions/3.7.6/lib/python3.7/site-packages']
>>> exit()
```

Our Python install is in `~/.pyenv/versions/3.7.6`, and the directories within contain the standard library. The `site-packages` directory contains third-party packages that we might install.

Just to show that we can change this, let's set the `PYTHONPATH` environment variable when starting the REPL.

```
$ PYTHONPATH=/home/cloud_user python3.7
Python 3.7.6 (default, Jan 29 2020, 21:20:26)
[GCC 4.8.5 20150623 (Red Hat 4.8.5-39)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> sys.path
['', '/home/cloud_user', '/home/cloud_user/.pyenv/versions/3.7.6/lib/python37.zip', '/home/cloud_user/.pyenv/versions/3.7.6/lib/python3.7', '/home/cloud_user/.pyenv/versions/3.7.6/lib/python3.7/lib-dynload', '/home/cloud_user/.pyenv/versions/3.7.6/lib/python3.7/site-packages']
>>> exit()
```

Now we can see that `/home/cloud_user` is the second item in the list. If we don't have a package in our current directory (the '' in the list), then it will check items passed in via `PYTHONPATH` before looking at items provided by our Python installation.

Note: Python will search for a built-in module by name before searching the paths in `sys.path`. This means you can't accidentally create a module with the same name as a built-in module, which prevents you from overwriting the built-in module.


## 43.6. Creating and Using Python Packages

Python modules are simply Python files, but they are not the only way we can bundle up our code for reuse. Modules are not that easy to share. The primary way we share code is by wrapping our modules into packages. In this lesson, we'll learn what it takes to create a Python package.

### Documentation 

- [Python Packages Documentation](https://docs.python.org/3/tutorial/modules.html#packages)
-[Implicit Namespace Packages](https://www.python.org/dev/peps/pep-0420/#specification)

### What Is a Package in Python?

A package is a namespace that allows us to group modules together. We create a package in Python by creating a directory to hold our modules and adding a special file named `__init__.py`. To show how a package can allow us to organize our code even more, let's create a helpers directory within using_modules. Let's create an empty `__init__.py` file within that directory.

```
$ mkdir ~/using_modules/helpers
$ touch ~/using_modules/helpers/__init__.py
```

The `__init__.py` doesn't need to have anything in it, though we can and will use it later. Next, let's move our `helpers.py` file into the `helpers` directory and change its name to `strings.py` since this file holds helper functions completely focused on working with strings. Our `extras.py` module actually doesn't do anything besides defining variables, so let's move it into `helpers` as `helpers/variables.py`.

```
$ cd ~/using_modules
$ mv helpers.py helpers/strings.py
$ mv extras.py helpers/variables.py
```

We now have a package that contains two modules, but we also broke main.py. Let's change main.py to use our package, instead of the modules that we had before.

`~/using_modules/main.py`

```
from helpers.strings import extract_lower, extract_upper
from helpers import variables
import helpers

print(f"Lowercase letters: {extract_lower(variables.name)}")
print(f"Uppercase letters: {extract_upper(variables.name)}")
print(f"From helpers: {helpers.strings.extract_lower(variables.name)}")
```

The things to note here are that we can access the modules within our packages by importing them directly like with `variables` and by chaining them off of the package name to import entities directly from the child module. Just like we can with a module, we're able to import the package directly.

Running `main.py` again we should see:

```
$ python3.7 main.py
Lowercase letters: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Uppercase letters: ['K', 'T']
From helpers: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
```

### What Does __init__.py Do?

The mysterious `__init__.py` file is used to set up the initialization code for a package, but what does this mean? This means that when the first subpackage or module within the parent package is accessed, then the code within `__init__.py` gets executed. The primary other thing we can do with our `__init__.py` is define the `__all__` value for when we use `from <package> import *`. This doesn't immediately make sense because our `__init__.py` doesn't define anything right now, but we can import parts from our submodules and then make those immediately available if someone imports our package. Let's modify `helpers/__init__.py` to do just that.

`~/using_modules/helpers/__init__.py`

```
__all__ = ['extract_upper']

from .strings import *
```

The syntax of `.strings` allows us to specify that we want to load the strings module within our package, regardless of what our package is named. This is just a way to be a little more explicit. Let's change our `main.py` to use this.

`~/using_modules/main.py`

```
from helpers.strings import extract_lower
from helpers import variables
from helpers import *
import helpers

print(f"Lowercase letters (from strings): {extract_lower(variables.name)}")
print(f"Uppercase letters (from package): {extract_upper(variables.name)}")
print(f"Off of helpers: {helpers.strings.extract_lower(variables.name)}")
```

Once again, let's run our script to see that this code works.

```
$ python3.7 main.py
Lowercase letters (from strings): ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Uppercase letters (from package): ['K', 'T']
Off of helpers: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
```

### Implicit Namespace Packages

While the PCAP syllabus doesn't actually mention implicit namespace packages, it is worth noting that they exist. As of Python 3.3, if we're creating a package that doesn't need to do anything with the `__init__.py`, then we can skip creating the `__init__.py` entirely and our package will work just fine.



## 43.7. Distributing and Installing Packages


## 43.8. Docstrings, Doctests, and Shebangs









{% include links.html %}
