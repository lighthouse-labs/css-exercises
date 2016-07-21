# CSS Exercise 2

We have a grid all set up. The next step is to add the content and style it appropriately. We'll take this one module at a time, slowly replacing each `placeholder` element with the content of the original design.

## Module 1: Labs Tech

We can't style anything until we've added some content. It's not necessary to copy the content verbatim, but the content should have about the same amount and length of words so that we can make design decisions the same as the original designer.

### The content

The placeholder `<div>` containing the text "Left column" should be replaced by the markup below.

```html
      <nav class="nav-primary">
        <header class="nav-brand">
          <h1 class="nav-title">Labs Tech</h1>
          <div class="nav-brand-mark">LL</div>
          <p class="nav-brand-link"><a href="http://lighthouselabs.ca/">lighthouselabs.ca</a></p>
        </header>
        <figure class="nav-news">
          <img src="http://placehold.it/75x75" alt="QR Code">
          <figcaption class="nav-news-caption">
            <p>Breaking tech news now.</p>
            <p class="call-to-action"><a href="#A2">How this works, A2</a></p>
          </figcaption>
        </figure>
        <article class="nav-article">
          <h1 class="nav-article-heading">SQL</h1>
          <h2 class="nav-article-subhead">Memorable moments</h2>
          <p class="nav-article-hook">A lighter look at the year that was in SQL.</p>
          <p class="call-to-action"><a href="#S4">Full Outer Join, S4</a></p>
        </article>
        <article class="nav-article">
          <h1 class="nav-article-heading">ERB</h1>
          <h2 class="nav-article-subhead">Passing fancy</h2>
          <p class="nav-article-hook">Server-side templating is not as hard as it used to be.</p>
          <p class="call-to-action"><a href="#S5">Page S5</a></p>
        </article>
        <article class="nav-article">
          <h1 class="nav-article-heading">2016</h1>
          <h2 class="nav-article-subhead">Year in tech</h2>
          <p class="nav-article-hook">A look at some of the year's big stories, including Don Burks' dominant season.</p>
          <p class="call-to-action"><a href="#S8">Page S8</a></p>
        </article>
      </nav>
```

You'll notice I decided that this part of the page is a `<nav>`. This is because it contains links to other pages of the newspaper in the form of page numbers. Other semantic tag choices were made. Class names were chosen to allow for us to style the content without the worry of breaking the styling by changing which tags are used.

### The colours

Alright, a good place to start with this module is the colours. They stand out quite well from the rest of the page. To do this, we'll change the background and foreground colours of the `.nav-primary` class. It's important not to style the column or row elements. They've played their part and can be left alone for the remainder of the design.

Add this CSS to the stylesheet. The colours were obtained using [Chrome's eye dropper tool](http://stackoverflow.com/questions/28716775/how-to-use-color-picker-eye-dropper).

```css
.nav-primary {
  background: #f17030;
  color: #fff;
}
```

Already we're seeing the grid system at work. One thing that jumps out at this point is the colour of the links. Because this is a newspaper, blue underlined links aren't going to work for us. What we can do is set the global link styles so that they inherit the text colour of their parent. That is done with the following CSS.

```css
a {
  color: inherit;
  text-decoration: none;
}
```

### The type

A couple more easy wins for this section are to center the text and add padding. Add these properties to the `.nav-primary` selector defined above.

```css
.nav-primary {
  background: #f17030;
  color: #fff;
  padding: 4pt;
  text-align: center;
}
```

Let's find a condensed serif font to use for this project. [This one](https://www.fontsquirrel.com/fonts/Dustismo-Roman?filter%5Btags%5D%5B0%5D=condensed&filter%5Btags%5D%5B1%5D=serif) could work. After following the instructions to download the fonts and link them to the document, the `.nav-title` can be set to this font family like this.

```css
.nav-title {
  font-family: dustismo_romanregular, serif;
}
```

We'll also need a condensed sans-serif font. [This one](https://fonts.google.com/specimen/Pragati+Narrow?category=Sans+Serif&width=3&selection.family=Pragati+Narrow:400,700) is hosted by Google Fonts, which is much easier to include into the project. After following the instructions to import the font stylesheet, the `.nav-brand-link` can be set to this font family like this.

```css
.nav-brand-link {
  font-family: 'Pragati Narrow', sans-serif;
}
```

### The sideways text

No we can start to get fancy. Let's get that big sideways text out of the way. We might have to cheat a little, but all we want is for it to look good. We can do that.

Now comes the magic. Below are the rest of the styles for the sideways text.

```css
.nav-brand {
  /* This needs to be set so that the sideways text in .nav-title can be positioned absolutely */
  position: relative;
  /* This makes space for the sideways text */
  padding-top: 9in;
}

.nav-title {
  font-family: dustismo_romanregular, serif;
  /* A lot of tweaking had to happen to find this font size */
  font-size: 132pt;
  font-weight: normal;
  /* This element is positioned absolutely, so the left edge is a good place to put it horizontally */
  left: 0;
  /* The line-height property is used to make sure the sideways text has equal space on either side */
  line-height: 98pt;
  /* The element this class is applied to might have default margins, so this removes those */
  margin: 0;
  position: absolute;
  /* Rather than using uppercase in the HTML, CSS can set text to uppercase (since it's presentational) */
  text-transform: uppercase;
  /* This value is used for the padding at the top of the header */
  top: 9in;
  /* These rules rotate the text */
  transform: rotate(-90deg);
  transform-origin: left top 0;
  /* This prevents the text from wrapping, which it would do normally because it's SO BIG */
  white-space: nowrap;
}
```

That was definitely the toughest part. One day there will be a CSS property specifically for sideways text, but for now, this hack will do. Let's get to the subtler and more valuable parts of this module.

### The brand

The next couple little things we can work on are the brand mark and link that come right below the sideways text. The brand mark is interesting because, if we want it to be a square, we'll have to set its width _and_ height to some specific value. Then we'll need to center both the block and the text within it. In order to write robust styles, we'll add `text-align: center` to this element, too, event though it inherits that from its container. This will allow it to be reused elsewhere if need be. To vertically center the text in its container, we can set the `line-height` to the same value as the `height`. This is what the finished styles look like.

```css
.nav-brand-mark {
  border: 1px solid #fff;
  font-family: dustismo_romanregular, serif;
  font-size: 26pt;
  height: 34pt;
  line-height: 34pt;
  /* Left and right margins are set to auto to horizontally center the whole block */
  margin: 0 auto;
  text-align: center;
  width: 34pt;
}
```

But we're not done there! The little cursor pointer can be approximated with CSS, too.

```css
.nav-brand-mark {
  border: 1px solid #fff;
  font-family: dustismo_romanregular, serif;
  font-size: 26pt;
  height: 34pt;
  line-height: 34pt;
  /* Left and right margins are set to auto to horizontally center the whole block */
  margin: 0 auto;
  /* This is set so that the generated :after content can be positioned absolutely */
  position: relative;
  text-align: center;
  width: 34pt;
}

/* Figure this out on your own! */
.nav-brand-mark:after {
  bottom: -15pt;
  content: '\27A4';
  font-size: 15pt;
  position: absolute;
  right: -7pt;
  text-shadow: 0 0 1px #000;
  transform: rotate(-135deg);
}
```

The last couple little changes that need to be made are the styles for the website link. Only minor typographical changes are necessary to get it looking like the newspaper.

```css
.nav-brand-link {
  font-family: 'Pragati Narrow', sans-serif;
  font-size: 14pt;
  margin: 4pt 0;
}
```

### The rest

The rest of this section is merely typigraphical. The only neat trick is adding the fixed width underline below the article headings. This will also use generated content (the `:after` pseudo element.) Add the styles below to accomplish this.

```css
.nav-article-heading:after {
  background: #fff;
  /* content needs to be set, otherwise nothing appears */
  content: '';
  display: block;
  height: 1px;
  margin: 4pt auto;
  width: 34pt;
}
```

All the rest is setting the correct font families, styles, weights, alignments, text transforms, and margins to the remaining contents. Try your best to do this without guidance. These are all the styles to complete this exercise.

```css
a {
  color: inherit;
  text-decoration: none;
}

.call-to-action {
  font-family: dustismoroman_italic, serif;
  font-style: italic;
}

.nav-article {
  margin: 12pt 0;
}

.nav-article .call-to-action {
  font-size: 12pt;
  margin: 0;
}

.nav-article-heading {
  font-family: dustismo_romanregular, serif;
  font-weight: normal;
  font-size: 26pt;
  /* Don't need to take more space than necessary for headings */
  line-height: 1;
  /* Eliminate inherited margins */
  margin: 0;
}

.nav-article-heading:after {
  background: #fff;
  /* content needs to be set, otherwise nothing appears */
  content: '';
  display: block;
  height: 1px;
  margin: 4pt auto;
  width: 34pt;
}

.nav-article-hook {
  font-family: dustismo_romanregular, serif;
  font-size: 12pt;
  font-weight: normal;
  line-height: 14pt;
  margin: 0;
  word-spacing: -2pt;
}

.nav-article-subhead {
  font-family: 'Pragati Narrow', sans-serif;
  font-size: 16pt;
  font-weight: normal;
  line-height: 1;
  margin: 8pt 0 0;
  text-transform: uppercase;
}

.nav-brand {
  /* This needs to be set so that the sideways text in .nav-title can be positioned absolutely */
  position: relative;
  /* This makes space for the sideways text */
  padding-top: 9in;
}

.nav-brand-link {
  font-family: 'Pragati Narrow', sans-serif;
  font-size: 14pt;
  margin: 4pt 0;
}

.nav-brand-mark {
  border: 1px solid #fff;
  font-family: dustismo_romanregular, serif;
  font-size: 26pt;
  font-weight: normal;
  height: 34pt;
  line-height: 34pt;
  /* Left and right margins are set to auto to horizontally center the whole block */
  margin: 0 auto;
  /* This is set so that the generated :after content can be positioned absolutely */
  position: relative;
  text-align: center;
  width: 34pt;
}

.nav-brand-mark:after {
  bottom: -15pt;
  content: '\27A4';
  font-size: 15pt;
  position: absolute;
  right: -7pt;
  text-shadow: 0 0 1px #000;
  transform: rotate(-135deg);
}

.nav-news {
  /* Font settings are here to avoid needing to style child elements directly */
  font-family: 'Pragati Narrow', sans-serif;
  font-size: 11pt;
  line-height: 1;
  margin: 8pt 0;
}

.nav-news img {
  border: 6pt solid #fff;
  /* This prevents weird spacing from placing the image on the text baseline */
  display: block;
  /* This centers the image after setting it to display block */
  margin: 0 auto;
}

.nav-news p {
  /* It can be assumed that if any p tags are within this module, their margins should be reset */
  margin: 4pt 0;
}

.nav-news .call-to-action {
  font-size: 9pt;
}

.nav-primary {
  background: #f17030;
  color: #fff;
  padding: 4pt;
  text-align: center;
}

.nav-title {
  font-family: dustismo_romanregular, serif;
  /* A lot of tweaking had to happen to find this font size */
  font-size: 132pt;
  font-weight: normal;
  /* This element is positioned absolutely, so the left edge is a good place to put it horizontally */
  left: 0;
  /* The line-height property is used to make sure the sideways text has equal space on either side */
  line-height: 98pt;
  /* The element this class is applied to might have default margins, so this removes those */
  margin: 0;
  position: absolute;
  /* Rather than using uppercase in the HTML, CSS can set text to uppercase (since it's presentational) */
  text-transform: uppercase;
  /* This value is used for the padding at the top of the header */
  top: 9in;
  /* These rules rotate the text */
  transform: rotate(-90deg);
  transform-origin: left top 0;
  /* This prevents the text from wrapping, which it would do normally because it's SO BIG */
  white-space: nowrap;
}
```

Having the right fonts makes a huge difference to a design. Luckily, because we only needed a couple fonts, switching them out if a better one is found shouldn't be too difficult. If we were using SASS and set the font families to variables, it would be a non-issue.

Next exercise, more modules!


