---
title: Flexbox Notes
tags: [Notebooks/CSS]
---

# Flexbox Notes
![Flexbox Diagram](https://www.w3.org/TR/css-flexbox-1/images/flex-direction-terms.svg)
## Container Element Styles
### `display: flex;`
 - Creates a flex container
### flex-direction
 - Determines the direction of the major and cross axis, which dictates the direction in which elements are ordered
 - **Values**
    - `row`: orders elements horizontally
    - `row-reverse`: orders elements in reverse order horizontally
    - `column`: orders elements vertically 
    - `column-reverse`: orders elements in reverse order vertically
### `justify-content`
 - Aligns items along the main axis
 - **Values**
    - `center`: places elements in the center of the container
    - `flex-start`: first element at the main-start and all other elements directly next to it
    - `flex-end`: places the last element at the main-end and all other elements directly next to it
    - `space-around`: Puts equal space between all elements and the edges of the container
    - `space-between`: Places the first and last elements at the edge of the container and equally spaces all other elements
### `align-items`
 - Aligns items along the cross axis
 - **Values**
    - `center`: center all elements along the cross axis
    - `flex-start`: Align all elements to the cross-start
    - `flex-end`: Align all elements to the cross-end
    - `stretch`: Have the elements stretch to fill the cross axis
    - `baseline`: Align items to their baselines, which is the line that letters in text elements sit on
### `flex-wrap`
 - Determines how elements should wrap if they fill the size of the container
 - **Values**
    - `nowrap`: smush all of the elements into one row/column
    - `wrap`: have the elements wrap into another row/column if there’s overflow
    - `wrap-reverse`: same as wrap, except you reverse the order of the wrapped rows/columns
## Flex Element Styles
### `flex`
 - Shorthand for describing a flex element
 - **Syntax**
    - `flex: <flex-grow> <flex-shrink> <flex-basis>;`
### `flex-grow`
 - Determines the scale factor of growth when a flex container increases size
 - **Values**
    - *0*: No growth at all
    - *Positive Numbers*: Grow relative to this #
       - i.e., if `.element-1` had `flex-grow: 1;` , and `.element-2` had `flex-grow: 2;`, `.element-2` would grow 2x as fast as `.element-1`
### `flex-shrink`
 - Determines the scale factor of shrinkage when a flex container decreases size
 - **Values**
    - 0: No shrinkage at all
    - Positive Numbers: Shrink relative to this #
       - i.e., if `.element-1` had a `flex-shrink: 1;` and `.element-2` had `flex-shrink: 2`, `.element-2` would shrink 2x as fast as `.element-1`
### `flex-basis`
 - Determines the relative sizes of different flex elements when the container is at its original size
 - **Example**
    - If `.element-1` had `flex-basis: 1;` and `.element-2` had `flex-basis: 2`, `.element-2` would be 2x as large as `.element-1`
 
### `order`
 - Determines the ordering of elements in a flex container (Think just like z-index).
 - **Values**
    - *Negative Numbers*: Get positioned before the default-positioned elements
    - *0*: Default. Ordered according to position in the DOM
    - *Positive Numbers*: Get positioned after the default-position elements
### `align-self`
 - Specifies the positioning of an individual element on the cross-axis
 - **Values**
    - Same as `align-items`
