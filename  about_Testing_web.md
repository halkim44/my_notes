# Testing

## Unit Testing

unit test have the narrowest scope of al. it make sure that a certain unit in the codebase works as intended.

## mount vs shallow

**mount** ― actually executes the html, css and js code like a browser would in a simulated way. used for integration testing.

**shallow** ― only renders the single component we are testing and does not render child components for test isolation. used for unit testing.

## unit vs integration vs end to end

**unit** ― testing an isolated part of the app.

**integration** ― if different parts work or integrate with each other.

**e to e testing** ― Usually a multi step test combining multiple unit and integration tests into one big test.

## other terms

**snapshot test** ― allows you to see how your component has cchanged since the last test.
