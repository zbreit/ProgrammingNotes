---
title: Object-Oriented Programming
tags: [Notebooks/JS]
---

# Object-Oriented Programming
Notes from the JS OOP tutorial on [FreeCodeCamp](https://www.freecodecamp.org/)
## Constructor Function
- Constructor functions create new object instances
   - They act as a blueprint for making a particular type of object
- To invoke a constructor function, use the `new` keyword in front of it
   - This allows JS to ensure that the `this` reference points to the object being created
```js
// Typical constructor function
function Bird(name, color) {
  this.name = name;
  this.color = color;
  this.numFeathers = 4;
}

let myPetBird = new Bird("Josiah", "blue");
myPetBird.numFeathers = 20;
```
## instanceof
 - To check if a variable was created using an object constructor, use the `instanceof` keyword
```js
function Bird(name, color, numFeathers) {...}
let actualBird = new Bird('a', 'b', 3);
let fakeBird = {name: 'c', color: 'r', numFeathers: 2};

actualBird instanceof Bird; // true
fakeBird instanceof Bird;   // false
```
 - You can alternatively use an objects `.constructor` property, although that can be overriden
    - The `.constructor` property is a reference to the object's constructor function
```js
console.log(actualBird.constructor === Bird); // true
```
## Prototype
 - Every constructor has a `prototype` object attached to it that is shared between all instances of that constructor function
    - This is useful if there is a piece of information shared between all objects made by that constructor
       - Ex. A `Bird` object always has a `numWings` value of `2`. So we can assign that to the prototype instead of storing a separate value in every `Bird`
```js
function Bird(name) {...}
Bird.prototype = {
  numWings: 2,
  numLegs: 2,
  eat() {
    console.log("bawk bawk bawk");
  }
}

let myPetBird = new Bird('hi');
console.log(myPetBird.numWings); // 2
```
- ***NOTE:*** When you define a `prototype` as an object (instead of using dot notation to assign each property of `prototype`), *you make the constructor property `undefined`*.
   - To fix this, simply add a `constructor` property in the prototype definition
```js
Bird.prototype = {
  constructor: Bird, // This is super-important
  numWings: 2,
  numLegs: 2,
  eat() {
    console.log("bawk bawk bawk");
  }
}
```
## Types of Properties
 - Thus, objects defined using constructors have two types of properties
    - `prototype`: properties that are shared among every instance
    - `own`: properties that belong to each instance
       - This explains the naming for the `.hasOwnProperty()` method, which will only return true for `own` properties
## IsPrototypeOf
 - To see if a prototype is inherited by a given object, use the `.isPrototypeOf()` method
```js
let jeff = new Bird('hi');
Bird.prototype.isPrototypeOf(jeff); // true
```
## Inheritance
 - To create supertypes, you start by defining a parent with all of the desired properties and functions in its prototype
 - Then, you use `Object.create(obj)` to set the prototype of your subclass to the prototype of the superclass.
    - This function creates a new object who's prototype is `obj`
    - This will allow us to access all of the important stuff from the parent
       - **Note**: We also inherit the constructor property from the Animal prototype, which we'll have to override
```js
// Animal is a superclass
function Animal(){}
Animal.prototype = {
  constructor: Animal,
  eat() {
    console.log('nom nom nom');
  }
}

// Bird is a subclass
function Bird() {
  this.name = name;
}

// Extend the functionality from the Animal superclass
Bird.prototype = Object.create(Animal.prototype);

// Reset the Bird constructor property, which was originally set to Animal
Bird.prototype.constructor = Bird;

// Define a new function in the Bird subclass
Bird.prototype.fly = () => console.log("I'm flying now!!!");
```

### Overriding Functions
 - If there was an inherited function called `eat()`, it would be easy to override it like so
```js
Bird.prototype.eat = () => console.log("peck peck peck");
```
## Using Mixins
 - Sometimes, you have objects with similar methods that are logically unrelated
    - Ex. `Bird` and `Airplane` both have a `fly()` method
 - In that case, you should use mixins to define a series of methods as properties to a supplied object
```js
function flyMixin(obj) {
  obj.fly = () => console.log("Flying WooHoo");
}

let bird = {
  name: "Donald",
  numLegs: 2
};

let plane = {
  model: "777",
  numPassengers: 524
};

flyMixin(bird);
flyMixin(plane);
```
## Private Variables
 - To create private properties, you have to define variables that are local to the constructor
    - The public properties and methods defined in the constructor have access to these local variables, but no one else does
```js
function Car() {
  let superSecretCarId = 1234; // Private property
  
  this.unlock = (passCode) => {
    console.log(passCode === superSecretCarID ? "In" : "Locked Out");
  };
}
```
## Immediately Invoked Function Expression (IIFE)
 - This expression allows a function to be invoked as soon as it's declared
    - The function is anonymous
 - You can assign an IIFE to a variable to package elements into a module (without polluting the global namespace)
```js
// Old IIFE
let myMixinModule = (function() {
  return {
    flyMixin(obj) {
      obj.fly = () => console.log("I'm Flying");
    },
    glideMixin(obj) {
      obj.glide = () => console.log("I'm Gliding");
    }
  };
})();

myMixinModule.flyMixin(duck);
duck.fly();

// ES6 IIFE
((someInput) => console.log(someInput))(someInput);
```
