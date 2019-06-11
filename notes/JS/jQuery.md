---
title: jQuery
tags: [Notebooks/JS]
---

# jQuery
Notes from the jQuery tutorial on [FreeCodeCamp](https://www.freecodecamp.org/)
## jQuery Function
 - `$(selector)`
    - Return an object in the DOM that corresponds to the given css `selector`
## Cool Selector Modifiers
 - `:nth-child(n)`
    - Select the nth object that applies to some selector
 - `:odd`
    - Target every other element, starting with the 2nd
       - This is because jQuery uses 0-based indexing
 - `:even`
    - Target every other element, starting with the 1st
       - This is because jQuery uses 0-based indexing
## Methods of `$` Objects
### Classes
 - `.addClass(class)`
    - Add `class` to the class list of the obj
 - `.removeClass(class)`
    - Remove `class` from the class list of the obj
### Styling
 - `.css(propName, value)`
    - Add the css rule `propName: value;` to the obj
### Editing Content
 - `.html(innerHtml)`
    - Set the inner HTML of the obj to `innerHTML` (can include tags)
 - `.text(text)`
    - Edit the text of the obj (All html tags in `text` are escaped)
 - `.prop(propName, value)`
    - Set the `propName` property in the html to `value` (`propName=value`) 
### Generating New Tags
 - `.clone()`
    - Get a copy of `obj`
 - `.appendTo(selector)`
    - Add the current obj to the end of the html element corresponding to the `selector`
### Traversing the DOM
 - `.parent()`
    - Return the parent of the given element
 - `.children()`
    - Return a list of the current object's children
