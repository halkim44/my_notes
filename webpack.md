# webpack

is a module bundler and has a broader definition of what a module is.

for webpack module is:

- CommonJS modules
- AMD modules
- CSS import
- Images url
- ES modules

webpack is able to ingest dependencies from any of these sources.

the goal is to unify all resources to and finally produce a shippable output.

## Entry point

the starting point from which all dependencies of a front end project are collected.(`src/indec.js`)

## Output

the resulting javascript and static files collected during the build process. (`dist/`)

## Loaders

third-party extensions that help webpack deal with various file extensions.

the goal is to transform file other than js to modules.

## Plugins

third party extensions that can alter how webpack works.

## Mode

**development** and **production**.

## Code Splitting

devs can decide to load whole blocks of js only response to some user interaction.

splitted piece of code is called **chunk**.
