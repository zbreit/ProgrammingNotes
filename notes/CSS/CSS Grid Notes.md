---
title: CSS Grid Notes
tags: [Notebooks/Learning Code/CSS]
---

# CSS Grid Notes
## Container Element Styles
### `display: grid;`
 - Creates a grid container
### `grid-template-rows` (& `grid-template-columns`)
 - Defines the size of a variable number of rows
   - Setting this property auto-determines the # of columns based on the # of items in the grid
 - Units
   - Px, ems, and other units are still valid, but there are a few with some special grid features
     - Fr: A fraction of the available space
     - %: A fraction of the parent container’s width
     - Auto: Automatically fills to the size of the data
 - Ex.
   - Create a 50px and 150px row
     - `grid-template-row: 50px 150px;`
   - Create an auto, 2fr, and 1fr column
     - `grid-template-row: auto 2fr 1fr;`
 #### `repeat(n, measurementList)`:
  - Repeat a measurement `n` times
     - Ex:
        - Create 100, `10px` rows
           - `grid-template-row: repeat(100, 10px);`
   - More advanced repeat functionality:
      - This:
         - `grid-template-row: repeat(2, 1fr 50px) 20px;`
      - Is the same as this:
         - `grid-template-row: 1fr 50px 1fr 50px 20px;`
#### `auto-fill`
 - If the grid size ever exceeds the total size of the items, continue introducing additional rows/cols. If the grid size is less than the total size of the items, additional rows/cols will be introduced to house them.
 - Ex:
    - Create a grid with a variable column number. As the container grows, the grid will add 60px columns and stretch existing columns to fit additional columns
       - `grid-template-columns: repeat(auto-fill, 10px 1fr);`
#### `auto-fit`
 - If the grid size ever exceeds the total size of the items, expand the size of the existing cells. If the grid size is less than the total size of the items, additional rows/cols will be introduced to house them
 - Ex.
    - Create a grid with a variable column number. As the container grows, the grid will add `60px` columns and stretch them until it can insert another one
       - `grid-template-columns: repeat(auto-fit, 10px 1fr);`
#### `minmax(min, max)`:
 - Create a variably-sized dimension with the specified `min` and `max` size
 - Ex:
    - Create a `20px` row and a row that can be between `30px` and `50px`
       - `grid-template-row: 20px minmax(30px, 50px);`
### `grid-gap`
 - Specifies the size of the gaps between the rows and cols (shorthand)
 - Ex:
    - Create `10px` gaps between rows and `20px` gaps between columns
       - `grid-gap: 10px 20px;`
    - Create `10px` gaps between the rows and columns
       - `grid-gap: 10px;`
 - Longhand
    - `grid-row-gap` (& `grid-column-gap`)
      - Creates a gap between the row
      - Ex.
         - Create a `10px` gap between each row
             - `grid-row-gap: 10;`
### `justify-items`
 - Determines the horizontal location of all items in their cells
 - Values: Same as `justify-self` (see below)
### `align-items`
 - Determines the vertical location of all items in their cells
 - Values: Same as justify-self (see below)
### `grid-template-areas`
 - Group different cells into areas with custom names
 - Ex: (for 3x3 grids)
Create a layout for a 3x3 grid
```css
grid-template-areas: 
“header header header”
“advert content content”
“footer footer footer”
```
<!-- Break up 2 code-blocks-->
Create a layout with an empty cell in the middle
```css
grid-template-areas: 
“a a a”
“b . b”
“c c c”;
```
## Item Styles
### `grid-row` (& `grid-column`)
![Grid Lines Diagram](https://cdn-images-1.medium.com/max/2000/1*H51JnBAnLJiZmlzRvhInlg.png)
 - Specifies the start and end row that an item occupies
    - the rows are numbered starting from 1 and can be seen as the gray lines in the above image
 - Ex:
    - Make an item span from the first line to the third, occupying the first two rows
       - `grid-row: 1 / 3;`
### `justify-self`
 - Determines the horizontal location of an item in its cell
 - *Values*
    - **Stretch**: fill the width of the cell
    - **Start**: Stay on the left of the cell
    - **End**: Stay on the right of the cell
    - **Center**: Stay in the center of the cell
### `align-self`
 - Determines the vertical location of an item in its cell
 - Values: same as `justify-self`
### `grid-area`
 - Places an item in a specified area in a grid
 - Ex:
    - Place an item in the predefined `footer` area
       - `grid-area: footer;`
    - Place an item between the 1st and 3rd horizontal lines and the 2nd and 4th vertical lines (top-right quadrant)
       - `grid-area: 1 / 2 / 3 / 4;`
