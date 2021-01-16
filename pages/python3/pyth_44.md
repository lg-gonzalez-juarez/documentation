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

Our `Vehicle.bicycle` class method does a good job of creating a vehicle that looks like a `bicycle`, but should we have a Bicycle class instead? Because a bicycle is a type of vehicle, we can leverage the code that exists in the `Vehicle` class by creating a new class that inherits from the `Vehicle` class. In this lesson, we'll learn about inheritance, one of the core tenants of object-oriented programming (OOP).

### Documentation 

- [Classes](https://docs.python.org/3/tutorial/classes.html#classes)
- [Inheritance](https://docs.python.org/3.7/tutorial/classes.html#inheritance)
- [Super](https://docs.python.org/3/library/functions.html#super)

### Using Inheritance to Customize an Existing Class

Our existing `Vehicle` implementation does exactly what we need it to do for a general vehicle, but there are other, more specific types of vehicles such as cars, trucks, boats, and bicycles. If we wanted to model these other types of vehicles, we could use our existing `Vehicle` class as a starting point by inheriting its existing implementation. Let's add a new `Bicycle` class to a new file called `bicycle.py`.

`~/python_objects/bicycle.py`

```
from vehicle import Vehicle

class Bicycle(Vehicle):
    pass
```

By passing in the `Vehicle` class to our class definition for `Bicycle`, we're specifying that our class is a subclass of `Vehicle`. As it stands right now, the `Bicycle` class will behave exactly like the `Vehicle` type. From here, we can add more functionality and internal states specific to a bicycle. The convenience method we added to `Vehicle` essentially allows us to have a constructor that doesn't accept an engine, since a bicycle doesn't have an engine. That's what the constructor for `Bicycle` should do. Let's customize the initializer to do this.

`~/python_objects/bicycle.py`

```
from vehicle import Vehicle

class Bicycle(Vehicle):
    def __init__(self, tires=[]):
        if not tires:
            tires = [self.default_tire, self.default_tire]
        self.tires = tires
```

Because `Bicycle` is a subclass of `Vehicle`, it already has access to the class-level variable `default_tire`, so we don't need to redefine that to use it within the `__init__` method. Let's use our class in the REPL to see if it is working correctly.

```
$ python -i bicycle.py
>>> bike = Bicycle()
>>> bike.tires
['tire', 'tire']
>>> custom_bike = Bicycle(['front-tire', 'back-tire'])
>>> custom_bike.description()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/cloud_user/python_objects/vehicle.py", line 18, in description
    print(f"A vehicle with an {self.engine} engine, and {self.tires} tires")
AttributeError: 'Bicycle' object has no attribute 'engine'
```

This error makes sense. Our bicycle doesn't have an engine. We're going to need to customize the `description` method to change the message. Looking at this error, does it make sense for `Vehicle` to require an engine and tires? Not really. A bicycle doesn't have an engine, and a boat doesn't have tires, so neither of those should be required. One piece of information that does describe a vehicle could be `distance_traveled`. Let's make `Vehicle` more abstract and have the `description` only print out the distance traveled.

`~/python_objects/vehicle.py`

```
class Vehicle:
    """
    Vehicle models a device that can be used to travel.
    """
    def __init__(self, distance_traveled=0, unit='miles'):
        self.distance_traveled = distance_traveled
        self.unit = unit

    def description(self):
        print(f"A {self.__class__.__name__} that has traveled {self.distance_traveled} {self.unit}")
```

Now our `Vehicle` class is much more generic and can be used as the parent class or base class for any more specific vehicle. We do need to change our `Bicycle` implementation now, and we will want to make sure that we're setting a `distance_traveled` and `unit`. Thankfully, we don't need to redo these lines, because we can use `super`. Let's break down the expressions `self.__class__.__name__`. The variable `self` is an instance of `Vehicle` in this case, but when this method is called from a subclass, then `self` will be an instance of that class instead. We want to display the name of the class in our `description` output, so we'll access the `__name__` attribute on the class itself. That will provide us the string value.

### Using super()

When we want to customize a method written on a parent class without entirely replacing the method, then we're able to invoke the parent class's implementation of the method by calling the `super()` function. We need to do this to change the  `Bicycle.__init__`method. A bicycle has tires, so we want that as another parameter in the initializer. Otherwise, we would like to have the initialization behave the same way as it does for `Vehicle`. Let's implement `__init__`.

`~/python_objects/bicycle.py`

```
from vehicle import Vehicle

class Bicycle(Vehicle):
    default_tire = 'tire'

    def __init__(self, tires=[], distance_traveled=0, unit='mile'):
        super().__init__(distance_traveled, unit)
        if not tires:
            tires = [self.default_tire, self.default_tire]
        self.tires = tires
```

By calling `super()`, we have access to the methods implemented in our parent class, `Vehicle`. We'll then call the `__init__` method with the proper parameters. The `self`, in the context of this call to `__init__`, is our `Bicycle` instance. So, this method call will set `distance_traveled` (`self.distance_traveled=0`) and `unit` (`self.unit = 'miles'`) on our `Bicycle` class. We're leveraging code from the parent class while adding a little more to the initialization of this new class.

Let's take this into the REPL to see how it works.

```
$ python3.7
Python 3.7.6 (default, Jan 30 2020, 15:46:02)
[GCC 4.8.5 20150623 (Red Hat 4.8.5-39)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from vehicle import Vehicle
>>> from bicycle import Bicycle
>>> vehicle = Vehicle()
>>> bike = Bicycle()
>>> vehicle.description()
A Vehicle that has traveled 0 miles
>>> bike.description()
A Bicycle that has traveled 0 mile
```

As we can see, description outputs something different for the `Bicycle` without us even changing it because we wrote it in a generic, context-aware way. That being said, we would like to add information about our tires to the `description` too, and once again this is a situation where we can leverage super. To make this a little quicker to test, we'll also add a `__name__` == `"__main__"` condition with some code to demonstrate what we're writing.

`~/python_objects/bicycle.py`

```
from vehicle import Vehicle

class Bicycle(Vehicle):
    default_tire = 'tire'

    def __init__(self, tires=[], distance_traveled=0, unit='mile'):
        super().__init__(distance_traveled, unit)
        if not tires:
            tires = [self.default_tire, self.default_tire]
        self.tires = tires

    def description(self):
        initial = super().description()
        return f"{initial} on {len(self.tires)} tires."

if __name__ == "__main__":
    bike = Bicycle()
    print(bike.description())
```

It doesn't really make sense for the call to `description` to print the information. That just makes it hard to work with. What we've written here works a little better and allows us to control when we're using the class that is going to be printed. We want the initial string provided by `Vehicle`, and then we'll customize it to show a little information about how many tires we have. Because of how `Vehicle.description` is currently written, this won't quite work the way we would like because its printing the description on two lines.

```
$ python3.7 bicycle.py
A Bicycle that has traveled 0 mile
None on 2 tires.
```

Let's fix this by making `Vehicle.description` return a string, rather than the side-effect of printing a message.

`~/python_objects/vehicle.py`

```
class Vehicle:
    """
    Vehicle models a device that can be used to travel.
    """
    def __init__(self, distance_traveled=0, unit='miles'):
        self.distance_traveled = distance_traveled
        self.unit = unit

    def description(self):
        return f"A {self.__class__.__name__} that has traveled {self.distance_traveled} {self.unit}"
```

Let's run `bicycle.py` one last time to see that the description is now on one line.

```
$ python3.7 bicycle.py
A Bicycle that has traveled 0 miles on 2 tires.
```

We've learned quite a bit in this lesson about inheritance and super, but also how not to design our objects. Sometimes our initial thoughts about our objects are just not right and can make working with the items harder than we originally imagined.

## 44.5. Single and Multiple Inheritance

Sometimes we have an object that makes sense to be a subclass of more than one other type. In these situations, we can use what is called multiple inheritance. Multiple inheritance is not something we use too often, but it is good to understand how it works. We'll learn all about it in this lesson.

### Documentation

- [Classes](https://docs.python.org/3/tutorial/classes.html#classes)
- [Inheritance](https://docs.python.org/3.7/tutorial/classes.html#inheritance)
- [Multiple Inheritance](https://docs.python.org/3/tutorial/classes.html#multiple-inheritance)
- [Super](https://docs.python.org/3/library/functions.html#super)

### Multiple Inheritance

Multiple inheritance allows us to inherit from multiple parent classes. This can be used to pull functionality from multiple different classes into a single class. To demonstrate multiple inheritance, we're going to continue modeling vehicles starting with new classes for a `Car` and a `Boat`. These classes are very similar to what we did with `Bicycle`, so we'll quickly create these classes without much additional comment.

`~/python_objects/car.py`

```
from vehicle import Vehicle

class Car(Vehicle):
    default_tire = 'tire'

    def __init__(self, engine, tires=[], distance_traveled=0, unit='miles'):
        super().__init__(distance_traveled, unit)
        if not tires:
            tires = [self.default_tire, self.default_tire]
        self.tires = tires
        self.engine = engine

    def drive(self, distance):
        self.distance_traveled += distance
```

`~/python_objects/boat.py`

```
from vehicle import Vehicle

class Boat(Vehicle):
    def __init__(self, boat_type='sail', distance_traveled=0, unit='miles'):
        super().__init__(distance_traveled, unit)
        self.boat_type = boat_type

    def voyage(self, distance):
        self.distance_traveled += distance

    def description(self):
        initial = super().description()
        return f"{initial} using a {self.boat_type}"
```

We can model another type of vehicle, called `AmphibiousVehicle`, by inheriting from both a `Car` and a `Boat`. This is a type of vehicle that is both a car (so it can travel on land) and a boat (so it can travel through the water). To use multiple inheritance, we separate our parent classes with a comma in the same way that we would with function parameters. Here's the initial version of our `AmphibiousVehicle` (in `amphibious_vehicle.py`):

```
~/python_objects/amphibious_vehicle.py

from boat import Boat
from car import Car

class AmphibiousVehicle(Car, Boat):
    pass
```

Let's load this class into the REPL to see what it attempts to do when we initialize a new one.

```
$ python -i amphibious_vehicle.py
>>> water_car = AmphibiousVehicle()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: __init__() missing 1 required positional argument: 'engine'
>>>
```

By default, our class will try to use the method from the first class in the list of classes (`Car`) that we inherit when we don't customize our method. We're going to want to customize `__init__` to explicitly set our `boat_type` to `'motor'` and then continue with our initialization using the code from the `Car` class.

`~/python_objects/amphibious_vehicle.py`

```
from boat import Boat
from car import Car

class AmphibiousVehicle(Car, Boat):
    def __init__(self, engine, tires=[], distance_traveled=0, unit='miles'):
        super().__init__(engine, tires, distance_traveled, unit)
        self.boat_type = 'motor'

    def travel(self, land_distance=0, water_distance=0):
        self.voyage(water_distance)
        self.drive(land_distance)
```

Let's try this again to see what happens.

```
$ python -i amphibious_vehicle.py
>>> water_car = AmphibiousVehicle('4 cylinder')
>>> water_car.description()
'A AmphibiousVehicle that has traveled miles miles using a motor'
```

There are some issues here. First, `AmphibiousVehicle` isn't quite what we're going for when we print this out. Additionally, our `distance_traveled` attribute is apparently being set to `'miles'` instead of `0`. To understand what is going on, we need to get a better understanding of the method resolution order when calling `super` when using multiple inheritance.

### Method Resolution Order

Method resolution order is a term for looking at how methods on an object are found and which ones are run. Thankfully, we can see the method resolution order (i.e. "MRO") by accessing the `__mro__` attribute on our `AmphibiousVehicle` class.

```
>>> AmphibiousVehicle.__mro__
(<class '__main__.AmphibiousVehicle'>, <class 'car.Car'>, <class 'boat.Boat'>, <class 'vehicle.Vehicle'>, <class 'object'>)
```

This shows us that we will run what is found in `AmphibiousVehicle` first, `Car` second, `Boat` third, `Vehicle` fourth, and `object` last (object is the default type that we inherit when we create a class). What this list doesn't tell us is that when we call `super`, it will call the method in all of our parent classes that implement it. To show this, let's add some print lines into our parent class `__init__` functions.

`~/python_objects/boat.py`

```
from vehicle import Vehicle

class Boat(Vehicle):
    def __init__(self, boat_type='sail', distance_traveled=0, unit='miles'):
        print(f"__init__ from Boat with distance_traveled: {distance_traveled} and {unit}")
        super().__init__(distance_traveled, unit)
        self.boat_type = boat_type

    def voyage(self, distance):
        self.distance_traveled += distance

    def description(self):
        initial = super().description()
        return f"{initial} using a {self.boat_type}"
```

`~/python_objects/car.py`

```
from vehicle import Vehicle

class Car(Vehicle):
    default_tire = 'tire'

    def __init__(self, engine, tires=[], distance_traveled=0, unit='miles'):
        print(f"__init__ from Car with distance_traveled: {distance_traveled} and {unit}")
        super().__init__(distance_traveled, unit)
        if not tires:
            tires = [self.default_tire, self.default_tire]
        self.tires = tires
        self.engine = engine

    def drive(self, distance):
        self.distance_traveled += distance
```

`~/python_objects/vehicle.py`

```
class Vehicle:
    """
    Vehicle models a device that can be used to travel.
    """
    def __init__(self, distance_traveled=0, unit='miles'):
        print(f"__init__ from Vehicle with distance_traveled: {distance_traveled} and {unit}")
        self.distance_traveled = distance_traveled
        self.unit = unit

    def description(self):
        return f"A {self.__class__.__name__} that has traveled {self.distance_traveled} {self.unit}"
```

Now if we initialize a new `AmphibiousVehicle`, we should get more insight into how `distance_traveled` is being set to `'miles'`.

```
$ python -i amphibious_vehicle.py
>>> water_car = AmphibiousVehicle('4-cylinder')
__init__ from Car with distance_traveled: 0 and miles
__init__ from Boat with distance_traveled: miles and miles
__init__ from Vehicle with distance_traveled: miles and miles
```

As we can see, we call `super` one time, and yet both `Car` and `Boat` have their `__init__` methods run. This is a little confusing because it's not that we're running both methods from `AmphibiousVehicle`. It's that Car.`__init__` also calls super. Because `self` is an `AmphibiousVehicle` at the moment that `super` is called from `Car`, it calls `__init__` from the next object in the method resolution order, which is `Boat`. We're then calling `Boat.__init__` with only `distance_traveled` and `unit` as positional arguments.

If we run `Boat(0, 'miles')`, this will give us a `Boat` with `distance_traveled` set to `'miles'`. How do we get around this? By adjusting our objects to be more flexible by using `**kwargs` to capture extra keyword arguments and explicitly use keyword arguments when calling `super().__init__`.

`~/python_objects/amphibious_vehicle.py`

```
from boat import Boat
from car import Car

class AmphibiousVehicle(Car, Boat):
    def __init__(self, engine, tires=[], distance_traveled=0, unit="miles"):
        super().__init__(
            engine=engine, tires=tires, distance_traveled=distance_traveled, unit=unit
        )
        self.boat_type = "motor"

    def travel(self, land_distance=0, water_distance=0):
        self.voyage(water_distance)
        self.drive(land_distance)
```

`~/python_objects/boat.py`

```
from vehicle import Vehicle

class Boat(Vehicle):
    def __init__(self, boat_type="sail", distance_traveled=0, unit="miles", **kwargs):
        super().__init__(distance_traveled=distance_traveled, unit=unit, **kwargs)
        self.boat_type = boat_type

    def voyage(self, distance):
        self.distance_traveled += distance

    def description(self):
        initial = super().description()
        return f"{initial} using a {self.boat_type}"
```

`~/python_objects/car.py`

```
from vehicle import Vehicle

class Car(Vehicle):
    default_tire = "tire"

    def __init__(self, engine, tires=[], distance_traveled=0, unit="miles", **kwargs):
        super().__init__(distance_traveled=distance_traveled, unit=unit, **kwargs)
        if not tires:
            tires = [self.default_tire, self.default_tire]
        self.tires = tires
        self.engine = engine

    def drive(self, distance):
        self.distance_traveled += distance
```

`~/python_objects/vehicle.py`

```
class Vehicle:
    """
    Vehicle models a device that can be used to travel.
    """

    def __init__(self, distance_traveled=0, unit="miles", **kwargs):
        self.distance_traveled = distance_traveled
        self.unit = unit

    def description(self):
        return f"A {self.__class__.__name__} that has traveled {self.distance_traveled} {self.unit}"
```

Now that our initialization methods are more flexible, and we're being more explicit, let's try this again to see if our attributes are set properly.

```
$ python -i amphibious_vehicle.py
>>> water_car = AmphibiousVehicle('4 cylinder')
>>> water_car.description()
'A AmphibiousVehicle that has traveled 0 miles using a motor'
>>> water_car.travel(10, 15)
>>> water_car.description()
'A AmphibiousVehicle that has traveled 25 miles using a motor'
```

We've finally been able to use our class properly and call the `travel` method. Because `Boat` implements `voyage`, and `Car` implements `drive`, we're able to call each of those methods using `super`. They will be dispatched to the proper parent class. This shows one of the important things to consider when working with multiple inheritance. Things work well if our parent classes don't implement the same method names, but it can become a headache to debug issues when multiple classes implement the same method and also call `super`.

## 44.6. Name Mangling

Python doesn't really have the concept of private classes or instance variables. Data on an object can always be accessed explicitly. But by following some conventions, we can utilize a feature called name mangling to ensure that private data on a parent class isn't overwritten if the subclass also has a variable with the same name.

### Documentation 
- [Classes](https://docs.python.org/3/tutorial/classes.html#classes)
- [Private Variables](https://docs.python.org/3/tutorial/classes.html#private-variables)

### What Is Name Mangling?

Name mangling is something that allows the interpreter to replace special identifiers in our classes with ones that are specific to the class they're written in. This isn't something we'll leverage often, but the official tutorial has a snippet of code that demonstrates this really well. Let's create a file called `mapping.py` to work with this example code (which can be found here).

```
~/python_objects/mapping.py

class Mapping:
    def __init__(self, iterable):
        self.items_list = []
        self.__update(iterable)

    def update(self, iterable):
        for item in iterable:
            self.items_list.append(item)

    __update = update   # private copy of original update() method

class MappingSubclass(Mapping):
    def update(self, keys, values):
        # provides new signature for update()
        # but does not break __init__()
        for item in zip(keys, values):
            self.items_list.append(item)
```

There are some comments in this code that roughly explain what is going on, but the important points are this:

* In `Mapping`, we're keeping a reference to the original version of `update` as `__update`, so that we can use it within the `__init__`method. By doing this, we'll always use the original version of the method even if a subclass implements a different version of `update` (as the `MappingSubclass` does).
* The name mangling aspect of things is that `__update` becomes `_Mapping__update`, even if we add an `__update` identifier to `MappingSubclass`.

Let's add an `__update` identifier to `MappingSubclass` before we take a look at what is going on in the REPL.

`~/python_objects/mapping.py`

```
class Mapping:
    def __init__(self, iterable):
        self.items_list = []
        self.__update(iterable)

    def update(self, iterable):
        for item in iterable:
            self.items_list.append(item)

    __update = update  # private copy of original update() method


class MappingSubclass(Mapping):
    def update(self, keys, values):
        # provides new signature for update()
        # but does not break __init__()
        for item in zip(keys, values):
            self.items_list.append(item)

    def print_something(self):
        print("Printing something")

    __update = print_something
```

Let's load this into the REPL and see the identifiers that exist on our classes.

$ python -i mapping.py
>>> Mapping.__update
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: type object 'Mapping' has no attribute '__update'
>>> dir(Mapping)
['_Mapping__update', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'update']
>>> dir(MappingSubclass)
['_MappingSubclass__update', '_Mapping__update', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'print_something', 'update']
```

Notice that `Mapping` has a `_Mapping__update` identifier, but not `__update`, and `MappingSubclass` has both `_MappingSubclass__update` and `_Mapping__update`. These are the rules for creating an identifier that will be name mangled:

* The name starts with at least two underscores (__).
* The name has at most one trailing underscore (_).
* The identifier must be defined in the definition of the class at the same level as methods.

## 44.7. Inspecting Objects





{% include links.html %}
