---
title: Basic JS
tags: [Notebooks/JS]
---

# Basic JS
Notes from the basic JS tutorial on [FreeCodeCamp](https://www.freecodecamp.org/)
## Data Types
 - Javascript has 7 data types:
    - `number`
    - `string`
    - `boolean`
    - `symbol`
    - `undefined`
    - `null`
    - `object`
## Declaring variables
 - Unitialized variables start out as `undefined`
 - `undefined` variables have the following behavior:
```js
var y;    // Has a value of undefined
9 + y;    // 9 + NaN = NaN
"hi" + y; // "hiundefined"
```
## Assorted Tidbits
 - The `String` data type is immutable
    - You can't assign characters to individual indices
```js
var z = "jello";
z[0] = "h"; // z is still "jello"
```
## Arrays
 - Arrays can store mixed types:
```js
var arr = [23, "hi", undefined, null];
```
### Array Methods
 - `.push(a, b, c, ...)`
    - Append elements to the end of the array
 - `.pop()`
    - Remove the last element of the array and return it
 - `.shift()`
    - Remove the first element of the array and return it
 - `.unshift(a, b, c, ...)`
    - Add elements to the front of the array
 - `.splice(start, numElements)`
    - Remove `numElements` from the array starting at index `start`
 - `.splice(start, numElements, a, b, c, ...)`
    - Replace `numElements` in the array with new values. Start replacing at index `start`
 - `.slice(start = 0, end = arr.length - 1)`
    - Extract elements from the array, starting at `start` and ending 1 element before `end`
       - The original array is not changed
## Functions
 - Basic method to define functions:
```js
  function foo(x, y) {
    ...
  }
```
 - The default return value for a function is `undefined`
```js
  function foo() {
    ...
  }
  
  console.log(foo); // undefined
```
## Scope
 - Variables created without the `var` keyword are globally-scoped
```js
var imGlobal = 10;

function foo() {
  imGlobalToo = 40;
  var imLocal = 80;
}
```
 - When there's a naming collision, local scope variables take precedence
```js
var x = 10;

function foo() {
  var x = 20;
  console.log(x); // 20
}
```
## Objects
 - Property names can initialized as strings or numbers, but they will always be typecast as strings
    - For single-word string properties, you can omit the quotations
```js
var x = {
  name: "Zach",
  8: undefined,
  "home address": "123 Sesame St.",
  20: null,
}
```
 - You can use dot notation (as in `obj.property`) if the property name is of type string and has no spaces
```js
x["8"] = 72; 
x[8] = 92;
x.name = 28;
x["home address"] = "hi";
```
 - Use the `delete` keyword to remove object properties
 ```js
 delete x.name;
 ```
## Object Methods
 - `.hasOwnProperty(propName)`
    - Returns `true` if an object has the property `propName`
## Miscellaneous Functions
 - `Math.random()`
    - Generate a random number on the interval (0, 1)
 - `Math.floor()`
    - Truncate a given number
 - `parseInt()`
    - Given a string representing a number, return the actual number
       - Non-numbers are assigned the value of `NaN`
    - The function optionally takes a second parameter (the `radix`) to specify the base of the string (e.g., `2` corresponds to binary, `16` to hexidecimal, `10` to decimal, etc.)
