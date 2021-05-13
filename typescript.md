# Typescript

- typescript is compiled to javascript. it is more stricter than javascript.
- you will get an error if a certain variable is not confirmed will have a value.
- we get an error during development.

**javascript** is dynamically typed while **typescript** is statically typed.

## Types

1. number(no diff between int and float)
2. string
3. boolean
4. object
5. array
6. tuple
7. enum
8. any
9. BigInt

### number

- no different between int and float. they all are numbers.

### Object

- Typescript give error when trying to access a non existing property of object.

```typescript
const person: {
  name: string;
  age: number;
} = {
  name: "Halkim",
  age: 23,
};
// but its better not to use this
```

### Array

- set the type of an array like this

```typescript
let sports: string[];
```

- when looping on an array IDE will suggest the correct methods to use for the array child
- will give an error early in development when using the wrong method

### Tuple

```typescript
const person: {
  name: string;
  age: number;
  role: [number, string]; // THIS IS A TUPLE
} = {
  name: "Halkim",
  age: 23,
  role: [2, "sniper"],
};
// but its better not to use this
```

- tuple is when you when you want an array with exactly n-number of element and what type resides in each element
- TS will give error if adding or modifying an element of a tuple
- adding element with `push()` will not give error on tuples (BE AWARE)

### Enum

- Enums or enumerations allow us to declare a set of named constants a collection of related values that can be numeric or string values.

three types of enums:

- Numeric
- String
- Heterogeneous

### Numeric Enums

- are number-based enums they store string values as numbers.
-

## Union types

```typescript
// Union type
function combine(input1: number | string, input2: number | string) {}
```

## Type alias

```typescript
type combinable = string | number;
```

## Functions

- in an IDE, if hover on a function name it will show information about the function and also its return type

```typescript
function functionName(arg1: argType): returnType;
function add(n1: number, n2: number): number;
```

- will throw an error if the return value's type is not the specified returnType
- there is a return type `: void` means the function doesnt return anything
- `: undefined` must specify at least return statement to avoid error while `: void` dont need anything to prove that the function doesnt return anything

### function type

```typescript
let combineValue: Function;
let cimba: () => number;
let cimba: (a: number, b: number) => number;
function addAndHandle(n1: number, n2: number, cb: (num: number) => void) {
  const result = n1 + n2;
  cb(result);
}
```

## Unkown type

- we dont know yet what the user will eventually enter
- can store any value in unknown type variable without getting errors

```typescript
let userInput: unknown;
let userName: string;

userInput = "Max";
userName = userInput; // this will be ERROR
```

## Never Type

- a newer type
- state that the function is to never return anything and essentially crash/break the script

```typescript
function generateError(message: string, code: number): never {
  throw { message: message, errorCode: code };
}
```

## tsc compiler

```
tsc app.ts --watch // watch mode on app.ts

tsc --init // initialize the project in which this command is called(will create tsconfig.json)

tsc // after the above command this command will compile all available typescript file inside the project
```

## what we can do with tsconfig.json

**we can**

- exclude a list of files
- include a list of files

**we can control how our typescript files are compiled**

- target javascript version to compile to
- you can specify library files to be included(this is useful when using tsc for other application than for the browser like node.js)
- include js file into the compilation
- include tsc file on the list source file when debugging on the browser
- tell the compiler where to output the compiled file
- tell the compiler where to output the compiled file
- remove comment in the compiled files
- tell the compiler to report and not ouput any js file
- tell the compiler to not output a js file if an error occured
- enable strict type checking options
- code quality checks(unused var, implicit return type)
- experimental options

## coder note

- dont open the ts and js file at the same time(in diffrent tabs). it will produce duplicate function error
- there is `any` type but using it will lose the benefit of typescript so use it less(use js la if still want to use any)
- `+varName` will convert to number

## Interface

interface is like a contract, a "model" for your entitiy.

code editor will detect the type for each properties.

can be extended like `Class`.

can describe function, not only objects.

## type

used to describe a custom shape, but its just an alias, or put in another way, a label for a custom type.

interface and type are used interchangeably in TypeScript.

use interface over type alias if possible.

## Access Modifiers

access modifiers specifies the accessibilty or scope of a field, method, constructor, or class.

three types of access modifiers: - public - private - protected

### Public

public members can be accessed anywhere without any restrictions. all members of a class are public by default.

TS will treat any property and methods as public by default if no modifier is applied.

### Private

ensure that class members are visible only visible to that class and are not accessible outside the containing class.

### Protected

similar to private except that protected members can be accessed using their deriving classes.

## Decorators

- is a pattern in programming in which you wrap something to change its behavior.
- a special kind of declaration that can be applied to classes, methods, accessor, property, or parameter.
- a function that are prefixed `@expression`, where expression must evaluate to a function that will be called at runtime with information about the decorated declaration.

## Object Types

### Extending types

- copy members from other named types and add whatever new members we want.
- useful in cutting down the amount of type declaration boilerplate we have to write.

### Extending and Intersection

- both do almost the same thing
- the main difference is how conflict is handled

## Generic Types

```ts
// instead of this
interface NumberBox {
  contents: number;
}
interface StringBox {
  contents: string;
}
interface BooleanBox {
  contents: boolean;
}

// we can write it like this
interface Box<Type> {
  contents: Type;
}
type OrNull<Type> = Type | null;
type OneOrMany<Type> = Type | Type[];
```

### The Array Type

`Array` itself is a generic type.

```ts
interface Array<Type> {
  /**
   * Gets or sets the length of the array.
   */
  length: number;

  /**
   * Removes the last element from an array and returns it.
   */
  pop(): Type | undefined;

  /**
   * Appends new elements to an array, and returns the new length of the array.
   */
  push(...items: Type[]): number;

  // ...
}
```

### The ReadonlyArray Type

- a special type that describe array that shouldn't be changed.
- we can set an Array without worrying about the content being changed.
- unlike `Array`, no constructor we can use instead we can assign Arrays to ReadonlyArrays:

```TS
const roArray: ReadonlyArray<string> = ["red", "green", "blue"];
```

- TS also provides a shorthand syntax for `ReadonlyArray<Type>` with `readonly Type[]`.
- unlike the readonly property modifier, assignability isn’t bidirectional between regular Arrays and ReadonlyArrays.

```TS
let x: readonly string[] = [];
let y: string[] = [];

x = y;
y = x;
```

### Tuple Types

- another sort of Array types that knows exactly how many elements it contains, and exactly which types it contains at specific positions.
- will get an error if try to index past the number of elements.
- can be destructured using JS Array destructuring.
- can have optional props
- can also have rest elements, which have to be an array/tuple type.
- rest and optional element in Tuple is useful in function parameters.

```ts
// this
function readButtonInput(...args: [string, number, ...boolean[]]) {
  const [name, version, ...input] = args;
  // ...
}

// is equal to
function readButtonInput(name: string, version: number, ...input: boolean[]) {
  // ...
}
```

- tuples can also be `readonly`.

## Creating Types from Types

### Generics

```ts
function identity<Type>(arg: Type): Type {
  return arg;
}
```

- `<Types>` allows us to capture the type the user provides.
-
