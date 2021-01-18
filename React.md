## Hooks

- before hooks, there is no way to use state in functional components in React
- because function components is less clunky and more readable than class components

### useEffect

when a component's variable or state changes based on some outside thing.

is a side effect because we cannot be sure of the action will be.

the same as `componentDidMount()` and `componentDidUpdate()`

Note: will run on every render and re-render. the second parameter solve this.

the second parameter contains list of things that will cause the useEffect hook to run.(passing an empty array will make it run only once like `componentDidMount()`)

the return statement in the function in the first parameter will run when the component is about to unmount.

## Context

provides a way of passing data through the component tree via Provider-Consumer pair without having to pass props down through every level

provide a way to make particular data available to all components throughout the component tree no matter how deeply nested that component may be

### Provider

every context object comes with a Provider React component that allows consuming components to subscribe to context changes.

allows the context to be consumed by other components.

### Consuming context with class based Components

#### through Class.contextType

- assign context object to `contextType` property of the class
- able to access the context value using `this.context`

#### ThemeConsumer.Consumer

- Each context object also comes with a Consumer React component which can be used in a class-based component
- consumer component takes a child as a function and that function returns a React node
- current context value is passed to that function as an argument

### Consuming context with Functional Components

- easier and less tedious
- using a hook called `useContext`

### React Redux

#### Provider

is a wrapper component from React Redux that wraps the React app allowing access to Redux store and dispatch functions throughout the component tree.

takes two props, the Redux store and the child components of your app.

allows to provide state and dispatch to React Components

## Code Splitting

Code-Splitting is a feature supported by bundlers like Webpack, Rollup and Browserify (via factor-bundle) which can create multiple bundles that can be dynamically loaded at runtime.

can help with "lazy-load" avoid loading the code that the user may never need

### Import()

when webpack come across this syntax, it automatically starts code-splitting the app.

### React.lazy

takes a function that must call a dynamic `import()`. This must return a `Promise` which resolves to a module with a default export containing a React component

lazy component should be rendered inside a Suspense component, which allows us to show some fallback content(such as a loading indicator)

currently only support default exports

## Memoization

an optimization technique which passes a complex function to be memoized or remembered.

the result is remembered, when the same exact parameters are passed in subsequently.

optimize components by avoiding complex re-rendering when it isn't intended.

## React-router

**Routing** is the process of keeping the browser URL in synch with whats being rendered on the page.

React router is a third-party library that lets you handle routing declaratively.

comprise of 3 packages:

- react-router(core)
- react-router-dom(for web app)
- react-router-native(for mobile)

### Basic

#### 1. wrap `<App>` in a `<Router>` using BorwserRouter or HashRouter

**BrowserRouter** uses the HTML5 History API to keep UI in synch with URL.(http://example.com/about)

**Hashrouter** uses the hash portion of the URL window.location.hash.(http://example.com/#/about)

```jsx
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
import { BrowserRouter } from "react-router-dom";

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById("root")
);
```

the above code will creates a History instance for <App> component.

**History** library lets you manage session history anywhere Javascript runs. the history object lets you manage the history stack, navigate, and persist state between sessions.

Each `<Router>` creates a history object that keeps track of the current and prev locations in stack.

we use `history.push` and `history.replace` to change location.

`history.push` is invoked when clicking `<Link>` and `history.replace` is invoked using `<redirect>`.

#### 1. Link And Route

the `<Route>` render the UI if the current location matches it's path.

the `<Link>` is used to navigate between pages.

there are a few other methods you can use to render something with a `<Route>`(these are provided mostly for supporting apps that were built with earlier versions of the router before hooks were introduced)

- components
- render
- children

##### Path and Match

the `path` uses **Path-to-RegExp** library to turn a path string into a regular expression and then matched against the current location.

if router's path and location are match, a **match object** is created which contains more info about the URL and the path:

- match.url
- match.path
- match.isExact
- match.params

##### Implicit passing of props

```jsx
<Route exact path="/" component={Home} />

// will log the following

{
  history: { ... }
  location: { ... }
  match: { ... }
}
// while

<Route exact path="/"><Home /></Route> // wil log {}

```

`<Switch>` ― when wrapping multiple `<Route>`, only the first child Route that match the location is rendered.

`/:id/` ― is used for dynamic routing. make the value in `id` available in component.

`useRouteMatch` hook ― used to gain access to `match` object.

`useParams` hook ― to access params object.

`<Redirect>` ― replace the current location in the history stack with a new location.

## Testing React

### React Testing Library

a lightweight test utility that encourages the developer to test their application in the same way that it’ll be used.

exports a render function that always does a full mount on the component.

#### render function

the render function is similar to the way react-dom renders a component onto the DOM, but it returns an object which we can destructure to get some neat test helpers.

`get` test helpers will fail test if doesnt found an element while `query` test helpers doesnt.