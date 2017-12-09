# Hexi-Flexi Grid

[Github Page](https://vmcreative.github.io/Hexi-Flexi-Grid/)

Hexi-Flexi Grid is an SCSS component, built on the CSS Grid layout, that creates a hexagonal lattice. The mixin includes a number of customizeable settings to control the size, layout and look of the hex grid.

## Features
- Pure CSS styling, no JavaScript
- Flexible height, width, column and row counts
- Modular styling for individual cells, columns and rows
- Supports auto-populating background images

## Browser Support
- Firefox 56+
- Chrome 61+
- Safari 10.1+
- iOS Safari 10.3+
- Chrome for Android 62+
- IE 11/Edge: CSS Grid is currently supported in modern IE and Edge, however Hexi-Flexi Grid makes use of CSS clip-path, which is not supported. A work-around for this would be to populate the grid with hexagonal SVG img elements, as SVG is universally supported by modern browsers.

## Getting Started
To build a basic 3x2 hex grid, follow the steps listed below.

### HTML
Include the following nested div tree in your HTML markup at the location you want to build the hex grid. Give the top level parent a unique id.
Within the div with the class `.hexContainer`, include a number of divs with the class `.hex` equal to the number of hexagonal cells in the grid (in this case 6).

```
<div id="myHexGrid">
  <div class="hexCrop">
    <div class="hexContainer">
      <div class="hex"></div>
      <div class="hex"></div>
      <div class="hex"></div>
      <div class="hex"></div>
      <div class="hex"></div>
      <div class="hex"></div>
    </div>
  </div>
</div>
```

### SCSS
Include the Hexi-Flexi Grid component files in the same directory as your main SCSS file. Within your main SCSS file, import `hex-style.scss` above any rules that will affect the content of the grid.

```
@import 'path/to/hex-style.scss';
```

Inside of `hex-style` is a modular block of code that contains settings for the hex grid. Set the id selector the top of the code block to match the id of the top-level parent div.
If there will be multiple unique hex grids, duplicate this code block for each unique id.

```
#myHexGrid {
  $gridWidth:   20em;
  $gridHeight:  auto;
  $columnCount: 3;
  $rowCount:    2;
  $hexCount:    auto;
  $hexLayout:   row;
  $gridOrient:  vertical;
  $crop:        none;
  $cropFactor:  1;
  $hexContent:  auto;
  $hexSize:     auto;
  $hexMargin:   0.5em;
  $hexShape:    hexagon;
  $hexColor:    #48a999;
  $breakpoints: none;
  $images:      none;

  // ...

}
```

### Customization
The grid can be assigned custom css from inside the `hex-style` codeblock.
Hexi-Flexi Grid assigns unique class names to each individual column, row and cell in the hex grid. 
- `.c-[n]` targets every cell in column [n]. 
- `.r-[n]` targets every cell in row [n]. 
- `.c-[n1].r-[n2]` targets the cell located at column [n1], row [n2].

```
#myHexGrid {

  // ...

  margin: 2em;
    // create 2em margin around the grid

  .c-1 {background-color: red;}
    // column 1 cells will be red

  .r-2 {transform: scale(0.8);}
    // row 2 cells will be 80% as large

  .c-3.r-1 {opacity:0.5;}
    // make column 3, row 1 50% opaque

  // ...

}
```

## Grid Settings

### $gridWidth
Set the width of the hex grid.

- **'auto'**  The grid width will match the ratio of $gridHeight. When set to auto, $gridHeight must be explicitly set.
- **_length_**	Explicitly set the height. Note: percent width is not supported.

### $gridHeight
Set the height of the hex grid.

- **'auto'**	The grid height will match the ratio of $gridWidth. When set to auto, $gridWidth must be explicitly set.
- **_length_**	Explicitly set the height. Note: percent height is not supported.

### $columnCount
Set the number of columns in the hex grid.

- **'auto'**	The column count will match the number of cells divided by the number of rows. When set to auto, $rowCount and $hexCount must be explicitly set.
- **_number_**	Explicitly set the number of columns.

### $rowCount
Set the number of rows in the hex grid.

- **'auto'**	The row count will match the number of cells divided by the number of columns. When set to auto, $columnCount and $hexCount must be explicitly set.
- **_number_**	Explicitly set the number of rows.

### $hexCount
Set the number of hex cells in the hex grid.

- **'auto'**	The cell count will match the number of columns times the number of rows. When set to auto, $rowCount and $columnCount must be explicitly set.
- **_number_**	Explicitly set the number of cells.

### $hexLayout
Set the direction the cells will populate the grid.

- **'row'**	Cells will populate the grid starting at the top left corner and filling in horizontally, spilling over into the next row once each has filled.
- **'column'**	Cells will populate the grid starting at the top left corner and filling in vertically, spilling over into the next column once each has filled.

### $gridOrient
Set the orientation in which the grid cells will align.

- **'vertical'**	Columns will run in straight lines, rows will offset by one half cell.
- **'horizontal'**	Rows will run in straight lines, rows will offset by one half cell.

### $crop
Set whether the grid will be rectangularly cropped.

- **'none'**	The grid will be uncropped.
- **'crop'**	The grid will be scaled by the factor set with $cropFactor and overflow is hidden.

### $cropFactor
Set the amount the grid will be scaled when it is cropped.

- **number**	Explicitly set the crop-factor. A value of 1.2 will scale the grid by 120%.

### $hexContent
Set the behavior of the cell content.

- **'auto'**	Cell content will stretch to cover the entire size of the cell, minus the value of $hexMargin.
- **'center'**	Cell content will be centered, and will match the value of $hexSize. $hexMargin will be ignored.

### $hexSize
Set the size of the cells.

- **'auto'**	Cells will take up 100% of the available space.
- **_number_**	Explicitly set the cell size. Note: percent size is not supported.

### $hexMargin
Set the size of the margins on the cells.

- **_number_**	Explicitly set the cell margin. Note: percent size is not supported.

### $hexShape
Set the shape of the clip-mask on the cells.

- **'hexagon'**	Cells will be hexagonal.
- **'circle'**	Cells will be circular.

### $hexColor
Set the background color of the cells.

- **_color_**	Accepts hexcode, rgb/a and named colors.

### $images
Set a list of files to be passed to the hex cells as background images. The files will be added to the grid according to the order specified by $gridLayout.
A value of 'none' will disable $images.

```
#myHexGrid {

  // ...

  $images:
    'path/to/image-1.jpg'
    'path/to/image-2.jpg'
    'path/to/image-3.jpg'
    'path/to/image-4.jpg'
    'path/to/image-5.jpg'
    'path/to/image-6.jpg'
  ;

  // ...

}
```
