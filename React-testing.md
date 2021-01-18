# React Testing

## What is testing

testing 3 step process:

- arrange(arrange your app in a certain original state)
- act (then something happens)
- assert (then you assert or hypothesize of the new state of the app)

## Drawbacks of testing

- time consuming
- can cost actual money
- give false positive/negative if done incorrectly

## What to test?

Instead of focussing on the code and how it works we simply take the perspective of the user. This forces us to focus on testing the important parts of the application.

Best Advice: Many integration tests. No snapshot tests. Few unit tests. Few e to e tests.

### What not to test?

- implementation details
- const variable
- third parties libraries
-

## screen.debug

print the DOM tree.

takes a parameter. this way you can output a single element to the console.

## how to access rendered DOM tree

to access rendered elements is via the screen object which is exported from Testing Library

screen object queries:

- getby\* (TestId, Text, Role) - these functions are synchronous and check if an element is currently inside the DOM
- findBy\* - asynchronous functions. wait for a certain time(5 sec) until an element appears in the DOM
- queryBy - are asynchronous but return null when an element is not present

Use test IDs only when there's no other query you can use

## Event

there are two options

- `fireEvent` that is exposed by `@testing-library/react`
- `click` functon from `@testing-library/user-event`

its recommended to use `@testing-library/user-event` it contains more events that are closer to real user event.

## Misc Advices

- Testing Reducers is one unit test that is always necessary.

## Testing with cypress

To actually run the cypress tests, your app will have to be running at the same time.

run `cypress open` command will give you basic config of cypress and create some files and folders for you automatically.

Unlike unit and integration tests we do not need to explicitly assert some things because some cypress commands have built in default assertions.

Even when testing with cypress we will stick to our philosophy of not testing implementation details.

`cy.contains()` command which will return a DOM node with matching text.

## Continuous Integration

A way to automatically run our tests continuously.

- Travis CI
- Docker
- Jenkins
- Coveralls(gives us coverage report of how much our code is being tested.)

## Integration tests

test the integration between various components of an application.They validate how a user interacts with your app without the overhead of e2e tests.

in react, unit and integration tests are written the same way with the same tools.

in React, this means testing

- iteractions between React components
- manipulation of component state
- direct manipulation of the DOM in react lifecycle methods

### Enzymes

the same features that allow you to easily unit test React components: access to component props and state, encourages poor testing practices when writing integration component tests.

## What is react-test-renderer

a library for rendering react components to pure javascript objects.