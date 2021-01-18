# Intersection Observer API

asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's viewport

register a callback function that is executed whenever an element they wish to monitor enters or exits another element (or the viewport), or when the amount by which the two intersect changes by a requested amount.

## Concepts

configure a callback that is called when either of these circumstances occur:

- **target** element intersect with device's viewport or an element
- the first time the observer is initially set to watch a target element

degree of intersection between the target element and its root is the intersection ratio.

Create the intersection observer by calling its constructor and passing it a callback function to be run whenever a threshold is crossed in one direction or the other

```javascript
let options = {
  root: document.querySelector('#scrollArea'),
  rootMargin: '0px',
  threshold: 1.0 // means that 100% of the target is visible within the element(root)
}

let observer = new IntersectionObserver(callback, options);
```