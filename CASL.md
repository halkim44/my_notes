# CASL

- an isomorphic authorization JS library which restricts what resource a given client is allowed to access.
- incrementally adoptable and can easily scale between a simple claim based and fully featured subject

## Ability

Ability allows us to check permissions in pretty readable way.

## How CASL detect subject type

gets object.constructor.modelName as subject type and if this is not available, it fallbacks to object.constructor.name.
