# C# Notes

## Program Structure

.NET generally refers to the family of programs and commands that let you make applications with C#.

the bare minimum consist of -

- Namespace declaration
- a class
- class method
- class attributes
- a Main method
- Statement and expressions
- comments

C# characteristic important point -

- is case sensitive
- all must end with semicolon
- program execution starts at ``Main`` method
- program file name can be different from class name
- is object-oriented

## Basic Syntax

### member variable

attributes or data members of a class used for storing data.

### member function

set of statements that perform a specific task.

## Data Types

C## is **strongly Typed programming Language**. all variable or constants for a given program must be described with one of the data types.

Every type directly or indirectly derives from the ``object`` class type.

Values of reference types are treated as objects simply by viewing the values as type object.

Values of value types are treated as objects by **boxing** and **unboxing**.

### Value Data Types

- directly store value of variable in memory
- accept signed and unsigned literals.
- the derived class of these data types are ``System.ValueType``

1. Signed & Unsigned Integral Types
2. Floating Point
3. Decimal
4. Character(16-bit Unicode)
5. Boolean

### Reference Data Types
contain a memory address or references of variable value.

1. String(``System.String``) - represent a sequence of Unicode characters
2. Object(base class) - all types, predefined and user-defined, reference types and value types, inherit directly or indirectly from Object.

when a value type is converted to object, its called **boxing**. when a variable of type object is converted to a value type, its **unboxing**.

### Pointer Data Types

same as in **C**.

contain memory address of the variable value.

``&`` - determine the address of a variable

``*`` - access the value of an address

### Nullable Types
assign ``null`` value to variable.

can only work with Value type not with reference type because it already contains null value.

can be used for checking a variable of certain type if it contain value or not.

### Enumeration types
a distinct value type that declares a set of named constants.

default associated constant values of enum members are of type **int**.

cannot define a method inside the definition of an enumeration type.

Multiple enum members may share the same associated value.

if enum member has no initializer, its associated value is set implicitly by:

- if its the first it will be 0
- otherwise the value = (preceding member value + 1)

~~~C#

enum Season
{
    Spring,
    Summer,
    Autumn,
    Winter
}

// can explicitly specify the constant values
enum ErrorCode : ushort
{
    None = 0,
    Unknown = 1,
    ConnectionLost = 100,
    OutlierReading = 200
}

~~~

## Constants

immutable values which are known at compile time and do not change for the life of the program. must be initialized as they are declared.

user defined types(classes, structs, arrays) cannot be ``const``(we use ``readonly`` modifier for that).

const methods, properties and event are not supported.

can be marked as public, private, protected, internal, protected internal or private protected.

## Casting and type conversion

after a variable is declared, it cannot be declared again or assigned a value of another type unless that type is implicitly convertible to the variable's type.

### Implicit conversion

no special syntax required. the conversion is type safe and no data lost.

conversion can be made when the value to be stored can fit into the variable without being truncated or rounded off.

implicit conversion can occur in a variety of situations:

- function member invocations
- cast expressions
- assignments

for integral type: the range of the source is a proper subset of the range for the target type.

For reference types, an implicit conversion always exists from a class to any one of its direct or indirect base classes or interfaces.

\* theres a chart reference of type conversion on the internet.

#### Implicit numeric conversion

from int, uint, long, or ulong to float and from long or ulong to double may cause a loss of precision, but will never cause a loss of magnitude.

no impicit to ``char`` type.

### Explicit conversion(cast)

require a **cast expression**.

a cast is a way of explicitly informing the compiler that you intend to make the conversion and that you are aware that data loss might occur.

cast between reference type does not change the run-time type of the underlying object(only changes the type of the value that is being used as a reference to that object)

C## provides the i``s`` operator to enable testing for compatibility before performing a cast.

### User Defined conversion

### Conversion with helper class


## Operators

most operator are the same as JS.

``++number`` is prefix, ``number++`` is postfix.

C## has **ternary operator**.

### Bitwise operator

- ``~`` ― complement
- ``&`` ― AND
- ``|`` ― OR
- ``^`` ― Exclusive OR
- ``<<`` ― Left Shift
- ``>>`` ― right Shift

C## have compuound assignments.

``=>`` is lambda Operator(Arrow function).

## Output

~~~c#
System.Console.WriteLine()
System.Console.Write()

// System is a namespace
// Console is a class within a namespace
// Write() WriteLine() is method
~~~

``Write()`` print only the string provided, ``WriteLine()`` print the string and moves to the start of next line.

### Printing concatenated string

~~~c#
Console.WriteLine("Value = " + val);
Console.WriteLine("Value = {0}", val);
Console.WriteLine("{0} + {1} = {2}", firstNumber, secondNumber, result);

~~~

using formatted string is better than concatenation.

## Input

~~~c#
Console.ReadLine(); // there is also Read(), ReadKey()
~~~

``ReadLine()`` read input until pressed enter and return the string.
``Read()`` read the next character and returns the ascii.
``ReadKey()``obtain the next key pressed by user. usually used to hold the screen until user press a key.

### Reading numeric Values

``Convert`` class for converting entered string to numeral.

## Expressions, Statements and Blocks

an **expression** must have at least one operand but may not have any operator.

### Statements

- Declaration - declare and initialize variables
- Expression
- Iteration
- Jump
- Exception Handling

### Blocks

a combination of zero or more statements that is enclosed inside curly brackets { }.

## Comments

1. Single line (//)
2. multi line (/* */)
3. XML (///)

### XML Documentation comments

is used to describe a piece of code.

### Commenting best practice

better to explain **why** than **how**.

## for, while, loops, conditional, while, switch, ternary

same syntax with JS.

foreach() have same functionality but different syntax with JS.

## Bitwise

C## has normal syntax.

it has uses 2's complement.

## Preprocessor directives

a block of statement that gets processed before the actual compilation starts. commands for the compiler that affects the compilation process.

begins with a ## (hash) symbol and all preprocessor directives last for one line(terminated by newline rather than semicolon).


### #define and #undef directives

define and undefine a ``symbol`` that will be used to specify conditions for compilation.

defined symbols will evaluates to true.

### #if, #elif, #else, #endif

to test the preprocessor expression.

a preprocessor expressions may consist of a symbol only or combination of symbols along with operators ``&&``, ``||``, ``!``.

### #warning

generate user-defined level one warning.

### #error

generate user-defined error(with message).

program will be terminated.

### #line

to modify the line number and the filename for #errors and #warnings.

### #region and #unregion

allows us to create a region that can be expanded or collapsed when using a Visual Studio Code Editor.

simply used to organize code.

### #pragma

used to give the compiler some special instructions for the compilation of the file in which it appears.

- ``#pragma warning``
- ``#pragma checksum``

## Namespace

to organize and provide a level of separation of codes.

namespace can contain:

- nested namespace
- Classes
- Interfaces
- Structures
- Delegates

accessing member of a namespace uses dot(.) operator or ``using``.

namespace can also help in controlling the scope of class and method names in larger programming projects.

the ``global`` namespace is the "root" namespace
``global::system`` will always refer to the .NET System namespace

## partial class

spliting the definition of a class to two or more source file. combined when compiled.

is used when:

- multiple developer can work on a large class simultaneously
- code can be added/modified easily

NOTE: ``partial`` modifier is not available on delegate or enumeration

### partial Method

a partial method consist of:

1. definition
2. implementation

things to remember:

- ``partial`` keywords
- return type ``void``
- implicit ``private``
- cannot be ``virtual``

## Structs

represent data structures that can contain data members and function members.

are value type and do not require heap allocation.

useful for small data structure that have value semantics.

can be nested.

implicitly inherit from the class ``System.ValueType``.

~~~C#
Point a = new Point(10, 10);
Point b = a;
a.x = 100;
System.Console.WriteLine(b.x);

// Output is 10 if its class it will be 100
~~~

### Structure properties

- can have methods, fields, indexers, properties, operator ,methods, and events
- can have defined constructors(but not destructors) but not default constructor
- no inheritance
- can implement on or more interfaces
- members cannot be abstract, virtual, or protected
- can be instantiated without ``new``2
- if ``new`` is not used, the fields remain unassigned and the object cant be used until all fields are initialized

## Methods

a code block that contains a series of statements. the statements is executed by calling the method and specifying any required arguments.

**argument** are values that are passed to a function when it is invoked.

**parameter** is a variable defined by a function that receives a value when a function is called.

``Main`` method is the entry point for every C# application and it's called by the common language runtime (CLR) when the program is started.

Methods are declared in a **class**, **struct**, or **interface** by specifying the:

- **access level**(public, private or optional modifiers)
- **return value**
- **name** of method
- **parameter**.

when an instance of a value type is passed to a method, its copy is passed(can use ``ref`` for passing as reference).

when an object of reference type is passed, the method receive the argument that indicates the location of the object. modification of the object inside the method will reflect on the original object.

### Passing parameters

#### Value Parameters

Parameters declared for a method without **in**, **ref** or **out**, are passed to the called method by **value**.

when a method is called a new storage location is created for each value parameter and is copied into them.

changes have no effect on the argument.

#### Reference Parameters

parameter modifier = **ref**.

represent the same memory location as the actual parameters that are supplied to the method.

#### Output Parameter

parameter modifier = **out**.

using output parameters, can return two values from a function.

same like reference parameters, except they transfer data out of the method.

#### in parameter

parameter modifier = **in**.

any operation on the parameter is made on the argument.

### Return Value

the value can be returned to the caller by value or (C# v7.0)by reference.

value returned by reference if the ``ref`` keyword is used in the method signature and it follows each return keyword.

return stops the execution of method.

non-void return type methods are **required** to use the return keyword to return a value.

### Async Methods

When control reaches an await expression in the async method, control returns to the caller, and progress in the method is suspended until the awaited task completes.

async method can have a return type of Task<TResult>, Task, or void.

async method that returns void can't be awaited and is used primarily to define event handlers.

### .Net Framework generic Tuple classes

named their properties Item1,Item2, ...

property name carry no semantic information.

### Tuples in C# v7.0 and later

use semantically meaningful names for the elements inside.

## Encapsulation

prevents access to implementation details.

**Abstraction** allows making relevant information visible and by encapsulation can implement a desired level of abstraction.

encapsulation is implemented using **access specifiers**(defines the scope and visibility of a class member).

### Access Specifier

the default access specifier of class member if we dont specify any is **private**.

#### Public

allows a class to expose its member variables and member functions to other function and objects. public members can be accessed outside the class.

#### Private

allows a class to hide its member variables and member functions from other functions and objects.

Only functions of the same class can access its private members.

even an instance of a class cannot access its private members.

#### Protected

allows a child class to access the member variables and member functions of its base class.

helps in **inheritance**.

#### Internal

allows a class to expose its member variables and member functions to other functions and objects in the current assembly.

can be accessed from any class or method defined within the application in which the member is defined(almost the same as **global**).

#### Protected Internal

allows a class to hide its member variables and member functions from other class objects and functions, except a child class within the same application.

used in **inheritance**.

## Classes

blueprint for a data type.

define what an object of the class consists of and what operations can be performed on that object.

default **access specifier** for a class type is **internal**. for the member is **private**.

use dot(.) operator to access member.

**member function** has its definition or its prototype within the class definition.

an **object** is a concrete entity based on a class. sometime called an instance of a class.

when an instance of a class(object) is created, a reference to the object is passed to the programmer. meaning we are interacting with variable of object is a reference to an object.

### class constructor

a special member function that is executed whenever we create  new objects of that class.

has the same name of the class and does not have return type.

does not(but can in **parameterized constructor**) have a parameter.

### Static members

only one instance of the member exist for a class.

no matter how many instance of a class is created, there is only one copy of the static member.

can be initialized outside/inside the member function or class definition.

## Inheritance

enables creating new classes that **reuse**, **extend**, and **modify** the behaviour defined in other classes.

the class whose member is inherited is called the **base class** and the class that inherits those members is called **derived class**.

derived class implicitly gains all the members of base class, except for constructor and finalizers. reuse the code in the base class without having to reimplement it.

derived class extends functionality the functionality of the base class.

## Arrays

properties:

- the number of dimensions and the length of each are cannot be changed during the lifetime of the instance
- default of numeric is 0, refernce is ``null``
- can be of any type including array type
- are reference type derived from the abstract base type Array

## Strings

- object of type String whose value is text
- the text is stored as a sequential read-only collection of Char objects
- no null-terminating character at the end
- length properties is determined number of Char object it contains, not the number of Unicode character.

## Polymorphism

'one interface, multiple function'.

provides the ability to a class to have multiple implementations with the same name

### static polymorphism

the response to a function is determined at compile time.

the decision of which method is to be called is made at compile time.

Overloading is the concept in which method names are the same with a different set of parameters.

known as Early Binding.

### dynamic polymorphism**

the response to a function is determined at run-time.

also known as late binding.

method name and signature must be the same and may have different implementation.

Method overiding - the base class and derived class to have the same method name and same something.

## Operator Overloading

a type/user-defined type can provide the custom implementation of an operation in case one or both of the operands are of that type.

``operator`` rules:

- include both ``public`` and ``static`` modifier
- at least one parameter must have type T or T? where T is the type that contains the operator declaration

theres a table of overloadability.

## Properties

member of a class that provides a flexible mechanism for classes to expose private fields. are named members of classes, structures, and interfaces. are extension of fields and are accessed using the same syntax.

**accessors** through which the value of the private fields can be read, written or manipulated.

Member variable or methods in a class or structures are called **Fields**.

by convention, all interface name begin with a capital I.

## Interfaces

a syntactical contract that all the classes inheriting the interface should follow.

contains definitions for a group of related functionality that a non-abstract class or a struct must implement.

defines the **what** part of the syntactical contract and the deriving classes define the **how** part of the syntactical contract.

contain only the declaration of the members. it is the resposibility of the deriving class to define the members.

may not declare instance data such as fields, auto-implemented properties, or property-like events.

may define default implementation of members.

a class or struct can implement multiple interfaces.

interface can contain instance:

- methods
- properties
- events
- indexers

to implement an interface member, the corresponding member must be:

- public
- non-static
- have the same name and signature

## Exception Handling

help deal with any unexpected or exceptional situations that occur when a program is running.

when an exception is thrown, CLR will unwind the stack and execute the first ``catch`` block it finds.

if no catch block found it will terminate the process and display a message to the user.

can explicitly generate exception with ``throw``.

## Tuples

enables packaging multiple values in a single object more easily.

to store a finite sequence of homogeneous or heterogeneous data of fixed sizes.

safely return multiple values from a method without resorting to out parameters (something you cannot do with anonymous types).

tuples are value type with mutable elements.

access element with ``tupleExample.item1`` or using **Named Tuples**.

## Abstract

create classes and members that are incomplete and must be implemented in a derived class.

abstract class cannot be intantiated.

provide common definition of a base class that multiple derived classes can share.

## sealed

prevent the inheritance of a class or certain class members that were previously marked ``virtual``.

cannot be used as a base class and cannot be abstract.

## Virtual

used to modify a method, property, indexer, or event declaration and allow for it to be overidden in a derived class.

## Override

is required to extend or modify the abstract or virtual implementation of an inherited method, property, indexer, or event.