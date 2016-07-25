# CSS Exercise 4

Finally, the home stretch. Much of the remainder of the content is font styles, however, there are a few neat tricks to learn. Let's polish this design off!

## Module 3: An article

On the right hand side of the page is a proper newspaper article. It contains several different elements in the header, but then goes into a series of paragraphs shortly. Replace the "Right article" placeholder with this markup.

```html
          <article class="article">
            <header>
              <h1 class="article-heading">T-shirt contest lacking felines</h1>
              <h2 class="article-subhead">Opponents in wolf shirts on Wednesdays</h2>
              <figure class="article-author">
                <img src="http://placehold.it/200x140" alt="James">
                <figcaption>
                  <span class="article-author-name">James Sapara</span>
                  <span class="article-author-location">in Vancouver</span>
                </figcaption>
              </figure>
            </header>
            <main>
              <p class="lead">Walk on car leaving trail of paw prints on hood and windshield wake up human for food at 4am or scamper.</p>
              <p>Stand in front of the computer screen scratch leg; meow for can opener to feed me. Hola te quiero immediately regret falling into bathtub for eat the fat cats food.</p>
              <p>Lie on your belly and purr when you are asleep scratch leg; meow for can opener to feed me or fall over dead (not really but gets sypathy) paw at your fat belly so shake treat bag.</p>
              <p>Attack feet has closed eyes but still sees you for rub face on everything, so chew iPad power cord sleep on dog bed, force dog to sleep on floor so stand in front of the computer screen poop in litter box, scratch the walls.</p>
              <p>Where is my slave? I'm getting hungry lick yarn hanging out of own butt thug cat intently sniff hand.</p>
              <p>Attack feet refuse to drink water except out of someone's glass plan steps for world domination or climb leg.</p>
              <p>Find something else more interesting chase mice, yet sit in window and stare ooo, a bird!</p>
              <p>yum yet hide at bottom of staircase to trip human, play time. Damn that dog chase mice.</p>
              <p>Lick the other cats brown cats with pink ears instantly break out into full speed gallop across the house for no reason shove bum in owner's face like camera lens nap all day, so meowing non stop for food.</p>
              <p>Claws in your leg swat at dog, but stare at wall turn and meow stare at wall some more meow again continue staring chase after silly colored fish toys around the house so lick butt if it smells like fish eat as much as you wish, or rub face on everything.</p>
              <p>See owner, run in terror behind the couch. Kitty scratches couch bad kitty attack the dog then pretend like nothing happened fall asleep on the washing machine for scratch leg; meow for can opener to feed me scream at teh bath chase imaginary bugs, for shake treat bag.</p>
              <p>Intently stare at the same spot vommit food and eat it again, hunt anything that moves immediately regret falling into bathtub stare out the window.</p>
            </main>
            <footer>
              <p class="call-to-action">See <em class="yelling">cats</em> on <a href="#S3">Page S3</a></p>
            </footer>
          </article>
```

### The header

With this semantic markup, we can start applying styles to match the design. Add these font styles for the heading and subhead of the article. The same trick from part 2 is used for the borders below the headings.

```css
/* Adds fixed width borders below header sections */
.article-author:after,
.article-subhead:after,
.article-subhead:before {
  background: #000;
  /* content needs to be set, otherwise nothing appears */
  content: '';
  display: block;
  height: 1px;
  margin: 10pt auto;
  width: 34pt;
}

.article-heading {
  font-family: dustismoroman_italic, serif;
  font-size: 26pt;
  font-style: italic;
  font-weight: normal;
  line-height: 1;
  margin: 0;
  text-align: center;
}

.article-subhead {
  font-family: dustismo_romanregular, serif;
  font-size: 16pt;
  font-weight: normal;
  line-height: 1;
  margin: 0;
  text-align: center;
}
```

We're getting close to some "normal" content at this point. That is, paragraphs of prose can mostly inherit their styles from the base styles of the module or page. Let's set up some base styles for the `.article` module before doing the author section.

```css
.article {
  font-family: Georgia, serif;
  font-size: 9pt;
  line-height: 1.3;
  text-align: justify;
}
```

With these font basics set for the entire article, let's make only the changes that need to happen to get the author section looking like it should.

```css
.article-author {
  margin: 0;
  text-align: center;
}

.article-author figcaption {
  margin: 10pt 0;
}

/* Ensure author image is centered and doesn't bleed out of column */
.article-author img {
  display: block;
  margin: 0 auto;
  max-width: 100%;
}

.article-author-location {
  /* Puts this element on its own line */
  display: block;
  font-style: italic;
}

.article-author-name {
  /* Puts this element on its own line */
  display: block;
  font-weight: bold;
}
```

### The main content

On to the article itself. Paragraphs in print typically don't have margins between them and are indicated by indentation. Add these styles to accomplish that.

```css
.article p {
  margin: 0;
  text-indent: 1.5em;
}
```

Now the fun bit! The drop cap in the leading paragraph of the article can be created without any additional markup. CSS provides a pseudo class for the first letter of an element, so we can just select and then style that. Because the text should wrap around the initial letter, it can be floated to the left. The rest are font styles.

```css
/* This selector needs to be more specific than `.article p` in order to be able to override the text-indent property */
.article p.lead {
  text-indent: 0;
}

.article .lead:first-letter {
  color: #25669d;
  float: left;
  font-size: 3.9em;
  line-height: .85;
  margin-right: 2pt;
}
```

Lastly, the styles of the `.call-to-action` differ in articles in that they aren't italic. Additionally, the typesetter decided to yell CANADA in the footer, so we'll add a class for that. The tag used for the yelling text was `<em>` which displays in italic by default, so we need to remove that style while adding the text transform to uppercase.

Add these styles to finish off this module.

```css
.article .call-to-action {
  font-family: inherit;
  font-style: normal;
}

.yelling {
  font-weight: normal;
  text-transform: uppercase;
}
```

## Module 4: Quotes and feature

The last of the content on the page are the two articles containing quotes and the large page header in the middle. Add this semantic markup to replace the placeholder elements.

```html
            <div class="col-1">
              <article class="article quotes-article">
                <header>
                  <h1 class="article-heading">Salty dogs</h1>
                </header>
                <main>
                  <p><q>There are two ways of constructing a software design: One way is to make it so simple that there are obviously no deficiencies, and the other way is to make it so complicated that there are no obvious deficiencies. The first method is far more difficult.</q> &mdash; British computer scientist <b class="quote-author">C.A.R. Hoare</b>, winner of the 1980 Turing Award.</p>
                  <p><q>If debugging is the process of removing software bugs, then programming must be the process of putting them in.</q> &mdash; Dutch computer scientist <b class="quote-author">Edsger Dijkstra</b>, winner of the 1972 Turing Award.</p>
                  <p><q>Measuring programming progress by lines of code is like measuring aircraft building progress by weight.</q> &mdash; co-founder of Microsoft <b class="quote-author">Bill Gates</b>.</p>
                  <p><q>Nine people can&rsquo;t make a baby in a month.</q> &mdash; American computer scientist, winner of the 1999 Turing Award <b class="quote-author">Fred Brooks</b> regarding the addition of more programmers to get a project completed faster.</p>
                  <p><q>C makes it easy to shoot yourself in the foot; C++ makes it harder, but when you do, it blows away your whole leg.</q> &mdash; Danish computer scientist <b class="quote-author">Bjarne Stroustrup</b>, developer of the C++ programming language.</p>
                </main>
              </article>
            </div>
            <div class="col-2">
              <article class="feature-article">
                <header class="feature-article-header">
                  <h1 class="feature-article-heading">The <b>year</b> at <b>LHL</b></h1>
                  <h2 class="feature-article-subhead">Year in <b>tech</b> <span class="credit">from The Labs</span></h2>
                </header>
                <main>
                  <p class="lead">What a great year in tech, good on so many fronts if only we could list them all. But there were still challenges to overcome, and that&rsquo;s a good thing. <b class="toast">Here is to just as great a year in 2017, everybody.</b></p>
                </main>
              </article>
            </div>
            <div class="col-1">
              <article class="article quotes-article">
                <header>
                  <h1 class="article-heading">Wise words</h1>
                </header>
                <main>
                  <p><q>Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it.</q> &mdash; Canadian computer scientist <b class="quote-author">Brian W. Kernighan</b>, co-author of <cite>The C programming language</cite>.</p>
                  <p><q>Computer science education cannot make anybody an expert programmer any more than studying brushes and pigment can make somebody an expert painter.</q> &mdash; American programmer and open source software advocate <b class="quote-author">Eric S. Raymond</b>, author of <cite>The Cathedral and the Bazaar</cite>.</p>
                  <p><q>Most good programmers do programming not because they expect to get paid or get adulation by the public, but because it is fun to program.</q> &mdash; Finnish American software engineer and hacker <b class="quote-author">Linus Torvalds</b>, principal force behind the development of the Linux kernel.</p>
                  <p><q>One of my most productive days was throwing away 1000 lines of code.</q> &mdash; computer scientist <b class="quote-author">Ken Thompson</b>, early developer of UNIX OS.</p>
                  <p><q>People think that computer science is the art of geniuses but the actual reality is the opposite, just many people doing things that build on each other, like a wall of mini stones.</q> &mdash; computer scientist <b class="quote-author">Donald Knuth</b>.</p>
                </main>
                <footer>
                  <p class="call-to-action">See <em class="yelling">year</em> on <a href="#S2">Page S2</a></p>
                </footer>
              </article>
            </div>
```

Some choices of note include extending the basic `.article` class by adding `.quotes-article` in addition to it. With this, the base font styles for articles are inherited but can be overridden with a more specific selector containing both classes.

The quotations are wrapped in the little used `<q>` tag, which is meant for inline quotations such as these. Proper em-dashes are used instead of hyphen-minus characters. `<cite>` tags are used where appropriate for titles of works.

In both the quote articles and the feature in the middle, `<b>` tags are used where text is typographically offset from surrounding text without conveying any additional meaning. This is the new usage of `<b>` as of HTML 5.

### The quotes

There are a couple default styles that won't work for us to copy this design. The `<cite>` element displays in italics by default, but we want it unstyled. The `<q>` element has straight quotes around it, but we want curly quotes. Add this CSS to make those changes.

```css
cite {
  font-style: normal;
}

q:after {
  content: "\201D";
}

q:before {
  content: "\201C";
}
```

The quotes articles' paragraphs aren't so much indented as they're preceded by a grey rectangle. I think the solution in CSS is to remove indentation from `.article.quotes-article p` but then add the grey blocks as a border on the inline quotes themselves. Paragraphs are also left aligned instead of fully justified. Strangely, the call to action is indented, but not the same amount as the regular article. It's only indented as much as the grey border plus the padding on the inline quotes. That can be accomplished with this CSS.

```css
.article.quotes-article {
  text-align: left;
}

.article.quotes-article p {
  text-indent: 0;
}

.article.quotes-article q {
  border-left: 4pt solid #ccc;
  padding-left: 3pt;
}

.article.quotes-article .call-to-action {
  text-indent: 7pt;
}
```

The only other styles to apply to these articles are some font and margin properties for the heading and quote authors. This CSS can be added for that.

```css
.article.quotes-article .article-heading {
  font-size: 18pt;
  margin: 3pt 0 8pt;
  text-align: left;
  text-transform: uppercase;
}

.article.quotes-article .quote-author {
  font-family: 'Pragati Narrow', sans-serif;
  font-weight: bold;
}
```

### The splashy heading

The last content in this design is the big, splashy heading. There are two items to note in this section. The dotted grey borders above some of the words can be accomplished using the same old generated content trick, but instead of applying a background colour to a box, we'll add a dotted border. The other is the orange badge, which will have to be positioned absolutely, given a 50% border radius to create a circle, given a box shadow in order to get the double border effect, and rotated using the translate property. Along with the fonts, colours, and margins, those styles should manifest like this.

```css
.feature-article .lead {
  color: #999;
  font-family: dustismo_romanregular, serif;
  font-size: 19pt;
  line-height: 1.2;
  text-align: center;
}

.feature-article .lead .toast {
  color: #0f7a77;
  display: block;
  font-weight: normal;
}

.feature-article-header {
  /* So that the subhead can be positioned absolutely */
  position: relative;
}

.feature-article-heading {
  font-family: 'Pragati Narrow', sans-serif;
  font-size: 116pt;
  font-weight: 200;
  /* The font isn't as condensed as desired, so squish in, everybody */
  letter-spacing: -5pt;
  line-height: .75;
  margin: 6pt 0;
  text-align: center;
  text-transform: uppercase;
}

.feature-article-heading:before,
.feature-article-heading b:first-child:after,
.feature-article-heading b:first-child:before {
  /* By using both the top and bottom borders, the dots appear more like lines like in the design */
  border-bottom: 5pt dotted #ccc;
  border-top: 5pt dotted #ccc;
  content: '';
  display: block;
  /* Setting negative margins the height of the border makes it fill the leading (gap) without adding space */
  margin: -5pt auto;
  width: 75%;
}

.feature-article-heading b {
  color: #0f7a77;
  /* So that each word is on a separate line */
  display: block;
  /* Being explicit, because we might consider overriding the default for b tags */
  font-weight: bold;
}

.feature-article-subhead {
  background: #f17030;
  border: 4pt solid #f17030;
  border-radius: 50%;
  box-shadow: inset 0 0 1px 1px #fab990;
  color: #fff;
  font-family: 'Pragati Narrow', sans-serif;
  font-size: 10pt;
  font-weight: normal;
  /* This plus the top padding should equal the width in order to create a circle */
  height: 52pt;
  line-height: .8;
  padding-top: 14pt;
  position: absolute;
  right: 0;
  transform: rotate(-20deg);
  text-align: center;
  text-transform: uppercase;
  top: 174pt;
  width: 66pt;
}

.feature-article-subhead b {
  color: #fab990;
  display: block;
  font-size: 28pt;
  font-weight: normal;
}

.feature-article-subhead .credit {
  color: #fab990;
  display: block;
  font-size: 8pt;
}
```

Dotted borders look a little different in different browsers, so ultimately to copy the design perfectly, we might need to use an image. Also, unfortunately, copying the design perfectly necessitates having all the right weights of the right fonts, but this is close enough for this exercise.

### Finishing touches

There's no need to style the ad at the bottom. Normally ads in websites are loaded into `<iframe>` elements, so we don't have control over the way they look. Let's just replace that last placeholder with an image that's about the right size.

```html
      <aside class="ad">
        <img src="http://placehold.it/1200x450" alt="Advertisement">
      </aside>
```

Then add the few styles to make it fit nicely into the layout.

```css
.ad {
  margin: 12pt 0 0;
}

.ad img {
  display: block;
  margin: 12pt 0;
  max-width: 100%;
}
```

There's one last feature missing, and that's the borders dividing the rows and columns. There is a decision to make here. Should we identify the specific modules that need borders in the gutters by giving them id attributes and then style the id selectors or do we create presentational class names and apply them to the appropriate row and column elements? The first is more "pure" and the second is more practical. Ultimately, the practical choice outweighs the pure choice when considering the reusability and maintainability of a code base, so we'll create a handful of presentational classes to add to our (already presentational) grid system.

```css
.large-thematic-break-bottom {
  border-bottom: 12pt solid #c6c6c6;
}

.medium-thematic-break-right {
  border-right: 1pt solid #999;
}

.medium-thematic-break-top {
  border-top: 1pt solid #999;
}

.small-thematic-break-left {
  border-left: 1pt dotted #999;
}

.small-thematic-break-right {
  border-right: 1pt dotted #999;
}
```

These are the subset of all possible classes of this kind that we could define that we need for this layout. Can you determine which elements to apply them to to get the best result?

## Conclusion

This was a lot of work, and as you can see, even with a ton of tricks, CSS struggles to do everything that desktop publishing software can achieve. Times are changing, and it's getting easier, but at the same time Web designers are changing the way they approach design to play to the strengths of CSS and leave some baggage of print design behind. It's still great practice to emulate print designs to get a good handle on CSS. Once these basics are solid, though, it will be time to dive into the cool features CSS has that print doesn't, such as flex-box and responsive layouts, animations, 3D transforms, and more!
