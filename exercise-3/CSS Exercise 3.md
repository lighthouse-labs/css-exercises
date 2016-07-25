# CSS Exercise 3

A big chunk of the project is now done. There will be a couple more tricks to learn, but after that it's just font properties and margins.

## Module 2: Photos with captions

The photos in the middle of the page will be a fun challenge. But before we get to that, there's an easy win.

### The yellow banner

Before we get to the photos, let's have an easy win with the yellow heading at the top of the page. The placeholder containing the text "Right column" can be replaced with this markup.

```html
      <article class="banner-article">
        <h1 class="banner-article-heading">Larry the duck&rsquo;s new name is causing a buzz</h1>
        <p class="call-to-action"><a href="#S6">S6</a></p>
      </article>
```

Then we can style it using these new classes. We will need to set the `<h1>` and `<p>` tags to `display: inline` in order to have them appear on the same row. Then we can center all the text to have equal whitespace on either side. We also need to add some generated content with the `:after` pseudo element to put the comma after the heading.

```css
.banner-article {
  background: #fcd243;
  margin: 0 0 16pt;
  padding: 4pt;
  text-align: center;
}

.banner-article .call-to-action,
.banner-article-heading {
  display: inline;
  font-family: dustismo_romanregular, serif;
  font-size: 23pt;
  font-weight: normal;
  text-transform: uppercase;
}

.banner-article-heading:after {
  content: ',';
}
```

### The photos

Now for the fun part. Let's start by adding semantic markup to replace each of the "Image #" placeholders. These are effectively `<figure>` elements with `<img>` and `<figcaption>` elements within.

It won't matter whether the images are all the same size, or even whether they fit into the appropriate space. We'll use CSS to make them all the same size and center them within the available space.

Replace the HTML containing the image placeholders with this markup.

```html
          <div class="row-4">
            <div class="col-1">
              <figure class="feature-photo">
                <img src="http://placehold.it/300x700" alt="David">
                <figcaption>
                  <p>What was David up to? &lsquo;Writing clean&nbsp;code.&rsquo;</p>
                </figcaption>
              </figure>
            </div>
            <div class="col-1">
              <figure class="feature-photo">
                <img src="http://placehold.it/310x680" alt="Khurram">
                <figcaption>
                  <p>Khurram Virani:<br>The jr. developers &lsquo;don&rsquo;t feel&nbsp;fear&rsquo;</p>
                </figcaption>
              </figure>
            </div>
            <div class="col-1">
              <figure class="feature-photo">
                <img src="http://placehold.it/310x710" alt="Monica">
                <figcaption>
                  <p>Monica will never Daffy what she can&rsquo;t&nbsp;Duck</p>
                </figcaption>
              </figure>
            </div>
            <div class="col-1">
              <figure class="feature-photo">
                <img src="http://placehold.it/295x690" alt="Don">
                <figcaption>
                  <p>Don Burks:<br>There&rsquo;s L.S.D. in&nbsp;coding</p>
                </figcaption>
              </figure>
            </div>
          </div>
```

You'll notice some unusual text in the captions. Curly quotes were used for quotation marks and apostrophes. This makes the typography look much more professional that if straight quotes were used. Also, non-breaking spaces were placed between the last two words of each quote. This is to address a [common typographical issue](https://www.fonts.com/content/learning/fontology/level-2/text-typography/rags-widows-orphans) where only a single word appears on the last line of a multi-line block of text.

Ok, so adding this HTML doesn't look good, and it appears to break things. Time to wrangle the images. We can't use either of the centering strategies we've used so far for the images because we want equal amounts of the image to bleed off either side of the column so that the middle portion of the image is visible. If we used `text-align: center` or `margin: 0 auto` and the image is wider than the column, it would only show the left part of the image.

Instead, we'll position the images absolutely (which means the container needs to be position relative) and then shift them into the center using a combination of the `left` and `transform` properties. Because they're being positioned absolutely, we need to set a static height on both the container and the image so that they take up the same amount of space.

```css
.feature-photo {
  /* Static height of the feature photos */
  height: 8in;
  /* Remove inherited margins */
  margin: 0;
  /* Crop off the parts of the image that bleed out of the container */
  overflow: hidden;
  /* Set this as the containing block of the image */
  position: relative;
}

.feature-photo img {
  /* Same as the height of the container */
  height: 8in;
  /* Position the image 50% of the width of the container to the left */
  left: 50%;
  position: absolute;
  /* Should be flush with the top of the container */
  top: 0;
  /* Shift the image back 50% of its own width to the left in order to center it */
  transform: translateX(-50%);
}
```

Because the `height` property of `<img>` tags default to `auto`, setting a static `height` results in the photos being scaled proportionately.

This looks pretty good, but where did the captions go?! Because the images are positioned absolutely, they cover the captions. Let's also set the captions to be positioned absolutely. While we're at it, we'll set the background colour, padding, and font styles with this CSS.

```css
.feature-photo figcaption {
  background: #fff;
  box-sizing: border-box;
  font-family: Georgia, serif;
  font-size: 9pt;
  left: 0;
  line-height: 1.3;
  padding: 10pt 6pt;
  position: absolute;
  top: 55%;
  width: 75%;
}

.feature-photo figcaption p {
  margin: 0;
}
```

It's pretty close, but in the original design, the positions and alignment of each caption is different. Can we do this with CSS? Yes we can! We'll align each even photo's caption to the right, and then we'll position each caption at a different distance from the top. To do this, we'll need to select the columns themselves using the `:nth-child` pseudo class.

```css
.col-1:nth-child(even) .feature-photo figcaption {
  /* Ensure the left is not still set to 0, otherwise it will conflict with the width property */
  left: auto;
  right: 0;
  /* In addition to aligning the box to the right, align the text to the right as well */
  text-align: right;
}

.col-1:nth-child(2) .feature-photo figcaption {
  top: 80%;
}

.col-1:nth-child(3) .feature-photo figcaption {
  top: 60%;
}

.col-1:nth-child(4) .feature-photo figcaption {
  top: 75%;
}
```

There are probably ways that additional classes or ids could be added to the markup to make these `nth-child` selectors more robust, but because we have no expectation for this markup to change in the future, we're not running any risk by selecting the columns directly. Perhaps a semantic class identifying the purpose of the row and columns could rectify this.

The last few modules of content will be addressed in the next exercise.
