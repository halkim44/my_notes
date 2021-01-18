# React Testing Library Notes

"The more your tests resemble the way your software is used the more confidence they can give you."

## afterEach(cleanup)

Since we are not using shallow render we have to unmount or cleanup after every test. And this is exactly what this function is doing.

## testing useEffect and API request

A mock is way to simulate behavior we dont actually want to do in our tests.

` waitForElement()` function, which will wait until the promise resolves before going to the next assertion.
