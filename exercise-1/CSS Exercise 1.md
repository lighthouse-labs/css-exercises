# CSS Exercise 1

CSS is the technology we use to apply design to content. CSS also requires a lot of practice. It can be very difficult to practice without content to work with. Furthermore, the design being applied is dependent on the content.

This exercise provides an idea for how to practice with CSS in the absence of Web application content to work with. This is done by finding designs for other media, such as magazines and newpapers, and recreating them using HTML and CSS. We'll walk through the process together, and then you can repeat it with new content as often as you wish.

## Find inspiration

A quick Google image search for "newspaper design inspiration" led me to [this page](http://newspaperdesign.in/m/discussion?id=2134745%3ATopic%3A42622) about the design of the newspaper The National Post. Let's choose one of the pages displayed here and recreate it to the best of our abilities using HTML and CSS. How about this one?

![National Post spread](national-post-page.jpeg)

I think that this would provide a number of examples of common Web design challenges, so let's start there.

## Rough it in

As tempting as it is to start with the content and typography, this design calls for a 'top down' approach. This will help us arrive at some interesting CSS issues sooner and will make our progress more evident. That means we'll start with the grid and then we'll fill in the content and work on the typography.

### The boilerplate

Start with a basic HTML document with a link to a style sheet.

```html
<!doctype html>
<html>
<head>
  <title>Post Sports</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
</body>
</html>
```

### The page

Because we're copying print media, it's meaningful to give the content a static width. Add a container `<div>` inside the `<body>` tag that will wrap all the other contents.

```html
...
<body>
<div class="page-container">
</div>
</body>  
</html>
```

Then, in the CSS file, add some styles to make this visible.

```css
body {
  /* The body gets a grey background so that the page stands out on top of it */
  background: #eee;
}
.page-container {
  /* The page (paper) is white */
  background: #fff;
  /* By setting the left and right margins to 'auto', the page will be horizontally centered */
  margin: 0 auto;
  /* A broadsheet newspaper is 22 inches long, but we use min-height here in case the content ends up longer in our Web version */
  min-height: 22in;
  /* Yep, we can use inches (and centimeters) as units in CSS */
  width: 11in;
}

```

Now that we can see our page, it's time to add some sections.

### The grid

Setting up the grid will take several steps. First we'll identify each of the grid components in the layout; then we'll mark the sections up appropriately; finally we'll write styles that set up our grid appropriately.

Many off-the-shelf CSS grid systems exist. It's important to understand the theory behind grid CSS as well as some of the nomenclature of typographic grids, so we'll be working from scratch in this exercise.

#### Identify the grid

Typographic grids have two primary components: rows and columns. Rows are the rectangles that span from the left edge of their container all the way to the right. Columns are the inner subdivisions of those rows. Many layouts have nested grids where columns are divided further into rows containing more columns. This is such a layout.

There are six grid columns in this layout. Grid columns are equal width divisions of the page. Between each column is a gap called the <dfn>gutter</dfn>. Sometimes there is a line midway through the gutter to separate contents in adjacent columns.

The outermost page can be divided into two rows. The first row contains all of the content in the upper portion of the page, and the second row is the ad at the bottom.

The first row is divided into two columns. The left column is the orange bar. The right column is the rest of the page content. Because the yellow bar along the top spans all the remaining five grid columns, the remaining divisions will have to be inside nested rows.

The second row has one column that spans all six grid columns.

Add this markup inside the `<div class="page-container">` to indicate the outermost rows and columns. Placeholders are added for the content so that it is visible when the HTML page is viewed as we continue.

```html
<div class="row">
  <div class="col-1">
    <div class="placeholder">Left column</div>
  </div>
  <div class="col-5">
    <div class="placeholder">Right column</div>
    <!-- more content will be placed here -->
  </div>
</div>
<div class="row">
  <div class="col-6">
    <div class="placeholder">Advertisement</div>
  </div>
</div>
```

The class `row` is used to markup rows. Columns have classes named `col-n` where `n` is the number of grid columns that are spanned. The only permitted children of a `row` element are `col` elements. `col` elements may contain anything, including more rows.

The next subdivision is in the "Right column". Below the yellow bar at the top it is divided into two more columns. The left column contains the photos and articles and spans four grid columns. The right column contains the "Canada games lacking drama" article.

**This is where we hit one of the tricky parts of CSS grid systems.** We must create a new row element and rows in our CSS are divided into six columns. We want the entire page to appear as though there are six columns, but this new row is only the width of five of those columns. So, we must have a way of indicating that the new nested row is only five of our page's columns wide.

This is addressed by conventional grid systems by choosing a higher number of columns on the page and attempting to fit the design within clean divisions of those columns. However, in our case, we'll specify the number of columns that each row is divided into to get around this issue.

Modify the markup to include this nested division (replacing the comment in the above code listing.)

```html
<div class="row-6">
  <div class="col-1">
    <div class="placeholder">Left column</div>
  </div>
  <div class="col-5">
    <div class="placeholder">Right column</div>
    <div class="row-5">
      <div class="col-4">
        <!-- more content will be placed here -->
      </div>
      <div class="col-1">
        <div class="placeholder">Right article</div>
      </div>
    </div>
  </div>
</div>
<div class="row-1">
  <div class="col-1">
    <div class="placeholder">Advertisement</div>
  </div>
</div>
```

The `row` classes we initially used have been modified to indicate how many columns they contain. The new classes are `row-n` where `n` is the number of divisions within them.

A new placeholder was added for the "Canada games" article because it is nested directly inside of its column. The other content lives within yet another grid.

There are two rows in the center section. The top row is divided into four columns, each with a photo and caption in it. The bottom row is divided into three columns. The left column contains the "January" article. In the center, the "Year in Lip" article spans two grid columns. The right column contains the "February" article.

Modify the markup again to add these last divisions (replacing the comment in the above code listing.)

```html
<div class="row-6">
  <div class="col-1">
    <div class="placeholder">Left column</div>
  </div>
  <div class="col-5">
    <div class="placeholder">Right column</div>
    <div class="row-5">
      <div class="col-4">
        <div class="row-4">
          <div class="col-1">
            <div class="placeholder">Image 1</div>
          </div>
          <div class="col-1">
            <div class="placeholder">Image 2</div>
          </div>
          <div class="col-1">
            <div class="placeholder">Image 3</div>
          </div>
          <div class="col-1">
            <div class="placeholder">Image 4</div>
          </div>
        </div>
        <div class="row-4">
          <div class="col-1">
            <div class="placeholder">Left article</div>
          </div>
          <div class="col-2">
            <div class="placeholder">Center article</div>
          </div>
          <div class="col-1">
            <div class="placeholder">Right article</div>
          </div>
        </div>
      </div>
      <div class="col-1">
        <div class="placeholder">Right article</div>
      </div>
    </div>
  </div>
</div>
<div class="row-1">
  <div class="col-1">
    <div class="placeholder">Advertisement</div>
  </div>
</div>
```

Finally we have a `placeholder` for each part of the page. It's time to write some CSS.

#### Style the grid

Some modern grid systems use the new "flexbox" CSS properties to position columns within the grid, but many continue to use CSS floats to do the same. We will use the float method because it can provide invaluable experience with the CSS box-model.

The first thing we should do is add a style for the `placeholder` class so that its width is visible as we move items around. Add this CSS to make the placeholders visible.

```css
.placeholder {
  background: #ddd;
  margin: 1em 0;
  text-align: center;
}
```

This will made the widths and positions of the placeholders evident.

The next step is to set the widths of the columns appropriately. For each `row-n` class, we must style its child `col-n` classes to have the appropriate width. The CSS for that looks like this.

```css
.row-1 > .col-1,
.row-2 > .col-2,
.row-3 > .col-3,
.row-4 > .col-4,
.row-5 > .col-5,
.row-6 > .col-6 {
  width: 100%;
}
.row-2 > .col-1,
.row-4 > .col-2,
.row-6 > .col-3 {
  width: 50%;
}
.row-3 > .col-1,
.row-6 > .col-2 {
  width: 33.333333%;
}
.row-3 > .col-2,
.row-6 > .col-4 {
  width: 66.666667%;
}
.row-4 > .col-1 {
  width: 25%;
}
.row-4 > .col-3 {
  width: 75%;
}
.row-5 > .col-1 {
  width: 20%;
}
.row-5 > .col-2 {
  width: 40%;
}
.row-5 > .col-3 {
  width: 60%;
}
.row-5 > .col-4 {
  width: 80%;
}
.row-6 > .col-1 {
  width: 16.666667%
}
.row-6 > .col-5 {
  width: 83.333333%
}
```

As you can see, the width has been set for every `col-n` class within every `row-n` class so that the columns take the appropriate width of the page.

Now, if we float all the columns to the left, they will form our grid. Add the following CSS to produce that effect.

```css
.col-1,
.col-2,
.col-3,
.col-4,
.col-5,
.col-6 {
  /* Have all the columns flow side-by-side */
  float: left;
}
```

As we add content, the content will stay within the boundaries of its column. There are further considerations to make with regard to building robust grid systems, but this is the primary concept.

There is one last consideration we must make before moving on, though, and that is the gutter between columns. The gutter should be set to a specific width in pixels, points, or a like unit. We can use padding for the column gutters, but this is where a big "gotcha" comes into play. The default CSS box model would add this padding to the percentage widths we used, breaking the grid. There's a solution, though, and that is to set the `box-sizing` property of the columns to `border-box`. Then the width will not increase with the addition of the padding.

Modify the above CSS code by adding these properties.

```css
.col-1,
.col-2,
.col-3,
.col-4,
.col-5,
.col-6 {
  /* Make sure the padding doesn't break the percentage widths */
  box-sizing: border-box;
  /* Have all the columns flow side-by-side */
  float: left;
  /* Left and right padding is half the gutter width */
  padding: 0 4pt;
}
```

Almost! This added gutters between the columns, but now nested columns have double the gutter they need. The solution is to give the row classes negative left and right margins that are the width of the gutter. Then everything will line up nicely.

Add the following CSS.

```css
.row-1,
.row-2,
.row-3,
.row-4,
.row-5,
.row-6 {
  /* Left and right margins are negative half the gutter width */
  margin: 0 -4pt;
}
```

Beauty! The same tricks can be applied to give the whole page a margin. Add the following CSS rules to the previously defined `.page-container`.

```css
.page-container {
  /* The page (paper) is white */
  background: #fff;
  /* Keep our desired width when adding padding */
  box-sizing: border-box;
  /* By setting the left and right margins to 'auto', the page will be horizontally centered */
  margin: 0 auto;
  /* A broadsheet newspaper is 22 inches long, but we use min-height here in case the content ends up longer in our Web version */
  min-height: 22in;
  /* The padding will be within the specified height and width due to the box-sizing property */
  padding: .5in;
  /* Yep, we can use inches (and centimeters) as units in CSS */
  width: 11in;
}
```

Now it's time to add some content!
