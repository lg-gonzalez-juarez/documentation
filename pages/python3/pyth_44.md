---
title: 44. Classes and Object-Oriented Programming
tags: [python]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: pyth_44.html
folder: python3
---

## 44.1. What is an Object?

Python is an object-oriented programming language and that means we work primarily with `objects`. In this lesson, we'll take a closer look at what an object is.

### Documentation 

[Python Classes Documentation](https://docs.python.org/3/tutorial/classes.html)

### What Is an Object?

Objects can be a little confusing, but a good way to think about objects is that they are entities encompassing data and functionality. Let's take a look at the built-in types we've been using to look at the data and functionality encompassed by them. Custom object types are more complex than the built-in types, but looking at the primitive types will help us understand objects from a high level.

For strings (the `str` type), the primary data that we interact with is the string itself, but that doesn't mean it's the only value a string encompasses. When we talk about the functionality an object encompasses, we mean the methods that the object has access to. We've seen a lot of methods on strings, such as `lower` and `upper`.

Thankfully, we can see everything an object encompasses by using the [dir](https://docs.python.org/3.3/library/functions.html#dir) built-in function. Let's take a look at a string in the REPL:

```
$ python3.7
Python 3.7.6 (default, Jan 30 2020, 15:46:02)
[GCC 4.8.5 20150623 (Red Hat 4.8.5-39)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> my_str = "Test String"
>>> dir(my_str)
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattr
ibute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '_
_len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rm
ul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode',
'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit'
, 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstri
p', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitline
s', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```

The [dir function](https://docs.python.org/3.3/library/functions.html#dir) returns a list of all of the variables and functions that the object encompasses. We can chain any of these items off of our object and it will return a value. That value might be a method.

```
>>> my_str.__doc__
"str(object='') -> str\nstr(bytes_or_buffer[, encoding[, errors]]) -> str\n\nCreate a new string object from the given object. If encoding or\nerrors is specified, then the object must expose a data buffer\nthat will be decoded using the given encoding and error handler.\nOtherwise, returns the result of object.__str__() (if defined)\nor repr(object).\nencoding defaults to sys.getdefaultencoding().\nerrors defaults to 'strict'."
>>> my_str.isdigit
<built-in method isdigit of str object at 0x7f7fc84c11f0>
>>> my_str.isdigit()
False
```

We can see the documentation for the `str` type and even access the methods from the object. A good way to tell if something is an object is to try to assign it to a variable. All objects can be assigned to variables.

## 44.2. Creating and Using Python Classes

The next step in our programming journey requires us to think about how we can model concepts from our problem. To do that, we'll often use classes to create completely new data types. In this lesson, we'll create our very first class and learn how to work with its data and functionality.

### Python Documentation 

[Classes](https://docs.python.org/3/tutorial/classes.html#classes)

### Defining New Types

Up to this point, we've been working with the built-in types that Python provides (e.g. `str`, `int`, `float`), but when we're modeling problems in our programs we often want more complex objects that fit our specific problem's domain. For instance, if we were writing a program to model information about vehicles for an automotive shop, then it would make sense for us to have an object type that represents a vehicle. This is where we will start working with classes.

From this point on, most of the code that we'll be writing will be in files. Let's create a `python_objects` directory to hold these files that are only there to facilitate learning.

```
$ mkdir ~/python_objects
$ cd ~/python_objects
```

### Creating Our First Class

For this lesson, we'll use a file called `vehicle.py`. Our goal is to model a vehicle that has tires and an engine. To create a `class` we use the class keyword, followed by a name for the class, starting with a capital letter. Let's create our first class, the `Vehicle` class:

`~/python_objects/vehicle.py`

```
class Vehicle:
    """
    Docstring describing the class
    """

    def __init__(self):
        """
        Docstring describing the method
        """
        pass
```

This is an incredibly simple class. A few things to note here are that by adding a triple-quoted string right under the definition of the class, and also right under the definition of a method or function, we can add documentation. This documentation is nice because we can add examples in this string to run as tests to help ensure our documentation stays up-to-date with the implementation.

A method is a function defined within the context of an object, and Python classes can define special functions that start with double underscores `__`, such as the `__init__`method. This method is the initializer for our class, and it is where we customize what happens when a new instance is being created. In practice, this method will usually just set attributes on the instance. The initializer is what is used when we create a new version of our class by running code like this:

```
>>> my_vehicle = Vehicle()
```

We would like our `Vehicle` class to hold a few pieces of data such as the tires and an engine. For the time being, we're going to have those be a list containing a string for the tires and a string for the engine. Let's modify our `__init__` method to have the `engine` and `tires` parameters:

`~/python_objects/vehicle.py`

```
class Vehicle:
    """
    Vehicle models a vehicle w/ tires and an engine
    """

    def __init__(self, engine, tires):
        self.engine = engine
        self.tires = tires
```

### What Is self?

A big change from writing functions to writing methods is the presence of `self`. This variable references the individual instance of the class that we're working with. The `Vehicle` class holds onto the information about vehicles within our program, where an instance of the `Vehicle` class could represent a specific vehicle like my Honda Civic. Let's load our class into the REPL using `python3.7 -i vehicle.py`, and then create a specific instance of my Honda Civic.

```
$ python3.7 -i vehicle.py
>>> civic = Vehicle('4-cylinder', ['front-driver', 'front-passenger', 'rear-driver', 'rear-passenger'])
>>> civic.tires
['front-driver', 'front-passenger', 'rear-driver', 'rear-passenger']
>>> civic.engine
'4-cylinder'
```

Once we have our instance, we can access our internal attributes by using a period (.). Attributes are variables attached to the instance. Our `civic` variable has an `engine` attribute, which just means that `engine` is one of its internal variables.

### Defining a Custom Method

The last thing that we'll do to round out the first rendition of our class is to define a method that prints a description of the vehicle to the screen.

`~/python_objects/vehicle.py`

```
class Vehicle:
    """
    Vehicle models a vehicle w/ tires and an engine
    """

    def __init__(self, engine, tires):
        self.engine = engine
        self.tires = tires

    def description(self):
            print(f"A vehicle with an {self.engine} engine, and {self.tires} tires")
```

Our `description` method doesn't have any actual arguments, but we pass the instance in as `self`. From there, we can access the instance's attributes by calling `self.attribute_name`.

Let's use this new method:

```
$ python3.7 -i vehicle.py
>>> civic = Vehicle('4-cylinder', ['front-driver', 'front-passenger', 'rear-driver', 'rear-passenger'])
>>> civic.engine
'4-cylinder'
>>> civic.tires
['front-driver', 'front-passenger', 'rear-driver', 'rear-passenger']
>>> civic.description
<bound method Vehicle.description of <__main__.Vehicle object at 0x7fb5f3fbbda0>>
>>> civic.description()
A vehicle with a 4-cylinder engine, and ['front-driver', 'front-passenger', 'rear-driver', 'rear-passenger'] tires
```
Just like a normal function, if we don't use parenthesis, the method won't execute.

### Adding and Removing Attributes from Instances

We've seen how to define attributes as part of our instance initialization code, but an instance of a custom class also acts as a namespace for any attribute we want. This means that after we create an instance of a custom class, we can add attributes to it in the same way we assign a new variable. We just need to chain the attribute off of our instance's identifier. Let's add a `serial_number` (attribute) to my `civic` (identifier).

```
>>> civic.serial_number = '1234'
>>> civic.serial_number
'1234'
```

We can remove attributes from an instance of a class using the `del` keyword, just like we would to delete a variable. Remember, we need to be accessing the attribute and not just pass in our object.

```
>>> del civic.serial_number
>>> civic.serial_number
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Vehicle' object has no attribute 'serial_number'
```

## 44.3. Custom Constructors, Class Methods, and Decorators

There's a lot to learn when it comes to creating and building robust classes. In this lesson, we continue to learn about some of the tools at our disposal when creating classes: custom constructors and class methods.

### Documentation 

- [Classes](https://docs.python.org/3/tutorial/classes.html#classes)
- [Class Methods](https://docs.python.org/3/library/functions.html#classmethod)

### Custom Class Constructors

Unlike other languages like Java, Python doesn't provide a way for us to create multiple constructor methods. Instead, we get a single constructor method that we can customize, the `__init__` method. We've already customized this for our `Vehicle` class. This method has a default implementation that takes no arguments, so by defining this in our class, we've created a custom constructor.

### Using @classmethod to Create Convenience Constructor Methods

Although creating multiple different constructors isn't a feature of Python, it doesn't mean we can't do something similar. If we want another way to construct a `Vehicle` object with some preset values, we can create convenience methods using what is known as a class method. A class method is a function attached to the class itself, not an instance of the class, and it has access to any class-level attributes. To create a class method, we need to use what is known as a decorator. Decorators are functions or classes that we use to add additional functionality to a function by prefixing the decorator's name with an at-sign (`@`) and putting it on the line above our function or method definition. This sounds confusing, but remember back to our look at higher-order functions. A decorator takes a function and returns another modified function in its place. For the purposes of the PCAP, we only need to know how to use one specific decorator so that we can add class methods to our classes: the `@classmethod` decorator. Let's add a method to our `Vehicle` class that will allow us to create a bicycle (which has two wheels, and no engine).

`~/python_objects/vehicle.py`

```
class Vehicle:

    """
    Vehicle models a vehicle w/ tires and an engine
    """
    default_tire = 'tire'

    def __init__(self, engine, tires):
        self.engine = engine
        self.tires = tires

    @classmethod
    def bicycle(cls, tires=None):
        if not tires:
            tires = [cls.default_tire, cls.default_tire]
        return cls(None, tires)

    def description(self):
        print(f"A vehicle with an {self.engine} engine, and {self.tires} tires")
```

Notice we added a class-level variable called `default_tire`. This variable is set on the class itself and will also be available to instances of the class. By decorating the `bicycle` as a `@classmethod`, we're able to call `Vehicle.bicycle()`, and the class itself will be passed in as the implicit `cls` argument (this name is a convention, not a required name). Because the class itself `(Vehicle)` is passed into the method as the `cls` variable, that means when we call `cls()`, it is equivalent to doing `Vehicle()` and will invoke the `__init__` method. It's beneficial to use the `cls` variable instead of the class name, because if we ever change the name of the class, then we won't need to modify this function. If no argument is passed in for the `tires` parameter, then we'll create a default list containing the value of the `default_tire` class attribute two times. Let's load this file into the REPL and see if it works:

```
$ python3.7 -i vehicle.py
>>> bike = Vehicle.bicycle()
>>> bike
<__main__.Vehicle object at 0x7f947c0f7750>
>>> bike.description()
A vehicle with an None engine, and ['tire', 'tire'] tires
>>> bike.engine
>>> bike.tires
['tire', 'tire']
```

As we start modeling more and more concepts, there will be more situations where we'll want to use class methods to perform actions that require information available to only the class and doesn't require any instance information.

## 44.4. Inheritance and Super


## 44.5. Single and Multiple Inheritance


## 44.6. Name Mangling


## 44.7. Inspecting Objects





{% include links.html %}
