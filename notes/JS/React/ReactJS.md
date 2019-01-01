---
title: ReactJS
tags: [Notebooks/JS]
---

# ReactJS

## What is React?
 - React is a declarative JS library for creating web apps with modular components
    - Declarative means that you describe the intention of your code rather than worrying about the implementation
 - These components, which can be any dynamic element on a page, are rendered and re-rendered automatically, you just have to define how to do so

## JSX
 - A modification for JS that allows you to include html markup in JS code
    - Any statement/variable in your JS can be placed inside the markup using `{}`
 - JSX actually works by creating new react elements like so:
```jsx
return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
```
 - To prevent JS's Automatic Semicolon Insertion (ASI), JSX is typically wrapped in `()`
 - Ex:
```jsx
const myJSXExpression =  (
      <div className="hi">
        {this.state.name}
      </div>
    );
```

## React.Component Superclass
 - Many of your components will extend this superclass
 - Each component takes in props as parameters, which are just properties for html elements, and renders the component accordingly
### Constructing a `React.Component`
 - Must use `super(props)` as the first line in your constructor (required by all subclasses in ES6)
 - Place any state variables in JS object called `this.state`
    
### setState()
 - The `setState()` method should be used by react components to update their state
    - This is because React will re-render components after this function is invoked
 - Ex: 
```jsx
  clickyButton.setState({key1: prop1, key2: prop2, ...});
```

### render()
 - The `render()` method returns a JSX expression that describes how a given component should be represented as html.
 - Ex.
```jsx
render() {
    return (
      <button className="square" onClick={() => alert("Hi")}>
        {this.state.value}
      </button>
    );
  }
```
### Component Design
 - Whenever a child class has to communicate with its parent, it is always best to have the shared data in the parent class.
    - This info is then passed into the child using `props`
    
### Interactive Components
 - When designing components that respond to events (e.g. click events), it's important to use arrow function syntax in your JSX.
   - This allows you to not worry about confusing issues with `this`
   - It's also required because otherwise the templating engine of JSX gets all confused
 - Ex.
```jsx
return (
 <button className="square" onClick={() => alert('click')}>
   {this.props.value}
 </button>
);
```
 - If you didn't include the `() =>`, React would fire an alert every time the component is re-rendered
 - However, **IN [FUNCTION COMPONENTS](#func-components)** you don't need the arrow syntax because you don't need to worry about the value of `this`:
   - Ex.
```jsx
function foo() {...}

return (
  <div
    className="container"
    onClick={foo}
  >
    "Hello, there!"
  </div>
);
```
## Immutable is Better (most of the time)
 - When referring to immutabliity here, we mean that you should create a new copy of an object's state and reassign that state to the object rather than mutating the state directly
### Pros
 - Allows you to create "undo" features by storing the previous object states
 - Helps build **pure components**
     - These were described very hand-wavely, but they allow React to more easily re-render things b/c it can detect changes in state
## Types of Components
### Controlled Component
 - A component that maintains no state (all information is stored in its properties)
 - Function Components <a id="func-components"></a>
   - A type of **Controlled Componenet** that only has a `render()` method.
     - These componenets can be declared using a function instead of a class
   - Ex.
```jsx
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```

## List Keys
 - React has trouble determining when to re-render list items. To see why, check out the following example:
```jsx
<li>Alexa: 7 tasks left</li>
<li>Ben: 5 tasks left</li>
```
vs.
```jsx
<li>Ben: 9 tasks left</li>
<li>Claudia: 8 tasks left</li>
<li>Alexa: 5 tasks left</li>
```
 - Apart from adding an additional `<li>...</li>` element, the second one altered the original order
 - To distinguish items from each other, we use the `key` property
   - The `key` property **cannot** be accessed using `this.props.key` because a component can't ask for its key
 - You'll want to specify a unique key for each element like so:
```jsx
return (
  <li key={user.id_from_db}>
    {user.name + ": " + user.taskNum + " tasks left"}
  </li>
```
- **Note**: keys only need to be unique between componenents & their siblings, not globally unique
### Default keys
 - If you don't give a key, React will use the array index, which is *ill-advised* and also throw an error
   - The warning is silenced if you pass in `key={i}` but isn't recommended due to complications with re-ordering. If your data isn't being reordered though, you're fine to use the index
