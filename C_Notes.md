# Variable, constants and literals
## variables
~~~c
int playerScore = 95;

int vowels, consonant, digit, space;
vowels = consonant = digit = space = 0;
~~~

### Rules for naming a variable
- leters, digits and underscore only
- first letter cannot be digit
- longer than 31 character is dangerous

variable type cannot be changed once declared.

~~~c
int number = 5;      // integer variable
number = 5.5;        // error
double number;       // error
~~~

## Literals
data used for representing fixed values.like how string cannot be assigned different value(immutable values).

- Integers(deci,oct,hex)
- Floating-point
- Characters(enclosing a single character inside quotation marks ``'a'``)
- escape sequences(``\n``)
- String
  
## Constants
variables whose value cannot change.
~~~C
const double PI = 3.14;
~~~

# Data Types
declarations for variable determining the type and size of data associated to with variables.

### int 
positive/negative values(no decimals).

**4 bytes** from -2147483648 to 2147483647.

### float and double
used to hold real numbers.
``float``(single precision float data type) is **4 bytes**. ``Double``(double precision float data type) is **8 bytes**.
### char
for character type variables(1 byte).
### void
nothing, no type, incomplete, absent.

cannot create variables of void type.

### short and long
``long`` for **large number**.

``short`` for small integer ([−32,767, +32,767] range).

``sizeof()`` to check size of variable.

### signed and unsigned
type modifiers.

~~~C
unsigned int x;
int y;
~~~
``x`` can hold value from ``0`` to ``2³²-1``.

### Enumerated
### Complex
### Derived
derived from fundamental data types(arrays,pointers, function types, structures, etc.).

# C Input Output(I/O)
~~~C
#include <stdio.h>    
int main()
{ 
    // Displays the string inside quotations
    printf("C Programming");
    return 0;
}
~~~
- all C program must contain ``main()``
- ``printf()`` send formatted output to screen
- must include ``stdio.h`` to use ``printf()``.

# Conditional
other conditional in C is the same syntax JS.
# goto
``goto`` allows transfer of control of program to ``label``.

~~~c
// Program to calculate the sum and average of positive numbers
// If the user enters a negative number, the sum and average are displayed.

#include <stdio.h>

int main() {

   const int maxInput = 100;
   int i;
   double number, average, sum = 0.0;

   for (i = 1; i <= maxInput; ++i) {
      printf("%d. Enter a number: ", i);
      scanf("%lf", &number);
      
      // go to jump if the user enters a negative number
      if (number < 0.0) {
         goto jump;
      }
      sum += number;
   }

jump:
   average = sum / (i - 1);
   printf("Sum = %.2f\n", sum);
   printf("Average = %.2f", average);

   return 0;
}
~~~

Note: ``goto`` may lead to buggy code

# functions
- standard library function
- User-defined function

## Standard library
defined in header files.

example: ``printf`` is standard library function from ``stdio.h`` header file.

## User-defined
~~~c
#include <stdio.h>
int addNumbers(int a, int b);         // function prototype

int main()
{
    int n1,n2,sum;

    printf("Enters two numbers: ");
    scanf("%d %d",&n1,&n2);

    sum = addNumbers(n1, n2);        // function call
    printf("sum = %d",sum);

    return 0;
}

int addNumbers(int a, int b)         // function definition   
{
    int result;
    result = a+b;
    return result;                  // return statement
}
~~~

### function Prototype
declaration of a function that specifies function's name parameters and return type(doesn't contain function body).

give information to compiler that the function may later be used in the program.

C compiler checks the types and counts of all parameter lists on the function that have prototype.

not needed if the user-defined function is defined before the ``main()``.

NOTE: the type of return value, arguments specified function definition and prototype must match.

# Storage Class
Every variable in C programming has two properties: type and storage class.

storage class determines the scope, visibility and lifetime of a variable.

4 types of storage class:
- automatic
- external
- static
- register

## local Variable
declared inside a block are **automatic** or local variable. exist only inside the block in which it is declared.

~~~c

int main() {
    int n1; // n1 is a local variable to main()
}

void func() {
   int n2;  // n2 is a local variable to func()
}
~~~
``func`` can access ``n1`` and ``n2`` is local to it. ``main`` is the same with ``n1`` is its local.

## Global variable
known as **external**.

use **extern** to access in different file.

## Register Variable
faster than local(depend on compiler) but rarely  useful.

unless in embedded systems, there is no use for it.

## static variable
the value persist until the end of program.

~~~c
#include <stdio.h>
void display();

int main()
{
    display(); // 6
    display(); // 11
}
void display()
{
    static int c = 1;
    c += 5;
    printf("%d  ",c);
}
~~~

# Arrays
~~~
dataType arrayName[arraySize][for2dArraySize][for3d][so On..];
~~~

size cannot be changed once declared.

dont access out of bound. accessing element out of bound sometimes get error and sometimes run correctly.

## Arrays & Functions
Passing arrays to function
~~~c
// Program to calculate the sum of array elements by passing to a function 

#include <stdio.h>
float calculateSum(float age[]);

int main() {
    float result, age[] = {23.4, 55, 22.6, 3, 40.5, 18};

    // age array is passed to calculateSum()
    result = calculateSum(age); // only the name is passed to function
    printf("Result = %.2f", result);
    return 0;
}

float calculateSum(float age[]) { // the [] is used to inform compiler that you are passing one-dimensional array to function

  float sum = 0.0;

  for (int i = 0; i < 6; ++i) {
		sum += age[i];
  }

  return sum;
}
~~~

NOTE: cannot return arrays from functions

# Pointers
## address in C
if ``myHome`` is a variable, ``&myHome`` will return **address in memory**.

the address will not be the same on every execution.

## C Pointers
Pointers are special variables that are used to store addresses rather than values.

The data type of pointer and the variable must match.
pointer is just like another variable, only its stores address of another variable other than a value.
~~~c
// ways to declare pointers
int* p;
int *p1;
int * p2;
int* p4, p5; // pointer p4 and normal var p5

// Assigning address to pointers
int* pc, c; // pc point to either no or random address| c has address but contain random garbage value
c = 5;
pc = &c; // address of c i assigned to pc pointer

// get value pointed by Pointer
printf("%d", *pc); // Output 5
// * is called dereference operator
~~~
``&`` get address of a variable. ``*`` get the value at address.

## Common Mistakes
~~~c
int c, *pc;

// pc is address but c is not
pc = c; // Error

// &c is address but *pc is not
*pc = &c; // Error

// both &c and pc are addresses
pc = &c;

// both c and *pc values 
*pc = c;

~~~

## Array and pointers
~~~c
#include <stdio.h>
int main() {
   int x[4];
   int i;

   for(i = 0; i < 4; ++i) {
      printf("&x[%d] = %p\n", i, &x[i]);  // using &
   }

   printf("Address of array x: %p", x);

   return 0;
}
// Output
// &x[0] = 1450734448
// &x[1] = 1450734452
// &x[2] = 1450734456
// &x[3] = 1450734460
// Address of array x: 1450734448
~~~

notice the difference of 4 bytes in the elements of the array(because ``int`` is 4 bytes).

variable name point to first element of the array.

Basically, &x[i] is equivalent to x+i and x[i] is equivalent to *(x+i).

**array names decays(converted) to pointers**:
~~~c
#include <stdio.h>
int main() {
  int i, x[6], sum = 0;
  printf("Enter 6 numbers: ");
  for(i = 0; i < 6; ++i) {
  // Equivalent to scanf("%d", &x[i]);
    scanf("%d", x+i);

  // Equivalent to sum += x[i]
    sum += *(x+i);
  }
  printf("Sum = %d", sum);
  return 0;
}
// Enter 6 numbers:  2
//  3
//  4
//  4
//  12
//  4
// Sum = 29 

#include <stdio.h>
int main() {
  int x[5] = {1, 2, 3, 4, 5};
  int* ptr;

  // ptr is assigned the address of the third element
  ptr = &x[2]; 

  printf("*ptr = %d \n", *ptr);   // 3
  printf("*(ptr+1) = %d \n", *(ptr+1)); // 4
  printf("*(ptr-1) = %d", *(ptr-1));  // 2

  return 0;
}

// *ptr = 3 
// *(ptr+1) = 4 
// *(ptr-1) = 2
~~~

cases array dont decay to pointer:
- it's the argument of ``&``
- it's the argument of ``sizeof``
- its a string literal of type ``char [N + 1]`` or a wide string literal of type wchar_t [N + 1] (N is the length of the string) which is used to initialize an array, as in char str[] = "foo"; or wchar_t wstr[] = "foo";.

## dynamic memory allocation
when the size of the array you declared is insufficient, you can allocate memory manually during run-time.

function used in ``stdlib.h`` for allocating memory:
- ``malloc()``(reserves a block of memory of the specified bytes and returns a pointer of void that can be casted into pointers of any form)
- ``calloc()``(contiguous allocation. allocates memory and initializes all bits to 0)
- ``realloc()``(can change an allocated memory especially when the size is insufficient)
- ``free()``(deallocating the memory)

# Strings
a sequence of characters enclosed in the double quotation marks, it appends a null character at the end by default.

conflict with array when assigning value once declared(can use ``strcpy()`` to solve this).

use ``fgets()`` to get a string with spaces from user input and puts to display.

strings also decayed to pointers.

string handling function are defined under ``string.h`` header file(except for ``gets()`` and ``puts()``).

~~~c
for (i = 0; s1[i] != '\0'; ++i) // string loop trick
~~~

# Structure
collections of variables(can be different types) under a single name.

~~~
struct structureName 
{
    dataType member1;
    dataType member2;
    ...
};
~~~

~~~c
// Program to add two distances (feet-inch)
#include <stdio.h>
struct Distance 
{
    int feet;
    float inch;
} dist1, dist2, sum; // these variables are of type struct Distance

int main()
{
    printf("1st distance\n");
    printf("Enter feet: ");
    scanf("%d", &dist1.feet);

    printf("Enter inch: ");
    scanf("%f", &dist1.inch);
    printf("2nd distance\n");

    printf("Enter feet: ");
    scanf("%d", &dist2.feet);

    printf("Enter inch: ");
    scanf("%f", &dist2.inch);

    // adding feet
    sum.feet = dist1.feet + dist2.feet; // accessing members of a structure using a member operator (.)
    // adding inches
    sum.inch = dist1.inch + dist2.inch;
~~~

you can create nested structure.

you can create pointers to structs and allocates its memory during runtime(dynamic allocation of structs).

## Unions
a user-defined type similar to structs.

the different of ``union`` with ``structure`` is:
- in union all members share the same memory which means the size of a union is the size of its largest element.
- can access all struct members at once, union can only one at a time(since all of the share memory).

# Bitwise Operator

~~~
// AND operator & //
12 = 00001100 (In Binary)
25 = 00011001 (In Binary)

Bit Operation of 12 and 25
  00001100
& 00011001
  ________
  00001000  = 8 (In decimal)

12 = 00001100 (In Binary)
25 = 00011001 (In Binary)

Bitwise OR Operation of 12 and 25
  00001100
| 00011001
  ________
  00011101  = 29 (In decimal)

12 = 00001100 (In Binary)
25 = 00011001 (In Binary)

Bitwise XOR Operation of 12 and 25
  00001100
^ 00011001
  ________
  00010101  = 21 (In decimal)

35 = 00100011 (In Binary)

Bitwise complement Operation of 35
~ 00100011  // an unary operator that changes 1 to 0 and 0 to 1.
  ________
  11011100  = 220 (In decimal)

// right shift operator //
212 = 11010100 (In binary)
212>>2 = 00110101 (In binary) [Right shift by two bits]
212>>7 = 00000001 (In binary)
212>>8 = 00000000 
212>>0 = 11010100 (No Shift)

// left shift operator //
212 = 11010100 (In binary)
212<<1 = 110101000 (In binary) [Left shift by one bit]
212<<0 =11010100 (Shift by 0)
212<<4 = 110101000000 (In binary) =3392(In decimal)
~~~
## twist in bitwise complement
the bitwise complement of 35 is -36 instead of 220 because for any integer ``n``, its bitwise complement will be ``-(n+1)``(two's complement).

**two complements** is used in computing as a method of signed number representation(representing negative and positive numbers).