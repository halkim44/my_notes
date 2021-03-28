# NestJS

## Introduction

- is a framework for building efficient, scalable Node.js server-side apps.
- is build with and fully supports Typescript
- combines elements of Object Oriented Programming, Functional Programming and Functional Reactive Programming.
- use Expressjs under the hood(can be configured to use Fastify)
- provide level of abstraction above the common Node.js framework(Express/Fastify), but also exposes their APIs directly to the developer.
- provides an out-of-the-box application architecture which allows developers and teams to create highly testable, scalable, loosely coupled, and easily maintainable app(inspired by Angular)
- it is cear architecture based on few simple components(controllers, modules and providers). this give great ease to split application
- offers dependency injection out of the box
- Easy Unit testing
- prevent the developer from mistake early on in the project regarding the architecture.

## Controllers

- handling incoming **request** and returning **responses** to the client.
- the **routing** mechanism controls which controller receives which requests.
- Decorators associate classes with required metadata and enable Nest to create a routing map.

to define a controller:

- include @Controller decorator
- @Controller("prefix") will make the controller handle all `/prefix` request
- add request decorator @Get, @Put, @Post, @Delete
- request decorators can also have prefix( will match the request in `/controllerPrefix/requestPrefix`)
- needs to be added to the module definition bef

## Providers

many of the basic Nest classes may be treated as a provider ― services, repositories, factories, helpers, and so on.

- providers are designed to abstract any form of complexity and logic
- can be injected into any controllers or other providers
- are also called **services**
- are simply a class annotated with an `@Injectable()` decorator

### Scopes

- when the application is bootstrapped, every dependency must be resolved, and therefore every provider has to be instantiated.
- when app shuts down, every provider will be destroyed
-

## Modules

- group related files
- typescript files decorated with @Module decorator that will be used to organize app structure.
- each Nestjs must have at least one module(root module)
- break a large app into multiple modules as it helps to maintain the structure of the application
-

### Global Module

- Nest encapsulates providers inside the module scope preventing using the providers elsewhere
- we can provide a set of providers which should be availabe everywhere using the `@Global` decorator
- global is not a good design desicion and should be used to reduce the amount of necessary boilerplate.

### Dynamic Modules

- create a customizable modules that can register and configure providers dynamically.

### The @Module object properties properties

- providers
- controllers
- imports (the list of imported modules that export the providers which are required in the module)
- exports (subset of providers that are provided by this module and should be available in other modules)

## Other important concepts in NestJs

- **DTO** ― Data Transfer Object is an obj that defines how data will be sent over the network.
- **Interfaces** ― used for type-checking and defining the types of data that can be passed to a controller or a Nest service.
- **Dependency Injection** ― a design pattern used to increase efficiency and modularity of apps. keep code clean and easier to use.

## Data Transfer Object(DTO)

- for type-checking
- to define the structures of what an object looks like when creating a new book
- could be determined by using TS interface or classes
- recommended to use classes, because features such as Pipes enable additional possibilties when they have access to metatype of variables at runtime.

## Exception Filters

when an exception is not handled by our app code, it is caught by the **global exception layer** which handles exceptions of type HttpException.

nest provide a built in HttpException class exposed from the @nest/common package.

Exception filters let you control the exact flow of control and the content of the response sent back to the client.

## Pipes

is a class annotated with the **@Injectable** decorator and should implement the PipeTransform interface.

has two typical use case:

- transformation(transform input data to desired form e.g. string to integer)
- validation (evaluate input data)

## Testing

- Nest automatically scaffolds default unit tests for components and e2e tests for applications.
- provides integration with Jest and Supertest out-of-the-box.
- make the Nest dependency injection system available in testing environment.
- nest doesnt force any specific tooling in testing(can use whatever I want)

### Test module

Test:

- providing an application execution context
- mocks the full Nest runtime
- provide hooks that make it easy to manage class instances, including mocking and overriding.
- has `createTestingModule()`

## Authentication

### Passport

- a popular node.js auth library.
- can be integrated in Nest using **@nestjs/passport**

Passport executes a series of steps to:

- authenticate a user by verifying their "credentials"(username/password, JWT, or identity token from an Identity Provider)
- Manage authenticated state
- Attach information about the authenticated user to the **Request** object for further use in route handlers

### Authentication Requirement

- client authenticat with a username and password
- server issue JWT
- protected route that is accessible only to request that contain a valid JWT

### how vanilla passport works

in vanilla passport, you configure a strategy by providing two things:

- a set of options that are specific to that strategy
- a verify callback ― where you tell Passport how to interact with your **user store**.

## Guards

Guards determine whether a given request will be handled by the route handler or not.

middleware is used for handling authentication, but middleware is dumb because it will not now which handler will be executed after `next()`.

Guards has access to ExecutionContext instance, thus know exactly whats going to be executed next.

are executed after middlewares, but before interceptor or pipe.

guard must implement `canActivate()` function which return boolean. can return either async or sync. **true** will proceed, falls will deny request.

### Execution context



## Encryption and Hashing

Nest has built-in **crypto module** that you can use to encrypt and decrypt strings, numbers, buffers, streams, and more.

## Validation

- automatically validate incoming request, nest provide:
- ValidationPipe
- ParseIntPipe
- ParseArrayPipe
- ParseBoolPipe
- ParseUUIDPipe

make use of class-validator

## Middleware

- is a function which called before the route handler.
- have access to request and response objects and next().
- equivalent to express middleware.

middleware can do:

- execute any code
- make changes to the request and response object
- end request-response cycle
- call the next middleware function

if middleware does not end the request-response cycle, it must call next() to pass control to the next middleware function or the request will be left hanging

```js
import { Module, NestModule, MiddlewareConsumer } from "@nestjs/common";
import { LoggerMiddleware } from "./common/middleware/logger.middleware";
import { CatsModule } from "./cats/cats.module";
import { CatsController } from "./cats/cats.controller.ts";

@Module({
  imports: [CatsModule],
})
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer
      .apply(LoggerMiddleware)
      .exclude(
        { path: "cats", method: RequestMethod.GET },
        { path: "cats", method: RequestMethod.POST }
      )
      .forRoutes(CatsController);
  }
}
```

**forRoute()** can take:

- a single or multiple string
- a RouteInfo object
- single or multiple controller class separated by commas

**apply()** may take a single middleware or multiple arguments to specify multiple middleware.

use functional than class when middleware doesn't need any dependecies.

## Request lifecycle

In general, a request flows through(in order):

- middleware
- guard
- interceptors
- pipes
- back to interceptors on the return path(as the response is generated)

### Middleware

nest runs:

1.  globally bound middleware
2.  module bound middleware

middleware run sequentially in the order they are bound(similar to express middleware)

in case of middleware bound across different modules, middleware bound to root modules will run first, then middleware will run in the order that the module are added to the imports array.

### Guards

run order:

1. global guards
2. controller guards
3. route guards

### Pipes

follow the standard global to controller to route bound sequence, with the same first in first out in regards to the @usePipes() parameters.

### Filters

- is not global first.
- resolve from the lowest level possible.
- starts with any route bound filters and proceeding next to controller level, and finally to global filters.

In general, the request lifecycle looks like the following:

- Incoming request
- Globally bound middleware
- Module bound middleware
- Global guards
- Controller guards
- Route guards
- Global interceptors (pre-controller)
- Controller interceptors (pre-controller)
- Route interceptors (pre-controller)
- Global pipes
- Controller pipes
- Route pipes
- Route parameter pipes
- Controller (method handler)
- Service (if exists)
- Route interceptor (post-request)
- Controller interceptor (post-request)
- Global interceptor (post-request)
- Exception filters (route, then controller, then global)
- Server response

## Guards
