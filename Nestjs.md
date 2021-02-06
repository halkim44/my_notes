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
