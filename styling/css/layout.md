## Layout

[Codepen](https://codepen.io/christinatruong/pen/OepEEP)

[Codepen Collection](https://codepen.io/collection/AQkgKB?grid_type=list)

/home/tim/Learning/Lynda/Styling/css-layouts

### css positioning

does not control entire page flow. instead, use to fine tune certain pieces

- normal flow: default layout method, same order as html
- element floating
- absolute positioning

position

[Codepen](https://codepen.io/christinatruong/pen/zXLemj)

- **values:** static | relative | absolute | inherit | fixed / sticky

- static: not positioned
- relative: relative to current position
- absolute: relative to the containing element
- fixed: relative to the viewport
- sticky: relative to containing element & viewport

### css displays

floats

- **values:** left | right | none | inherit
- requires a _clear_ after the float(s) to resume normal flow

  [Codepen](https://codepen.io/christinatruong/pen/ROQdZJ)

  [Codepen](https://codepen.io/christinatruong/pen/dLjeVV)

### flexbox

- use for space distibution for items along same axis

https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox

[Codepen](https://codepen.io/christinatruong/pen/qwgjJo)

The **Flexible Box Layout** (flexbox) provides many ways for aligning content, ordering items, and implementing flexible sizing

one-dimension way to arrange elements - items are laid out in either single column or single row

define flex on the parent container
all child elements will be flex items

- flex container (if `inline-flex`, sets width to contents)
- flex items

use `flex-direction` property to determine ordering of content

use `flex-wrap` property to wrap items to new row

can control:

- alignment
- direction
- order
- size

aligning items in a flex container

https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox#Horizontal_and_vertical_alignment

- **justify-content**: aligns items on the main axis - [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content)
- **align-items**: aligns items on the cross axis - [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items)
- **flex-direction**: sets how flex items are placed in the flex container - [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-direction)
- **flex-wrap**: sets whether flex items are forced onto one line or can wrap onto multiple lines - [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-wrap)

```css
.box {
  /* place item in center of container*/
  display: flex;
  align-items: center;
  justify-content: center;
}
```

### css grid

- use to control items that are in rows & columns

[Codepen](https://codepen.io/christinatruong/pen/YbRWzy)

https://hacks.mozilla.org/2017/10/an-introduction-to-css-grid-layout-part-1/

two-dimension way to arrange elements

**explicit grid**

use: `grid-template-columns` & `grid-template-rows`

```css
/*creates a grid with 3 columns & 2 rows*/
.grid-container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px;
}
```

can use `fr` as unit within the grid-template values, represents the fraction of available space in the grid container.

```css
grid-template-columns: 1fr 2fr 1fr;
/*use repeat*/
grid-template-columns: 50px repeat(2, 1fr);
```

add **gutters** (space between grids) with `gap`

```css
gap: 10px;
/* set gutter for rows then columns*/
gap: 10px 20px;
```

**implicit grid**

use implicit grid when working with dynamic / unknown data

`grid-auto-rows` & `grid-auto-columns`

**minmax**

Defines a size range greater than or equal to min and less than or equal to max.

```css
grid-template-columns: minmax(20px, auto) 1fr 1fr;
```

**grid-template-areas**

Specifies named grid areas, establishing the cells in the grid and assigning them names.

```css
/* set the template */
grid-template-areas:
  "a a a"
  "b c c"
  "b c c";
/* place element in an area */
.header {
  grid-area: a;
}
.side-nav {
  grid-area: b;
}
}
```
