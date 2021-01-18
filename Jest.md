# Jest

a javascript test runner that is, a javascript library for creating, running and structuring tests.

## how a typical test flow look like

1. import function to test
2. give input to function
3. define what to expect as an output
4. check if function produces the expected output

## describe

jest method for containing one or more related tests.

## matcher

a jest function for checking the output.

## manual mocks

manual mocks are used to stub out functionality with mock data.

manual mocks are defined by writing a module in a `__mocks__/` subdirectiory immediately adjacent to the module.

### Mocking node_modules

the mocks should be placed in the `__mocks__` directory adjacent to `node_modules` and will.

## Understanding Jest Mocks

mocking is technique to isolate test subjects by replacing dependencies with objects that you can control and inspect.

### Mock Functions

```js
jest.fn();
```

the goal is to replace something we dont control with something we do.

the mock function provide features to:

- capture calls
- set return values
- change implementation

### mocking modules and functions

3 types of module and function mocking in jest:

- `jest.fn`
- `jest.spyOn`
- `jest.mock`
