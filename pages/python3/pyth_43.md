---
title: 43. Modules and Packages
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: pyth_43.html
folder: python3
---
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

For this section of the course, we're going to be putting our example code into a script called `main.py`. Let's create that script now and look at what we can do to pull in these functions so that we can use them.

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
```

No output is a good sign. To utilize the functions defined in our module, we'll add a period to the end of our module name (i.e. the file name) and then type the name of our function to call it as we otherwise would.

`~/using_modules/main.py`

```
import helpers

name = "Keith Thompson"
print(f"Lowercase letters: {helpers.extract_lower(name)}")
print(f"Uppercase letters: {helpers.extract_upper(name)}")
```

Let's run this and verify it works as expected.

```
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

* [Python Modules Documentation](https://docs.python.org/3/tutorial/modules.html)

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
- [Implicit Namespace Packages](https://www.python.org/dev/peps/pep-0420/#specification)

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

Packages are invaluable when working in Python because the community has published a plethora of useful packages that can prevent us from needing to write that code ourselves. Additionally, we can share our own code with others by setting up our packages for distribution.

### Documentation 

- [Distributing Packages and Setuptools](https://packaging.python.org/guides/distributing-packages-using-setuptools/)
- [The Python Package Index](https://pypi.org/)
- [pip](https://pip.pypa.io/en/stable/quickstart/)
- [requests PyPi Page](https://pypi.org/project/requests/)

### Installing Packages

Before we look at how we can go about making our own packages installable, let's cover installing a package from someone else. The primary place we'll be installing packages from will be from the ["Python Package Index"](https://pypi.org/) or ["PyPi"](https://pypi.org/) for short.

To install packages, we'll use [pip](https://pip.pypa.io/en/stable/quickstart/). Let's install one of the most popular Python packages, the [requests](https://pypi.org/project/requests/) package.

```
$ pip3.7 install requests
Collecting requests
  Downloading https://files.pythonhosted.org/packages/51/bd/23c926cd341ea6b7dd0b2a00aba99ae0f828be89d72b2190f27c11d4b7fb/requests-2.22.0-py2.py3-none-any.whl (57kB)
     |????????????????????????????????| 61kB 2.4MB/s
Collecting certifi>=2017.4.17 (from requests)
  Downloading https://files.pythonhosted.org/packages/b9/63/df50cac98ea0d5b006c55a399c3bf1db9da7b5a24de7890bc9cfd5dd9e99/certifi-2019.11.28-py2.py3-none-any.whl (156kB)
     |????????????????????????????????| 163kB 8.0MB/s
Collecting idna<2.9,>=2.5 (from requests)
  Downloading https://files.pythonhosted.org/packages/14/2c/cd551d81dbe15200be1cf41cd03869a46fe7226e7450af7a6545bfc474c9/idna-2.8-py2.py3-none-any.whl (58kB)
     |????????????????????????????????| 61kB 10.8MB/s
Collecting urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 (from requests)
  Downloading https://files.pythonhosted.org/packages/e8/74/6e4f91745020f967d09332bb2b8b9b10090957334692eb88ea4afe91b77f/urllib3-1.25.8-py2.py3-none-any.whl (125kB)
     |????????????????????????????????| 133kB 10.8MB/s
Collecting chardet<3.1.0,>=3.0.2 (from requests)
  Downloading https://files.pythonhosted.org/packages/bc/a9/01ffebfb562e4274b6487b4bb1ddec7ca55ec7510b22e4c51f14098443b8/chardet-3.0.4-py2.py3-none-any.whl (133kB)
     |????????????????????????????????| 143kB 12.8MB/s
Installing collected packages: certifi, idna, urllib3, chardet, requests
Successfully installed certifi-2019.11.28 chardet-3.0.4 idna-2.8 requests-2.22.0 urllib3-1.25.8
$
```

The `requests` package has some dependencies on other packages so `pip` will go ahead and download those dependencies. For the purposes of the PCAP exam, we just need to know how to install packages, but it is definitely worth viewing the other commands provided by `pip` by running `pip --help`.

### Making a Package Installable

To make a package installable, it needs to have a file in the root of the package called `setup.py`. The structure of installable packages can vary, but the presence of a `setup.py` is constant. Let's make our `helpers` package installable by adding a `setup.py` and configuring it using the [setup function](https://packaging.python.org/guides/distributing-packages-using-setuptools/#setup-args). The "Python Packaging Authority" is the working group that maintains the core projects use for Python packaging, and they provide an example project. We're going to take the `setup.py` from that project as a starting point and modify it for our purposes. To begin, we do need to change our `helpers` directory to be the container for our installable package (different than a "python package"). Let's move things around before creating our `setup.py`.

```
$ cd ~/using_modules
$ mkdir -p helpers/src/helpers
$ mv helpers/*.py helpers/src/helpers/
```

Using `tree` on our directory structure for `helpers` will provide us a better way to view our directories. Note that you may have to install tree using `sudo yum install tree`.

```
$ tree helpers
helpers/
     |---> src
           |---> helpers
                |---> __init__.py
                |---> strings.py
                |---> variables.py

2 directories, 3 files
```

The outer `helpers` directory is there just to hold onto our code and isn't actually a Python package. The inner `helpers` will provide the package that can be imported after the distribution of this code is installed. For our code to be installable, we still need a `setup.py` file, which will go in the outer `helpers` directory. Feel free to download it directly using the `curl` command or copy and paste the contents below.

```
$ cd helpers/
$ curl -O https://raw.githubusercontent.com/pypa/sampleproject/master/setup.py
```

Here's what it will look like:

`~/using_modules/helpers/setup.py`

```
from setuptools import setup, find_packages
from os import path

here = path.abspath(path.dirname(__file__))

# Get the long description from the README file
with open(path.join(here, 'README.md'), encoding='utf-8') as f:
    long_description = f.read()

setup(
    name='helpers', # Required
    version='1.0.0', # Required
    description='Our custom collection of helper functions and variables.', # Optional
    # long_description=long_description, # Optional
    # long_description_content_type='text/markdown', # Optional (the README is markdown so we want to set this)
    # url='https://github.com/pypa/sampleproject', # Optional
    author='Keith Thompson',  # Optional
    author_email='keith@linuxacademy.com',  # Optional

    # Classifiers help users find your project by categorizing it.
    #
    # For a list of valid classifiers, see https://pypi.org/classifiers/
    classifiers=[  # Optional
        # How mature is this project? Common values are
        #   3 - Alpha
        #   4 - Beta
        #   5 - Production/Stable
        'Development Status :: 3 - Alpha',

        # Indicate who your project is intended for
        'Intended Audience :: Developers',
        'Topic :: Software Development :: Build Tools',

        # Pick your license as you wish
        'License :: OSI Approved :: MIT License',

        # Specify the Python versions you support here. In particular, ensure
        # that you indicate whether you support Python 2, Python 3 or both.
        # These classifiers are *not* checked by 'pip install'. See instead
        # 'python_requires' below.
        'Programming Language :: Python :: 3',
        'Programming Language :: Python :: 3.5',
        'Programming Language :: Python :: 3.6',
        'Programming Language :: Python :: 3.7',
        'Programming Language :: Python :: 3.8',
    ],
    keywords='helpers',  # Optional

    # When your source code is in a subdirectory under the project root, e.g.
    # `src/`, it is necessary to specify the `package_dir` argument.
    package_dir={'': 'src'},  # Optional

    # You can just specify package directories manually here if your project is
    # simple. Or you can use find_packages().
    #
    # Alternatively, if you just want to distribute a single Python file, use
    # the `py_modules` argument instead as follows, which will expect a file
    # called `my_module.py` to exist:
    #
    #   py_modules=["my_module"],
    #
    packages=find_packages(where='src'),  # Required
    # Specify which Python versions you support. In contrast to the
    # 'Programming Language' classifiers above, 'pip install' will check this
    # and refuse to install the project if the version does not match. If you
    # do not support Python 2, you can simplify this to '>=3.5' or similar, see
    # https://packaging.python.org/guides/distributing-packages-using-setuptools/#python-requires
    python_requires='!=3.0.*, !=3.1.*, !=3.2.*, !=3.3.*, !=3.4.*, <4',

    # This field lists other packages that your project depends on to run.
    # Any package you put here will be installed by pip when your project is
    # installed, so they must be valid existing projects.
    #
    # For an analysis of "install_requires" vs pip's requirements files see:
    # https://packaging.python.org/en/latest/requirements.html
    # install_requires=['peppercorn'],  # Optional

    # List additional groups of dependencies here (e.g. development
    # dependencies). Users will be able to install these using the "extras"
    # syntax, for example:
    #
    #   $ pip install sampleproject[dev]
    #
    # Similar to `install_requires` above, these must be valid existing
    # projects.
    # extras_require={  # Optional
    #     'dev': ['check-manifest'],
    #     'test': ['coverage'],
    # },

    # If there are data files included in your packages that need to be
    # installed, specify them here.
    #
    # If using Python 2.6 or earlier, then these have to be included in
    # MANIFEST.in as well.
    # package_data={  # Optional
    #     'sample': ['package_data.dat'],
    # },

    # Although 'package_data' is the preferred approach, in some case you may
    # need to place data files outside of your packages. See:
    # http://docs.python.org/3.4/distutils/setupscript.html#installing-additional-files
    #
    # In this case, 'data_file' will be installed into '<sys.prefix>/my_data'
    # data_files=[('my_data', ['data/data_file'])],  # Optional

    # To provide executable scripts, use entry points in preference to the
    # "scripts" keyword. Entry points provide cross-platform support and allow
    # `pip` to create the appropriate form of executable for the target
    # platform.
    #
    # For example, the following would provide a command called `sample` which
    # executes the function `main` from this package when invoked:
    # entry_points={  # Optional
    #     'console_scripts': [
    #         'sample=sample:main',
    #     ],
    # },

    # List additional URLs that are relevant to your project as a dict.
    #
    # This field corresponds to the "Project-URL" metadata fields:
    # https://packaging.python.org/specifications/core-metadata/#project-url-multiple-use
    #
    # Examples listed include a pattern for specifying where the package tracks
    # issues, where the source is hosted, where to say thanks to the package
    # maintainers, and where to support the project financially. The key is
    # what's used to render the link text on PyPI.
    # project_urls={  # Optional
    #     'Bug Reports': 'https://github.com/pypa/sampleproject/issues',
    #     'Funding': 'https://donate.pypi.org',
    #     'Say Thanks!': 'http://saythanks.io/to/example',
    #     'Source': 'https://github.com/pypa/sampleproject/',
    # },
)
```


We left a lot of comments in there because they are good to read and understand, but they're for optional fields. Some of the important and potentially confusing lines to look at are the `package_dir` and `packages arguments`. We've put our code into the src directory. We've set these two arguments and used the `find_packages` function from `setuptools` to automatically find the packages that we're providing when someone installs this.

### Building a Distribution

Making code installable in Python means that we need to create a distribution. There are two primary types of distributions: eggs and wheels. Wheels are the modern way to create a distribution and they're a single file that can be installed by pip. They will install any dependencies and place or unpack the source code into the `site-packages` directory for our Python installation. For us to build a wheel distribution, we need to install the `wheel` package and run a command using Python and our `setup.py` file. Let's install wheel first.

```
$ pip3.7 install --upgrade wheel
...
```

Setuptools provides us with multiple different subcommands if we process our `setup.py` through the Python interpreter. Let's take a look at those commands.

```
$ python3.7 setup.py --help
Traceback (most recent call last):
  File "setup.py", line 7, in <module>
    with open(path.join(here, 'README.md'), encoding='utf-8') as f:
FileNotFoundError: [Errno 2] No such file or directory: '/home/cloud_user/using_modules/helpers/README.md'
```

Our `setup.py` specifies that we'll provide documentation in a `README.md` file, but that file doesn't exist, so we can't read it. We'll cover file IO later in the course, but for now, we just need to make sure that that file exists.

```
$ touch README.md
```

Now, let's try again.

```
$ python3.7 setup.py --help
Common commands: (see '--help-commands' for more)

  setup.py build      will build the package underneath 'build/'
  setup.py install    will install the package

Global options:
  --verbose (-v)      run verbosely (default)
  --quiet (-q)        run quietly (turns verbosity off)
  --dry-run (-n)      don't actually do anything
  --help (-h)         show detailed help message
  --no-user-cfg       ignore pydistutils.cfg in your home directory
  --command-packages  list of packages that provide distutils commands

Information display options (just display information, ignore any commands)
  --help-commands     list all available commands
  --name              print package name
  --version (-V)      print package version
  --fullname          print <package name>-<version>
  --author            print the author's name
  --author-email      print the author's email address
  --maintainer        print the maintainer's name
  --maintainer-email  print the maintainer's email address
  --contact           print the maintainer's name if known, else the author's
  --contact-email     print the maintainer's email address if known, else the
                      author's
  --url               print the URL for this package
  --license           print the license of the package
  --licence           alias for --license
  --description       print the package description
  --long-description  print the long package description
  --platforms         print the list of platforms
  --classifiers       print the list of classifiers
  --keywords          print the list of keywords
  --provides          print the list of packages/modules provided
  --requires          print the list of packages/modules required
  --obsoletes         print the list of packages/modules made obsolete

usage: setup.py [global_opts] cmd1 [cmd1_opts] [cmd2 [cmd2_opts] ...]
   or: setup.py --help [cmd1 cmd2 ...]
   or: setup.py --help-commands
   or: setup.py cmd --help
```

This gives us a lot of output, but only the common commands are provided to us. Reading the first line of the output, we can see that the rest of the commands can be shown by using --help-commands instead of `--help`. Let's do that.

```
$ python3.7 setup.py --help-commands
Standard commands:
  build             build everything needed to install
  build_py          "build" pure Python modules (copy to build directory)
  build_ext         build C/C++ extensions (compile/link to build directory)
  build_clib        build C/C++ libraries used by Python extensions
  build_scripts     "build" scripts (copy and fixup #! line)
  clean             clean up temporary files from 'build' command
  install           install everything from build directory
  install_lib       install all Python modules (extensions and pure Python)
  install_headers   install C/C++ header files
  install_scripts   install scripts (Python or otherwise)
  install_data      install data files
  sdist             create a source distribution (tarball, zip file, etc.)
  register          register the distribution with the Python package index
  bdist             create a built (binary) distribution
  bdist_dumb        create a "dumb" built distribution
  bdist_rpm         create an RPM distribution
  bdist_wininst     create an executable installer for MS Windows
  check             perform some checks on the package
  upload            upload binary package to PyPI

Extra commands:
  bdist_wheel       create a wheel distribution
  alias             define a shortcut to invoke one or more commands
  bdist_egg         create an "egg" distribution
  develop           install package in 'development mode'
  dist_info         create a .dist-info directory
  easy_install      Find/get/install Python packages
  egg_info          create a distribution's .egg-info directory
  install_egg_info  Install an .egg-info directory for the package
  rotate            delete older distributions, keeping N newest files
  saveopts          save supplied options to setup.cfg or other config file
  setopt            set an option in setup.cfg or another config file
  test              run unit tests after in-place build
  upload_docs       Upload documentation to PyPI

usage: setup.py [global_opts] cmd1 [cmd1_opts] [cmd2 [cmd2_opts] ...]
   or: setup.py --help [cmd1 cmd2 ...]
   or: setup.py --help-commands
   or: setup.py cmd --help
```

There are plenty of commands in here to play with, but the one that we care about is the extra command `bdist_wheel`. This will build a wheel distribution that will work perfectly with pip. Let's run that now.

```
$ python3.7 setup.py bdist_wheel
running bdist_wheel
running build
running build_py
creating build
creating build/lib
creating build/lib/helpers
copying src/helpers/__init__.py -> build/lib/helpers
copying src/helpers/strings.py -> build/lib/helpers
copying src/helpers/variables.py -> build/lib/helpers
installing to build/bdist.linux-x86_64/wheel
running install
running install_lib
creating build/bdist.linux-x86_64
creating build/bdist.linux-x86_64/wheel
creating build/bdist.linux-x86_64/wheel/helpers
copying build/lib/helpers/__init__.py -> build/bdist.linux-x86_64/wheel/helpers
copying build/lib/helpers/strings.py -> build/bdist.linux-x86_64/wheel/helpers
copying build/lib/helpers/variables.py -> build/bdist.linux-x86_64/wheel/helpers
running install_egg_info
running egg_info
writing src/helpers.egg-info/PKG-INFO
writing dependency_links to src/helpers.egg-info/dependency_links.txt
writing top-level names to src/helpers.egg-info/top_level.txt
reading manifest file 'src/helpers.egg-info/SOURCES.txt'
writing manifest file 'src/helpers.egg-info/SOURCES.txt'
Copying src/helpers.egg-info to build/bdist.linux-x86_64/wheel/helpers-1.0.0-py3.7.egg-info
running install_scripts
creating build/bdist.linux-x86_64/wheel/helpers-1.0.0.dist-info/WHEEL
creating 'dist/helpers-1.0.0-py3-none-any.whl' and adding 'build/bdist.linux-x86_64/wheel' to it
adding 'helpers/__init__.py'
adding 'helpers/strings.py'
adding 'helpers/variables.py'
adding 'helpers-1.0.0.dist-info/METADATA'
adding 'helpers-1.0.0.dist-info/WHEEL'
adding 'helpers-1.0.0.dist-info/top_level.txt'
adding 'helpers-1.0.0.dist-info/RECORD'
removing build/bdist.linux-x86_64/wheel
```

We now have a `build` and `dist` directory inside of the upper `helpers` directory. The artifact that we created will be within the `dist` directory and end with a `.whl` extension.

Going back to `~/using_modules`, we'll actual ly run into issues if we try to run `main.py` right now because there is no `helpers` package local to the file anymore. Here's what we'll see when we run that script:

```
$ cd ~/using_modules
$ python3.7 main.py
Traceback (most recent call last):
  File "main.py", line 1, in <module>
    from helpers.strings import extract_lower
ModuleNotFoundError: No module named 'helpers.strings'
```

To get around this, we'll install our package using `pip` and the wheel we built.

```
$ pip3.7 install helpers/dist/helpers-1.0.0-py3-none-any.whl
Processing ./helpers/dist/helpers-1.0.0-py3-none-any.whl
Installing collected packages: helpers
Successfully installed helpers-1.0.0
```

When we run a script or load the REPL, we can load the `helpers` package and its internal modules.

```
$ python3.7 main.py
Lowercase letters (from strings): ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Uppercase letters (from package): ['K', 'T']
Off of helpers: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
```

Our package is installed and our script runs again without using a module local to the script. We're not going to cover publishing a package to PyPi in this course, but the PyPA documentation also details how to do that.


## 43.8. Docstrings, Doctests, and Shebangs

Now that we've created both modules and packages, we should help the potential users of our code by adding some documentation. Additionally, it's a little cumbersome to continually pass our `main.py` script to the Python executable to run it, so we're going to turn that script into an executable to make using it a little easier.

### Documentation 

- [Python Packages Documentation](https://docs.python.org/3/tutorial/modules.html#packages)
- [Python doctest Module](https://docs.python.org/3/library/doctest.html)

### Documenting Python Code Using Docstrings

In many languages, when we write documentation for our code, it exists in the source code as a comment. Python is a little different because the documentation exists in the code. This official type of documentation is done by adding docstrings to our modules at the top of the file, or within functions, methods, and classes. Docstrings are triple quoted strings (start with `"""` or `'''`) used to write multi-line, structured documentation. To add documentation to a package, we can add a docstring to the top of the package's `__init__.py` file. Let's add some documentation to the `helpers` package.

`~/using_modules/helpers/src/helpers/__init__.py`

```
"""
Helpers is a package that provides easy to use helper functions
and variables.
"""

__all__ = ["extract_upper"]

from .strings import *
```

One of the most common misconceptions in Python is that we just created a "block comment". That's entirely incorrect. We created a multi-line string and the interpreter has to do some work to read that content. An actual comment starts with an `octothorp/hash/`pound sign and the interpreter completely ignores it. In the very specific case of a docstring, this string will actually be assigned to a hidden variable on the package, module, function: the `__doc__` variable. To demonstrate this, we're going to change how we installed our package so that it will pick up code changes as we write them. First, let's uninstall the existing `helpers` package.

Note: Since `pip` matches your Python version, if you are not using `pip 3.7` you can use the `pip -V` command to find its version.

```
$ pip3.7 uninstall -y helpers
Found existing installation: helpers 1.0.0
Uninstalling helpers-1.0.0:
  Successfully uninstalled helpers-1.0.0
```

We can install the package's source so that the changes we make will be available without a reinstall. This is handy in development, but not something we would have other users do.

```
$ cd ~/using_modules/helpers
$ pip3.7 install --editable .
Obtaining file:///home/cloud_user/using_modules/helpers
Installing collected packages: helpers
  Running setup.py develop for helpers
Successfully installed helpers
```

To see that our documentation is accessible in code, let's start the REPL, import our package, and access the `__doc__` variable:

```
$ python3.7
Python 3.7.6 (default, Jan 30 2020, 15:46:02)
[GCC 4.8.5 20150623 (Red Hat 4.8.5-39)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import helpers
>>> helpers.__doc__
'\nHelpers is a package that provides easy to use helper functions\nand variables.\n'
```

Since modules are just Python files, we can do this same thing to document any module we write. To document a function we will create a triple-quoted string at the top of the function body. Let's write some documentation for `extract_upper` now.

`~/using_modules/helpers/src/helpers/strings.py`

```
def extract_upper(phrase):
    """
    extract_upper takes a string and returns a list containing
    only the uppercase characters from the string

    >>> extract_upper("Hello There, BOB")
    ['H', 'T', 'B', 'O', '']
    """
    return list(filter(str.isupper, phrase))

def extract_lower(phrase):
    return list(filter(str.islower, phrase))

if __name__ == "__main__":
    print("HELLO FROM HELPERS")
```

We've now created a docstring for a function. One of the downsides with documenting code is that it is pretty easy for the documentation and the code to get out of sync with one another, and bad documentation helps no one. Thankfully, docstrings can be used by another standard library module called `doctest` that allows us to add what looks like Python REPL lines into our docstrings that will then be evaluated to verify that they produce the expected results. Let's use the `doctest` module on our file to see if our documentation is accurate.

```
$ python3.7 -m doctest src/helpers/strings.py
**********************************************************************
File "src/helpers/strings.py", line 6, in strings.extract_upper
Failed example:
    extract_upper("Hello There, BOB")
Expected:
    ['H', 'T', 'B', 'O', '']
Got:
    ['H', 'T', 'B', 'O', 'B']
**********************************************************************
1 items had failures:
   1 of   1 in strings.extract_upper
***Test Failed*** 1 failures.
```

Our documentation is acting as an automated test and can now help us find regressions in our code and our documentation. In this case, the code works as intended, but there's a typo in the documentation that demonstrates how the code would be used. Let's fix that.

`~/using_modules/helpers/src/helpers/strings.py`

```
def extract_upper(phrase):
    """
    extract_upper takes a string and returns a list containing
    only the uppercase characters from the string

    >>> extract_upper("Hello There, BOB")
    ['H', 'T', 'B', 'O', 'B']
    """
    return list(filter(str.isupper, phrase))

def extract_lower(phrase):
    return list(filter(str.islower, phrase))

if __name__ == "__main__":
    print("HELLO FROM HELPERS")
```

If we run `doctest` again, we should see no output because the results match the expected outcome.

```
$ python3.7 -m doctest src/helpers/strings.py
$
```

### Setting a Shebang for a Script

The last thing we want to do is adjust `main.py`, so that we can run it directly. To do this, we need to do two things:

* Explicitly make it executable using `chmod`.
* Add a shebang to the top of the script so that the proper program will run the script.

Shebangs are useful because they allow us to write scripts in languages other than our shell's language (bash, sh, zsh, etc.). For this to work, we need to add a reference to the executable to use at the top of the file in a special comment called a shebang. From the perspective of Python, a shebang starts like any other comment, but then immediately has an exclamation point. Let's set our script to use the default `python` executable that is currently active in our environment.

`~/using_modules/main.py`

```
#!/usr/bin/env python

from helpers.strings import extract_lower
from helpers import variables
from helpers import *
import helpers

print(f"Lowercase letters (from strings): {extract_lower(variables.name)}")
print(f"Uppercase letters (from package): {extract_upper(variables.name)}")
print(f"Off of helpers: {helpers.strings.extract_lower(variables.name)}")
```

If we make the script exectuable and run it, we should see the usual output without needing to pass it to the Python executable.

```
$ chmod +x ~/using_modules/main.py
$ ~/using_modules/main.py
Lowercase letters (from strings): ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Uppercase letters (from package): ['K', 'T']
Off of helpers: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
```

Using the `env` command followed by the executable we'd normally use is a good approach to setting a shebang for Python. If we want to be explicit about the version of Python to use, then we can use the absolute path. Using our pyenv-installed Python 3.7.6, we would use this path:

`~/using_modules/main.py`

```
#!/home/cloud_user/.pyenv/versions/3.7.6/bin/python

from helpers.strings import extract_lower
from helpers import variables
from helpers import *
import helpers

print(f"Lowercase letters (from strings): {extract_lower(variables.name)}")
print(f"Uppercase letters (from package): {extract_upper(variables.name)}")
print(f"Off of helpers: {helpers.strings.extract_lower(variables.name)}")
```

If we switch our Python back to the system Python and run `main.py`, it will still have access to the `helpers` package which is only installed for version 3.7.6.

```
$ pyenv shell system
$ python -V
Python 2.7.5
$ ~/using_modules/main.py
Lowercase letters (from strings): ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
Uppercase letters (from package): ['K', 'T']
Off of helpers: ['e', 'i', 't', 'h', 'h', 'o', 'm', 'p', 's', 'o', 'n']
```





{% include links.html %}
