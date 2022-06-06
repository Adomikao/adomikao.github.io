---
title: grid-row / grid-column
date: 2022-06-06 09:39:16
tags:
---

## Grid-row-start and grid-column-start ..

1. The `grid-row-start` & `grid-row-end` CSS property specifies a grid item's start position  & end position within the grid row by contributing a line, a span, or nothing (automatic) to its grid placement, thereby specifying inline-start edge  and inline-end edge of its grid area.

2. The `grid-column-start` & `grid-column-end` CSS property specifies a grid item's start position and end position within the grid column by contributing a line, a span, or nothing (automatic) to its grid placement. These defines the block-start edge and block-end edge of the grid area.

### Example

{% codepen gOvjzPd result 400 100 Adomikao dark %}


Determines a grid item’s location within the grid by referring to specific grid lines. grid-column-start/grid-row-start is the line where the item begins, and grid-column-end/grid-row-end is the line where the item ends.

### Values:

- `<line>` – can be a number to refer to a numbered grid line, or a name to refer to a named grid line
- `span <number>` – the item will span across the provided number of grid tracks
- `span <name>` – the item will span across until it hits the next line with the provided name
- `auto` – indicates auto-placement, an automatic span, or a default span of one

e.g.
```CSS CSS
.item-a {
  grid-column-start: 2;
  grid-column-end: five;
  grid-row-start: row1-start;
  grid-row-end: 3;
}
```

![](/images/grid-column-row-start-end-01.svg)

```CSS CSS
.item-b {
  grid-column-start: 1;
  grid-column-end: span col4-start;
  grid-row-start: 2;
  grid-row-end: span 2;
}
```
![](/images/grid-column-row-start-end-02.svg)

1. If no grid-column-end/grid-row-end is declared, the item will span 1 track by default.

2. Items can overlap each other. You can use z-index to control their stacking order.



### Syntax

```CSS CSS
/* Keyword value */
grid-column-end: auto;

/* <custom-ident> values */
grid-row-start: somegridarea;

/* span + <integer> + <custom-ident> values */
grid-row-start: span 3;

/* Global values */
grid-row-start: inherit;
grid-row-start: initial;
grid-row-start: unset;
```

## Grid-row and grid-column

1. Typing both `grid-column-start` and `grid-column-end` every time can get tiring. Fortunately, `grid-column` is a shorthand property that can accept both values at once, separated by a slash.
For example, grid-column: 2 / 4; will set the grid item to start on the 2nd vertical grid line and end on the 4th grid line.

2. The grid-row and grid-column properties define which row or column an element will be displayed on. Grid-row is shorthand for  `grid-row-start` + `grid-row-end`, grid-column is shorthand for `grid-column-start` + `grid-column-end`.

```CSS CSS
#water {
grid-row: 1 / span 5;
grid-column: 2 / -1;
}
```


### Example

Here’s an explicit 3 × 3 grid where these properties are used to place grid items onto it in specific places:

{% codepen qBxyYrP result 400 100 Adomikao dark %}

### Values:

- `<start-line> / <end-line>` – each one accepts all the same values as the longhand version, including span

e.g.

```CSS CSS
.item-c {
  grid-column: 3 / span 2;
  grid-row: third-line / 4;
}
```
![](/images/grid-column-row.svg)

If no end line value is declared, the item will span 1 track by default.
