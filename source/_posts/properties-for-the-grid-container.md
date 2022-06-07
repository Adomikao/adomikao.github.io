---
title: Properties for the Grid container
date: 2022-06-06 17:35:42
tags:
---

## display

Defines the element as a grid container and establishes a new grid formatting context for its contents.

### Values:

- `grid` – generates a block-level grid
- `inline-grid` – generates an inline-level grid

```CSS CSS
.container {
  display: grid | inline-grid;
}
```

## grid-template-columns and grid-template-rows

Defines the columns and rows of the grid with a space-separated list of values. The values represent the track size, and the space between them represents the grid line.

### Values:

- `<track-size>` – can be a length, a percentage, or a fraction of the free space in the grid (using the `fr` unit)
- `<line-name>` – an arbitrary name of your choosing

```CSS CSS
.container {
  grid-template-columns: ...  ...;
  /* e.g. 
      1fr 1fr
      minmax(10px, 1fr) 3fr
      repeat(5, 1fr)
      50px auto 100px 1fr
  */
  grid-template-rows: ... ...;
  /* e.g. 
      min-content 1fr min-content
      100px 1fr max-content
  */
}
```

Grid lines are automatically assigned positive numbers from these assignments (-1 being an alternate for the very last row).

![](/images/template-columns-rows-01.svg)

But you can choose to explicitly name the lines. Note the bracket syntax for the line names:

```CSS CSS
.container {
  grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end];
  grid-template-rows: [row1-start] 25% [row1-end] 100px [third-line] auto [last-line];
}
```

![](/images/template-columns-rows-02.svg)

Note that a line can have more than one name. For example, here the second line will have two names: row1-end and row2-start:

``` CSS CSS
.container {
  grid-template-rows: [row1-start] 25% [row1-end row2-start] 25% [row2-end];
}
```

If your definition contains repeating parts, you can use the repeat() notation to streamline things:

```CSS CSS
.container {
  grid-template-columns: repeat(3, 20px [col-start]);
}
```
Which is equivalent to this:

```CSS CSS
.container {
  grid-template-columns: 20px [col-start] 20px [col-start] 20px [col-start];
}
```

If multiple lines share the same name, they can be referenced by their line name and count.

```CSS CSS
.item {
  grid-column-start: col-start 2;
}
```

The `fr` unit allows you to set the size of a track as a fraction of the free space of the grid container. For example, this will set each item to one third the width of the grid container:

```CSS CSS
.container {
  grid-template-columns: 1fr 1fr 1fr;
}
```

The free space is calculated after any non-flexible items. In this example the total amount of free space available to the fr units doesn’t include the 50px:

```CSS CSS 
.container {
  grid-template-columns: 1fr 50px 1fr 1fr;
}
```

## grid-template-areas

### Values:

- `<grid-area-name>` – the name of a grid area specified with `grid-area`
- `.` – a period signifies an empty grid cell
- `none` – no grid areas are defined

```CSS CSS
.container {
  grid-template-areas: 
    "<grid-area-name> | . | none | ..."
    "...";
}
```

e.g.

```CSS CSS
.item-a {
  grid-area: header;
}
.item-b {
  grid-area: main;
}
.item-c {
  grid-area: sidebar;
}
.item-d {
  grid-area: footer;
}

.container {
  display: grid;
  grid-template-columns: 50px 50px 50px 50px;
  grid-template-rows: auto;
  grid-template-areas: 
    "header header header header"
    "main main . sidebar"
    "footer footer footer footer";
}
```

That’ll create a grid that’s four columns wide by three rows tall. The entire top row will be composed of the **header** area. The middle row will be composed of two **main** areas, one empty cell, and one **sidebar** area. The last row is all **footer**.

![](/images/dddgrid-template-areas.svg)

Each row in your declaration needs to have the same number of cells.

You can use any number of adjacent periods to declare a single empty cell. As long as the periods have no spaces between them they represent a single cell.

Notice that you’re not naming lines with this syntax, just areas. When you use this syntax the lines on either end of the areas are actually getting named automatically. If the name of your grid area is **foo**, the name of the area’s starting row line and starting column line will be **foo-start**, and the name of its last row line and last column line will be **foo-end**. This means that some lines might have multiple names, such as the far left line in the above example, which will have three names: `header-start,` `main-start`, and `footer-start`.

## grid-template

A shorthand for setting `grid-template-rows`, `grid-template-columns`, and `grid-template-areas` in a single declaration.

Values:

- `none` – sets all three properties to their initial values
- `<grid-template-rows> / <grid-template-columns>` – sets grid-template-columns and grid-template-rows to the specified values, respectively, and sets grid-template-areas to none

It also accepts a more complex but quite handy syntax for specifying all three. Here’s an example:

```CSS CSS
.container {
  grid-template:
    [row1-start] "header header header" 25px [row1-end]
    [row2-start] "footer footer footer" 25px [row2-end]
    / auto 50px auto;
}
```

That’s equivalent to this:

```CSS CSS
.container {
  grid-template-rows: [row1-start] 25px [row1-end row2-start] 25px [row2-end];
  grid-template-columns: auto 50px auto;
  grid-template-areas: 
    "header header header" 
    "footer footer footer";
}
```
Since grid-template doesn’t reset the implicit grid properties (grid-auto-columns, grid-auto-rows, and grid-auto-flow), which is probably what you want to do in most cases, it’s recommended to use the grid property instead of grid-template.
