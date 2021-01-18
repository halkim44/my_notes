# Typescript

- typescript is compiled to javascript. it is more stricter than javascript.
- you will get an error if a certain variable is not confirmed will have a value.
- we get an error during development.

**javascript** is dynamically typed while **typescript** is statically typed.

## Types

- number(no diff between int and float)
- string
- boolean
- object
- array
- tuple
- enum
- any

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

- automatically enumerated global constant identifiers

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

##

## coder note

- dont open the ts and js file at the same time(in diffrent tabs). it will produce duplicate function error
- there is `any` type but using it will lose the benefit of typescript so use it less(use js la if still want to use any)
- `+varName` will convert to number

```

```
