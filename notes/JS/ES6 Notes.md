---
title: ES6 Notes
tags: [Notebooks/JS]
---

# ES6 Notes
Notes from the ES6 tutorial on [FreeCodeCamp](https://www.freecodecamp.org/)
## Strict Mode
 - If you put `'use strict';` at the top of your file, JS will enter a more strict mode that will catch common errors during linting.
    - Ex.
```js
"use strict";
x = 3.14; // throws an error because x is not declared
```

## Let vs. Var
 - **Naming Conflicts**
    - Using `var`, you can override other variables with the same name:
    - `let` will throw an error if there's a naming conflict
```js
var dave = "10";
var dave = null; // dave is now null!!
let ben = "hi";
let ben = 9;     // Throws an error
```
 - **Scope**
    - `var` is either function scope or global scope
    - `let` is block scope 
```js
for(var imGlobal = 0; imGlobal < 10; imGlobal++) {
  console.log("Hello, World!");
}
console.log(imGlobal); // 10

for(let imLocal = 0; imLocal < 10; imLocal++) {
  console.log("Hello, World!");
}
console.log(imLocal); // Throw an error
```
## Const
 - Variables declared with `const` can't be reassigned (i.e., they are read-only)
    - This does not mean they're immutable (e.g., you can change a value in an array index or object key)
 - Variables declared using `const` are named using all caps w/ underscores
 - It is standard to name all variables with `const` and use `let` for everything that needs to be reassigned a value
```js
const MY_NAME = "Zach";
MY_NAME = "Jeff"; // INVALID

const MY_ARR = [1, 2, 3];
MY_ARR[0] = 20; // valid
```
## Immutable Objects
 - To make an object immutable, you can call `Object.freeze()`
    - This will prevent anything from deleting, altering, or adding any properties
```js
let obj = {
  name:"FreeCodeCamp",
  review:"Awesome"
};
Object.freeze(obj);
obj.review = "bad";   //will be ignored. Mutation not allowed
obj.newProp = "Test"; // will be ignored. Mutation not allowed
```
## Arrow Functions
 - Shorthand method for writing anonymous functions
    - If there is just a return value, you can omit the word `return`
    - If there is only 1 parameter, you can omit the enclosing `()`
```js
const oldWay = function() {
  ...
}

const newWay = () => {
  ...
}

const square = num => num*num;
```

## Array Methods
 - `.map(func)`
    - Returns a new array that replaces every value in the original array with `func(val)`
 - `arr.filter(testFunc)`
    - Returns a new array that only includes values from the original array such that `testFunc(val) === true`
## Default Parameters
 - All parameters with default values must go after parameters without default args
 - If you pass in the value of undefined for the parameter, the default value will still be used
 - Specify default parameters like so:
```js
function sayHi(name, greeting = "Hello, there ") {
  console.log(greeting + name);
}
```
## Rest Operator
 - Represented as `...`
 - Provies an easy way to accept a variable number of arguments
```js
function sum(...args) {
  return args.reduce((currentSum, currentVal) => currentSum + currentVal);
}
```
## Spread Operator
 - Represented as `...`
 - Expands/unpacks an array into its values if it passed in as an argument
    - This functionality replaces the `.apply()` method for functions, which supplies a `this` value and a list of arguments
```js
const arr = [1, 5, 10];

// Use apply with the array as the args list and no value for this
const oldWayMax = Math.max.apply(null, arr);

// Use the spread operator to avoid using apply
const newWayMax = Math.max(...arr);
```
 - You can also use the spread operator to make a shallow copy of an array
```js
const arrCopy = [...arr];
```
## Destructuring Assignment
 - A new syntax for unpacking objects into a comma separrated list (a la Matlab)
```js
const obj = {
  x: 10,
  y: 20,
  z: 30,
  innerObj: {
    name: "Zach",
    age: 19
  },
}


const { x, y, z } = obj; // x = 10, y = 20, z = 30

// Create variables w/ names different from the properties
const { x : a, z : c } = obj; // a = 10, c = 30

// Nested Destructuring
const { innerObj : { name : myName, age : myAge } } = obj; // myName = "Zach", myAge = 19;
```
 - You can also use destructuring to unpack an array
    - To skip over certain values, we can use extra commas
```js
const arr = [1,3,5,7,9];

const [a, b, c, d, e] = arr; // a = 1, b = 3, c = 5, d = 7, e = 9
const [a, b,,, e] = arr;     // a = 1, b = 3, e = 9
```
 - Swap the value of 2 variables:
```js
let a = 1, b = 2;
[b, a] = [a, b];
```
- Combining the rest operator with destructuring assignment
```js
const [a, b, ...arr] = [1,3,5,7,9]; // a = 1, b = 3, arr = [5,7,9]
```
- Using destructuring to pass in object properties as function parameters
```js
// Take in an object and extract its name, age, nationality, and location
const profileUpdate = ({ name, age, nationality, location }) => {
  ...
}
```
## Template Literals
 - Essentially, string formatting for JS
    - Strings that use template literals are wrapped with ` `` ` (backtick) characters
       - This means that any return characters in the middle of the string will print as `\n` characters
    - Dynamic elements are added in using `${value}` rather than using concatenation
```js
const person = {
  name: "Zach",
  age: 19,
};
const numNeighbors = 2;

const myTemplatedString = `Hi ${player.name}, how does it feel to be
${player.age}? Must be lonely with only ${numNeighbors} neighbors.`;

console.log(myTemplatedString); // prints
// Hi Zach, how does it feel to be
// 19? Must be lonely with only 2 neighbors.
```
## Simpler Object Literal Declarations
 - When generating object literals using functions, you will often want to use the parameters as both properties and values in the returned object:
```js
function getObj(x, y) {
  return {
    x: x,
    y: y,
  };
}
```
 - ES6 introduces syntactic sugar to streamline this process and avoid the redundant use of the parameter names
```js
function getObj(x, y) {
  return {x, y};
}

const obj = getObj(3, 4); // obj = {x: 3, y: 4}
```
## Defining Object Methods Concisely
 - Instead of this:
```js
const obj = {
  name: "Zach"
  foo: function() {
    ...
  }
};
```
 - You can do this:
 ```js
const obj = {
  name: "Zach"
  foo() {
    ...
  }
};
```
## Class Syntax
- A `class` in JS is simply syntactic sugar for a function that creates objects 
### Constructors
- You can use a `class` to mimic old constructor functions in ES5, which look like this:
```js
var Person = function(name, age) {
  this.name = name;
  this.age = age;
}

var Jeff = new Person("Jeff", 27);
```
 - In ES6, you use the `class` declaration to do define the same type of constructor function:
```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

const Jeff = new Person("Jeff", 27);
```
### Getters and Setters
 - To enable data encapsulation, getters and setters can be used as a public API for your class
    - Note that private class variables are not yet implemented in JS, though will be able to do so in a future spec using the `#` symbol
 - `Getters` allow you have a function called when an object property is looked up
```js
const obj = {
  myList: [1, 3, 5],
  get latest() {
    if(myList.length != 0) {
      return undefined;
    }
    
    return this.myList[this.myList.length - 1];
  }
}

console.log(obj.latest); // 5
```
- `Setters` allow you have a function called when an object property is set
```js
const obj = {
  myList: [],
  set current(val) {
    myList.push(val);
  }
}

obj.current = 'hi'; // obj.myList = ['hi'];
```
## Imports
 - Previously, to obtain external bits of JS, you had to use `require()` statements, which would include the **entirety** of a JS file
 - Using `import` statements, ES6 allows you to select **specific** functions or variables tuat we'd like to import
```js
import { sum, countItems } from "./math_array_functions"
countItems([1, 4, 8]);
```
 - **Note**: it is best practice to include space between `{}` and the function/variable names for readibility
 - **Note**: `import` statements don't work in browser JS, but do work in things like node, electron, and React
 - **Note**: the `./` is included because node looks in the `node_modules` folder for dependencies by default
### Importing Everything
 - Use the `*` to import all exports from a file
```js
import * as personalLibrary from './myLib';
```
### Importing Default Exports
 - Use the following syntax to import a default function
    - For the sake of the scenario, assume that `makeNoise()` is the default export from `'my_lib'`
```js
import makeNoise from 'my_lib';
```
## Exports
 - In order to for functions/variables to be available for importing, they must first be exported from the original file
### Named Exports
Method 1
```js
const getFirstChar = (string) => {
  return string.charAt(0);
}
export { getFirstChar };  //How to export functions.
export const foo = "bar"; //How to export variables.
```

Method 2
```js
const getLastChar = (string) => {
  return string.charAt(string.length - 1);
}
const goo = "bar";
export { getLastChar, goo };  // How to export everything at once
```
### Default Exports
 - In the case that you only need to export one thing from a file, or that you need a fallback export to represent a file, use the `default` keyword:
```js
export default function add(x,y) {
  return x + y;
}
```
or
```js
export default foo = "someCoolVal";
```
