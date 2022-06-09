---
title: Properties for the Grid container III
date: 2022-06-06 21:46:10
tags:
---

## justify-content

Sometimes the total size of your grid might be less than the size of its grid container. This could happen if all of your grid items are sized with non-flexible units like px. In this case you can set the alignment of the grid within the grid container. This property aligns the grid along the inline (row) axis (as opposed to align-content which aligns the grid along the block (column) axis).

### Values:

- `start` – aligns the grid to be flush with the start edge of the grid container
- `end` – aligns the grid to be flush with the end edge of the grid container
- `center` – aligns the grid in the center of the grid container
- `stretch` – resizes the grid items to allow the grid to fill the full width of the grid container
- `space-around` – places an even amount of space between each grid item, with half-sized spaces on the far ends
- `space-between` – places an even amount of space between each grid item, with no space at the far ends
- `space-evenly` – places an even amount of space between each grid item, including the far ends

```CSS CSS
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;    
}
```

e.g.

```CSS CSS
.container {
  justify-content: start;
}
```
![](/images/justify-content-start.svg)

```CSS CSS
.container {
  justify-content: end;
}
```
![](/images/justify-content-end.svg)

```CSS CSS
.container {
  justify-content: center;
}
```
![](/images/justify-content-center.svg)

```CSS CSS
.container {
  justify-content: stretch;
}
```
![](/images/justify-content-stretch.svg)

```CSS CSS
.container {
  justify-content: space-around;
}
```
![](/images/justify-content-space-around.svg)

```CSS CSS
.container {
  justify-content: space-between;
}
```
![](/images/justify-content-space-between.svg)

```CSS CSS
.container {
  justify-content: space-evenly;
}
```
![](/images/justify-content-space-evenly.svg)


## align-content

Sometimes the total size of your grid might be less than the size of its grid container. This could happen if all of your grid items are sized with non-flexible units like px. In this case you can set the alignment of the grid within the grid container. This property aligns the grid along the block (column) axis (as opposed to justify-content which aligns the grid along the inline (row) axis).

```CSS CSS
.container {
  align-content: start | end | center | stretch | space-around | space-between | space-evenly;    
}
```

## place-content

`place-content` sets both the align-content and justify-content properties in a single declaration.

### Values:

- `<align-content> / <justify-content>` – The first value sets align-content, the second value justify-content. If the second value is omitted, the first value is assigned to both properties.

All major browsers except Edge support the place-content shorthand property.


## grid-auto-columns and grid-auto-rows

Specifies the size of any auto-generated grid tracks (aka implicit grid tracks). Implicit tracks get created when there are more grid items than cells in the grid or when a grid item is placed outside of the explicit grid.

### Values:

- `<track-size>` – can be a length, a percentage, or a fraction of the free space in the grid (using the fr unit)

To illustrate how implicit grid tracks get created, think about this:

```CSS CSS
.container {
  grid-template-columns: 60px 60px;
  grid-template-rows: 90px 90px;
}
```

![](/images/grid-auto-columns-rows-01.svg)

This creates a 2 x 2 grid.

But now imagine you use grid-column and grid-row to position your grid items like this:

```CSS CSS
.item-a {
  grid-column: 1 / 2;
  grid-row: 2 / 3;
}
.item-b {
  grid-column: 5 / 6;
  grid-row: 2 / 3;
}
```
![](/images/grid-auto-columns-rows-02.svg)

We told .item-b to start on column line 5 and end at column line 6, but we never defined a column line 5 or 6. Because we referenced lines that don’t exist, implicit tracks with widths of 0 are created to fill in the gaps. We can use grid-auto-columns and grid-auto-rows to specify the widths of these implicit tracks:

```CSS CSS
.container {
  grid-auto-columns: 60px;
}
```

![](/images/grid-auto-columns-rows-03.svg)

## grid-auto-flow

### Values:

- `row` – tells the auto-placement algorithm to fill in each row in turn, adding new rows as necessary (default)
- `column` – tells the auto-placement algorithm to fill in each column in turn, adding new columns as necessary
- `dense` – tells the auto-placement algorithm to attempt to fill in holes earlier in the grid if smaller items come up later

```CSS CSS
.container {
  grid-auto-flow: row | column | row dense | column dense;
}
```

Note that dense only changes the visual order of your items and might cause them to appear out of order, which is bad for accessibility.


e.g.

```HTML HTML
<section class="container">
  <div class="item-a">item-a</div>
  <div class="item-b">item-b</div>
  <div class="item-c">item-c</div>
  <div class="item-d">item-d</div>
  <div class="item-e">item-e</div>
</section>
```

You define a grid with five columns and two rows, and set grid-auto-flow to row (which is also the default):

```CSS CSS
.container {
  display: grid;
  grid-template-columns: 60px 60px 60px 60px 60px;
  grid-template-rows: 30px 30px;
  grid-auto-flow: row;
}
```

When placing the items on the grid, you only specify spots for two of them:

```CSS CSS
.item-a {
  grid-column: 1;
  grid-row: 1 / 3;
}
.item-e {
  grid-column: 5;
  grid-row: 1 / 3;
}
```

Because we set grid-auto-flow to row, our grid will look like this. Notice how the three items we didn’t place (item-b, item-c and item-d) flow across the available rows:

![](/images/grid-auto-flow-01.svg)

If we instead set grid-auto-flow to column, item-b, item-c and item-d flow down the columns:

```CSS CSS
.container {
  display: grid;
  grid-template-columns: 60px 60px 60px 60px 60px;
  grid-template-rows: 30px 30px;
  grid-auto-flow: column;
}
```

![](/images/grid-auto-flow-02.svg)

