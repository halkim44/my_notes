# Angular notes

## adding navigations

routes are collected in `app.module.ts`.

### ActivatedRoute

contains information about route and the route's parameters.

## Components

each components consists of:

- html template
- Typescript class that defines behavior
- Css selector
- Css styles

### Css selector

every component requires a CSS selector.

a selector instructs Angular to instantiate this component wherever it finds the corresponding tag in template HTML.

### Templates

a block of HTML that tells Angular how to render the component in your application.

can define a template in two ways:

- referencing an external file(templateUrl prop in @Component)
- directly inside the component(template prop in @Component)

### lifecycles

1. Angular instantiates the component class and renders the component view along with its child views.
2. Angular checks to see when data-bound properties change, and update both the view and the component instance as needed.
3. lifecycle ends when Angular destroys the component instance and remove its rendered templates from the DOM.

Directive has similar lifecycle.

## tools to check

- [ ] `currency` transform a number into price format
- [ ] `HttpClient`

## Intro of Angular's concept

Angular is written in typescript.

the basic building blocks of the angular framework are Angular components that are organized into NgModules.

an app always has at least a **root module** tht enable bootstrapping, and typically has many more feature modules.

- Components _view_ which are sets of screen elements that Angular can choose among and modify according to the program logic and data
- _services_ - provide specific functionality not directly related to views.

Modules, components and services are classes that use decorators that will mark their type and provide metadata that tells Angular how to use them:

- The metadata for a component class associates it with a template that defines a view. A template combines ordinary HTML with Angular directives and binding markup that allow Angular to modify the HTML before rendering it for display.
- The metadata for a service class provides the information Angular needs to make it available to components through dependency injection (DI).

### Modules (NgModules)

differ from and complement JavaScript (ES2015) modules.

an NgModules:

- declares a compilation context for a set of componentsthat is dedicated to an app domain, workflow, or related sets of capabilities.
- can associates its components with related code(such as _services_)

every Angular app has a **root modules**(conventionally named AppModule) which provide the bootstrap mechanism that launches the app.

an app contains many functional modules.

NgModules can import functionality from other NgModules, and allow their own functionality to be exported and used by other NgModules.

### Components

every Angular app has _root_ component that connect the components hierarchy with the page DOM.

Each Components define a class that contains app data and logic, and is assiciated with an HTML _template_ that defines a view to be displayed in a target environment.

### Templates, directives and data bindings

A template combines HTML with Angular markup that can

### Services and dependency injection

_service_ is data or logic that isn't associated with a specific view, and that is shared across components.

_Dependency Injection_ keep component classes lean and efficient by delegating tasks(such as fetching data, validate user input ...) to services.

#### Dependency Injection

- are services or objects that a class needs to perform its function.
- a design pattern in which a class requests dependencies from external sources rather than creating them.

#### Routing

Route NgModules provides a service that lets you define a navigation path among the different application states and view hierarchies in your app.

router intercepts the browser's behavior(such as user clicking a link) and show or hides view hierarchies.

## What is a Decorator?

a decorator is simply a way of wrapping one piece of code with another.

Decorators are also a function that modify Javascript classes.

```js
function doSomething(name) {
  console.log("Hello, " + name);
}

function loggingDecorator(wrapped) {
  return function () {
    console.log("Starting");
    const result = wrapped.apply(this, arguments);
    console.log("Finished");
    return result;
  };
}

const wrapped = loggingDecorator(doSomething);

// output

doSomething("Graham");
// Hello, Graham

wrapped("Graham");
// Starting
// Hello, Graham
// Finished
```
