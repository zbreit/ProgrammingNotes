---
title: Functional Programming
tags: [Notebooks/JS]
---

# Functional Programming
Notes from the JS Functional Programming tutorial on [FreeCodeCamp](https://www.freecodecamp.org/)
## Terminology
 - **Pure Function**: A function with no side-effects (on the supplied data, the console, etc.)
 - **Callback Function**: A function that is supplied to and invoked by another function 
 - **First Class Function**: A function that can be passed into or returned by other functions
    - In JS, all functions are **first class**
 - **Higher Order Function**: A function that is supplied a function or that returns a function
 - **Lambda**: A function that is passed around/returned by a higher order function
## Hazards of Imperative Programming
 - **Imperative Programming** is concerned with the steps/commands that are used to implement specific actions
    - Ex. Using a `for` loop to decide exactly how to iterate over an array
 - **Declarative Programming** involves telling the computer *what* to do using function calls
    - Ex. Using `map` to handle array iteration for you
## Design Principles
### Avoid External Dependencies
  - Any function computation should depend only on its parameters, not any global values or functions
     - This makes your function more modular, easier to write tests for, and explicitly states its inputs
### Don't Alter Data
 - Keep your functions free of side effects by returning new objects and variables intead of mutating the original values
    - In ES6, this means using the spread operator (`...`) a lot to create copies of supplied data structures
## Functional Programming Tools in JS
### Pure Functions
All of the following methods are higher order, pure functions that don't mutate their inputs
 - `Array.prototype.map(func)`: Returns a new array with `func` applied to each element of `this`
 - `Array.prototype.concat(newArr)`: Returns a new array with all elements in `newArr` added to the end of `this`
 - `Array.prototype.reduce(func, initialVal)`: Accepts `func`, which has two parameters: `accumulator` and `currentEntry`. The `reduce` function will call `func` with each element of the array and the return value will be passed in as `accumulator` for the next entry. `initialVal` sets the starting value of the accumulator.
 - `Array.prototype.every(func)`: Returns true if `func(element)` returns `true` for all elements in the array
 - `Array.prototype.some(func)`: Returns true if `func(element)` returns `true` for any element in the array
### Functions with Sideffects
The following methods are not pure (meaning they mutate the original array)
 - `Array.prototype.sort(func)`: Return a new array that is sorted based on `func`. `func` takes in two parameters, `a` and `b`. It returns a negative (falsy) value if `a` should be placed before `b`, a positive (true) value if `a` should be placed after `b` and 0 if they're equivalent.
    - If `func` isn't supplied, the elements will be sorted based on Unicode values (which leads to weird results).
## Decomposing Functions
 - `Arity`: The number of arguments a function accepts
 - `Currying`: Expanding a function an `arity` of N into N functions of `arity` 1.
```js
function add(x, y) {
  return x + y;
}

function addCurried(x) {
  return function(y) {
    return x + y;
  }
}

addCurried(3)(4); // 7
```
 - This pattern allows you to save intermediate function results and only call the function with all of the parameters later
```js
function addInSteps(x, y) {
  return function(z) {
    return x + y + z;
  }
}

let intermediateStep = addInSteps(4, 5);
console.log(intermediateStep(10)); // 19
```
