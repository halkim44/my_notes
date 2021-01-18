# Redux

- a state management framework that can be used with a number of different web technologies.
- there is a single state object that's responsible for the entire state of the application(Redux `store`)
- any update must do so through the Redux `store`
- easier to track state management
- `state` is ``read only

## Redux store

holds and manages application `state`

## Action

- all state updates are triggered by dispatching `actions`.
- is a JS object that contains information about an action event that has occured.
- sometimes carries data
- must carry a `type` property that specify the type of action

## Reducer

- responsible for the state modifications that takes place in response to actions.
- its **only** role is takes state and action as arguments and return a new state.

when the state grow more complex, you define multiple reducer to handle different pieces of your application state then compose it into one root reducer.

## Listener

`subscribe` will call the callback function passed when when store receives an action.

## Redux Thunk Middleware

for when need to call asynch endpoints.

```js
const store = Redux.createStore(
  asyncDataReducer,
  Redux.applyMiddleware(ReduxThunk.default)
);
```

## connecting react with redux

1. install **react-redux**
2. Setup Provider
3. use `connect` method
4. `mapStateToProps` or `mapDispatchToProps`

### mapStateToProps and mapDispatchToProps

**mapStateToProps** connect a part of the redux state to the props of a React component. the component will have access to the exact part of the store it needs.

**mapDispatchToProps** is similar, but for actions. this way a connected react app will be able to send messages to the store.

## Redux Middleware

redux middleware is a function that is able to intercept, and act accordingly, our actions, before they reach the reducer.

in its basic form react middleware is **a function returning a function, which takes next as a parameter. then the inner function which takes action as parameter and finally returns next(action).**

`getState` and `dispatch` is also accessible in the middleware.

## Asynchronous actions in Redux

calling `Fetch` from an action creator does not work because Redux is expecting an object as actions but recieve a Promise.

### Redux-thunk

redux-thunk is middleware that allow us to call APIs in action creators or delay the dispatch of an action and more.

with redux-thunk we can return function from action creator not just objects.

### redux-saga

- is a middleware for managing side effects.
- with it you can have a separate thread in your app for dealing with impure actions.
- can have clear separation between sync and async logic

redux saga structure can live in a single file containing:

- a watcher function (a generator function watching for every action we are interested in)
- a worker function (a generator function that will perform API call)
