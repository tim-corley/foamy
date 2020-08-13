## Layout

[Codepen](https://codepen.io/christinatruong/pen/OepEEP)

### css positioning

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

floats

- **values:** left | right | none | inherit
- requires a _clear_ after the float(s) to resume normal flow

  [Codepen](https://codepen.io/christinatruong/pen/ROQdZJ)

  [Codepen](https://codepen.io/christinatruong/pen/dLjeVV)

### flexbox

https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox

[Codepen](https://codepen.io/christinatruong/pen/qwgjJo)

one-dimension way to arrange elements

define flex on the parent container
all child elements will be flex items

- flex container (if `inline-flex`, sets width to contents)
- flex items

us `flex-direction` to determine ordering of content

can control:

- alignment
- direction
- order
- size

aligning items in a flex container

https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox#Horizontal_and_vertical_alignment
https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content
https://developer.mozilla.org/en-US/docs/Web/CSS/align-items

- **justify-content**: aligns items on the main axis
- **align-items**: aligns items on the cross axis

```css
.box {
  /* place item in center of container*/
  display: flex;
  align-items: center;
  justify-content: center;
}
```

### css grid

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
