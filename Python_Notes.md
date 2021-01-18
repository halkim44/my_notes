# Python

is a high-level, interpreted scripting language developed in the late 80s by Guido van Rossum.

- initial version was released in 1994.
- version 2.0 released in 2000
- version 3.0 was released in 2008 and were not backward compatible

the name was derived from Monty Python's Flying Circus.

## Operators

- no triple(===) like in JS
- (and, or, not) for logical operator
- there are 13 different assignment operators (e.g. +=, %=, |=)

### identity operators

- is
- is not

### membership operators

- in
- not in

## variables

variables are not statically typed.

# Namespace and scope

## name

- names(like var in js) are a name given to object
- different name with same data will have same id() as python does not create duplicate objects

## namespace

mapping of every name you have defined to corresponding objects.

Different namespaces can co-exist at a given time but are completely isolated.

exist as long as the interpreter runs.

When a reference is made inside a function, the name is searched in the local namespace, then in the global namespace and finally in the built-in namespace.

# Conditional

- avoid nesting if(its confusing)

# loops

- pass(placeholder in code)
- continue(like `break` skip and iteration)

# global variable

`global` keyword allow to modify var outide current scope
The basic rules for global keyword in Python are:

- When we create a variable inside a function, it is local by default.
- When we define a variable outside of a function, it is global by default. You don't have to use global keyword.
- We use global keyword to read and write a global variable inside a function.
- Use of global keyword outside a function has no effect.

```python
def foo():
    x = 20

    def bar():
        global x
        x = 25

    print("Before calling bar: ", x)
    print("Calling bar now")
    bar()
    print("After calling bar: ", x)

foo()
print("x in main: ", x)
```

return

```
Before calling bar: 20
Calling bar now
After calling bar: 20
x in main: 25
```

# Module

While importing a module, Python looks at several places. Interpreter first looks for a built-in module. Then(if built-in module not found), Python looks into a list of directories defined in sys.path. The search is in this order.

- The current directory.
- PYTHONPATH (an environment variable with a list of directories).
- The installation-dependent default directory.

modules only imported once.

use `imp`(default module) to reload.

## dir()

- to find out names that are defined inside a module
- names that begin with an underscore are default Python attributes associated with the module

# packages

As our application program grows larger in size with a lot of modules, we place similar modules in one package and different modules in different packages.

A directory must contain a file named `__init__.py` in order for Python to consider it as a package

# Data types

## Primitive datatypes

- integer
- floats
- strings

## Sequence datatypes

- strings
- list
- tuple

All sequences are ordered, indexed by integers, and have a length.

the only datatypes that can be **iterated**.

## tuples

different than lists bcoz we cannot change the element once assigned

creating tuple with ONE element is tricky(put comma at the end)

can delete a tuple(a way to reset tuple perhaps?)

advantages over list:

- tuples for different data types, lists for similar data types
- faster iteration (since it is immutable)
- as key for dictionary
- write-potected data

## String

place `r` or `R` to ignore escapes

## Sets

an unordered collection of items. Every set element is unique (no duplicates) and must be immutable.

can remove and add elements(set are mutable).

creating with `a = {}` will make a dictionary use `a = set()`

cannot access with indexing(since its unorder).

`add()`, `update()` and etc for modifying sets

the mathematical application of sets is what makes it interesting

### Frozenset

frozensets are immutable sets.

hashable.

```python
>>> A.isdisjoint(B)
False
>>> A.difference(B)
frozenset({1, 2})
>>> A | B
frozenset({1, 2, 3, 4, 5, 6})
>>> A.add(3)
...
AttributeError: 'frozenset' object has no attribute 'add'
```

## Dictionary

the key and value.
keys must be immutable.

```python
# empty dictionary
my_dict = {}

# dictionary with integer keys
my_dict = {1: 'apple', 2: 'ball'}

# dictionary with mixed keys
my_dict = {'name': 'John', 1: [2, 4, 3]}

# using dict()
my_dict = dict({1:'apple', 2:'ball'})

# from sequence having each item as a pair
my_dict = dict([(1,'apple'), (2,'ball')])
```

accessing values uses keys through `[]`(produce `KeyError` when not found) or `get()`(returns `none` when not found).

have dictionary comprehension.

# Python File I/O

we can open file in text mode or binary mode(used when dealing with non-text).

use `open()`.

encoding is involved for text file.

use `close()` after done. will free up the resources that were tied with the file.

dont forget to use `try...finally` when closing.

the best way to open without worrying about closing:

```python
with open("test.txt", encoding = 'utf-8') as f:
   # perform file operations
```

you can read file w `for loop`. its fast and efficient.

# Objects

**assignment** operations never make a copy of the value being assigned(pointer copies).

variables are names, not memory locations.

`copy` module for deep copying.

# directories & file management

python has `os` module tht have methods to work with directories.

# Errors and Built-in Exceptions

two classes of errors:

- Syntax
- logical (Exceptions)

## Logical Errors

occurs at runtime after passing syntax test.

examples

- FileNotFoundError
- ZeroDivisionError
- ImportError

create an exception object when occurs.

prints a traceback to error when not handled.

## Built-In Exceptions

to view all the built-in exception:

```python
print(dir(locals()['__builtins__']))
```

NOTE: there are also User-defined Exceptions

`try`, `except` and `finally` to handle exceptions(built-in and user-defined).

# Exception Handling

it is good programming practice to specify exceptions in the except clause as it will catch all exceptions and handle every case in the same way.

can also `raise exceptions`.

## Custom Exceptions

users can define such exceptions by creating a new class that has to be derived, either directly or indirectly, from `Exception` class.

a good practice to place all the user-defined exceptions that our program raises in a separate file.

```python
# define Python user-defined exceptions
class Error(Exception):
  """Base class for other exceptions"""
  pass

class ValueTooSmallError(Error):
  """Raised when the input value is too small"""
  pass

class ValueTooLargeError(Error):
  """Raise when the input value is too large"""
  pass

# our main program
# user guesses a number until he/she gets it right

# you need to guess this number
number = 10

while True:
  try:
    i_num= int(input("Enter a number: "))
    if i_num < number:
      raise ValueTooSmallError
    elif i_num > number:
        raise ValueTooLargeError
    break
   except ValueTooSmallError:
       print("This value is too small, try again!")
       print()
   except ValueTooLargeError:
       print("This value is too large, try again!")
       print()

print("Congratulations! You guessed it correctly.")
```

# OOP In Python

basic principles of OOP in Python:

- Inheritance
- Encapsulation
- Polymorphism

## inheritance

almost the same kind of ways that i used to with `super` and evythng..

## Encapsulation

prevent data from direct modifications.

denoted with `"_"` or `"__"`.

## Polymorphism

Polymorphism is an ability (in OOP) to use common interface for multiple form (data types).

```python
class Parrot:

    def fly(self):
        print("Parrot can fly")

    def swim(self):
        print("Parrot can't swim")

class Penguin:

    def fly(self):
        print("Penguin can't fly")

    def swim(self):
        print("Penguin can swim")

# common interface
def flying_test(bird):
    bird.fly()

#instantiate objects
blu = Parrot()
peggy = Penguin()

# passing the object
flying_test(blu)
flying_test(peggy)
```

NOTE: the methods have `self` as it's first argument because whenever an object calls its method, the object itself is passed as the first argument.

## Benefit of OOP

- The programming gets easy and efficient.
- The class is sharable, so codes can be reused.
- The productivity of programmars increases
- Data is safe and secure with data abstraction.

## Class

An object is also called an instance of a class and the process of creating this object is called `instantiation`.

A class creates a new local `namespace` where all its attributes are defined. Attributes may be data or functions.

### Constructors

`__init__()` gets called whenever a new object of that class is instantiated.

attributes of an object can be created on the fly:

```python
# Create another ComplexNumber object
# and create a new attribute 'attr'
c2 = MyClass(5)
c2.attr = 10

# Output: 10
print(c2.attr)
```

### deleting object

On the command `del c2`, the bind between `c2` and the object is removed.

But the object continues to exist in memory.

if no other name bound to it, is later automatically destroyed(garbage collection).

## Inheritance

defining a new class with little or no modification to an existing class.

new class called `derived (or child)class`, the on it inherits from is `base(or parent) class`.

the method in the derived class overrides that in the base class. This is to say, `__init__()` in Triangle gets preference over the same in Polygon

### Multiple inheritance

In multiple inheritance, any specified attribute is searched first in the current class. If not found, the search continues into parent classes in depth-first, left-right fashion without searching same class twice.

the order is called linearization of class an the set of rule to fine the order is `Method Resolution Order(MRO)`(can check on `__mro__`).

# Operator Overloading

the feature that allows same operator to have different meaning according to the context(like how `+` will perform arithmetic addition, merge lists and concatenate strings) is called `operator overloading`.

`special functions` can make our class compatible with built-in functions.

example of overloading with special function:

```python
class Point:
  def __init__(self, x = 0, y = 0):
    self.x = x
    self.y = y

  def __str__(self):
    return "({0},{1})".format(self.x, self.y)

  def __add__(self, other):
    x = self.x + other.x
    y = self.y + other.y
    return Point(x,y)

```

```python
>>> p1 = Point(2,3)
>>> p2 = Point(-1,2)
>>> print(p1 + p2)
# output: (1,5)
```

there is a table that shows lists of special function with its corresponding operator(including comparison operator).

# Python Advanced Topics

## Iterators

implemented in `for loops`, `comprehensions`, `generators` but hidden in plain sight.

is simply an object which will return data one at a time.

**iterator object** must implement two special methods, `__iter__()` and `__next__()`(called iterator protocol).

an object is called **iterable** if we can get an iterator from it(list, tuples,string etc.).

### how for loops work

```python
# create an iterator object from that iterable
iter_obj = iter(iterable)

# infinite loop
while True:
    try:
        # get the next item
        element = next(iter_obj)
        # do something with element
    except StopIteration:
        # if StopIteration is raised, break from loop
        break
```

### Build your own iterator

```python
class PowTwo:
  """Class to implement an iterator
  of powers of two"""

  def __init__(self, max = 0):
    self.max = max

  def __iter__(self):
    self.n = 0
    return self

  def __next__(self):
    if self.n <= self.max;
      result = 2 ** self.n
      self.n +=1
      return result
    else:
      raise StopIteration
```

the PowTwo now can be used in `iter()` `next()` or in a `for loop`.

```
NOTE AS OF THIS POINT
>>> int() # will output 0

```

we can also make `infine iterator` that must be included with a terminating condition.

using iterators save more memory(as we can iterate something without storing elements in memory).

## List Comprehension

creating a new list by applying an operation to each element of a sequence.

general syntax:

```
[ <expression> for <variable_name> in <sequence> if <condition>]
```

## Generator

a generator is a function that returns an object (iterator) which we can iterate over (one value at a time).

defined like normal function but with a `yield` instead of `return`.

if function has `yield` its a generator function.

how generator function differs from normal function:

- contains one or more `yield`
- When called, it returns an object (iterator) but does not start execution immediately.
- `__iter__()` and `__next__()` are implemented automatically.
- once function yields, the function is paused and the control is transfered to the caller.
- local variables and their states are remembered between successive calls
- when function terminates, `StopIteration` is raised automatically.

you can `for loop` generators.

Normally, generator functions are implemented with a loop having a suitable terminating condition:

```python
def rev_str(my_str):
    length = len(my_str)
    for i in range(length - 1, -1, -1):
        yield my_str[i]


# For loop to reverse the string
for char in rev_str("hello"):
    print(char)
"""
this prints:
o
l
l
e
h
"""
```

### Generator Expression

simple generators can be easily created on the fly using generator expressons.

the diffrence with **list comprehension** is it produce one item at a time which is lazy execution(producing items only when asked for) which makes generator more memory efficient.

can also be used as function arguments(can drop the round parentheses).

### why generators are used

- makes code shorter that can be implemented in a clear and concise way.
- memory efficient
- excelent mediums to represent an infinite stream of data. since generators produce only one item at a time, they can represent an infinite stream of data.
- Multiple generators can be used **to pipeline a series of operations**.

## Closure

```python
def print_msg(msg):
# This is the outer enclosing function

    def printer():
# This is the nested function
        print(msg)

    return printer  # this got changed

# Now let's try calling this function.
# Output: Hello
another = print_msg("Hello")
another()


>>> del print_msg
>>> another()
Hello
>>> print_msg("Hello")
Traceback (most recent call last):
...
NameError: name 'print_msg' is not defined
```

### When do we have closure

- must have a nested function.
- nested function must refer to a value in the enclosing function.
- enclosing function must return nested function.

### when to use closure

- avoid the use of global values
- data hiding(sort of)
- When there are few methods to be implemented in a class, best to use closure.

NOTE: `__closure__` attributes returns a tuples of cell objects if it is a closure function

## Decorators

also called **metaprogramming** as a part of the program tries to modify another part of the program at compile time.

everything in python are objects(like in JS).

a decorator is a callable that returns a callable(object which implements `__call__()`).

```python
def smart_divide(func): ## this is a decorator function
   def inner(a,b):
      print("I am going to divide",a,"and",b)
      if b == 0:
         print("Whoops! cannot divide")
         return

      return func(a,b)
   return inner

# we can do this
@smart_divide
def divide(a,b):
    return a/b
# or this
def divide(a,b):
    return a/b
divide = smart_divide(divide)

# both will return the same
divide(2,5)
# Output: 0.5

```

there is a way to make `inner()` work with any number of parameter.

this magic is done as `inner(*args, **kwargs)`. In this way, args will be the tuple of positional arguments and kwargs will be the dictionary of keyword arguments

you can chain the `@` decorator on top of the function if you have multiple decorators(the orders matter).

# Itertools

a module that provides various function that work with iterators to produce complex iterators.

as a fast, memory-efficient tool that is used either by themselves or in combination to form Iterator algebra.

types of iterators in the module:

- Infinite iterators (methods that iterate something infinitely)
- Combinatoric iterators(used to simplify combinatorial constructs such as permutation,combination, and cartesian products are called combinatoric iterators).
- Terminating iterators

# Collectons module

implements specialized data structures which provide **alternative to python’s built-in container data types**.

# Complex number in Python

complex number can be created using `complex()` function and using direct assignment.

complex number are mostly used where we define something using two real numbers.

```python
c = 1 + 2j
print(type(c)) // <class 'complex'>
print(c) // (1+2j)

c1 = complex(2, 4)
print(type(c1)) // <class 'complex'>
print(c1) (2+4j)

```

## python attributes and instance

- `.real`
- `.imag`
- `.conjugate()`

## calculations

support addition, subtraction, multiplication and divisions.

cant be used with comparison operators.

## cmath module

provide access to mathematical function for complex numbers.

### phase of Complex number

is the angle between real axis and the vector representing the imaginary part.

return in radian(convert using `numpy.degrees()`).

### polar coordinate and cartesian(rectangular) coordinate

`cmath.polar()` write a complex number in polar coordinates, which is a tuple of modulus and phase of the complex number.

# Date & Time

use module `datetime` to work with dates and times.

commonly used class inside `datetime` module:

- date
- time
- datetime(contain date and time information)
- timedelta(difference between 2 dates or times. can perform arithmetic operations on timedelta obj.)

formatting date use `strftime()` and `strptime()`.

`pytz` module can handle timezone.

## strftime

return a string rerpresenting date and time using `date`, `time` and `datetime` object.

takes one or more **format codes** as argument and returns a formatted string based on it.

## strptime()

creates a datetime object from the given string(but need to be in certain format or else `ValueError`).

NOTE:timestamp is the number of seconds between a particular date and January 1, 1970 at UTC.

## Time module

### time.sleep()

suspends (waits) execution of the current thread for a given number of seconds.

Before Python 3.5, the actual suspension time may be **less than** the argument specified.

in multi-threaded program, `sleep()` will suspend a thread rather than the whole execution.

## Object Identity

- every object that is created is given a number that uniquely identifies it.
- it is guaranteed that no two object will have the same identity.

## Deep Dives

- interpreter creates objects for the integers in the range[-5, 256] at startup and reuse them during program executions thus why numbers in that range have same `id()`.
