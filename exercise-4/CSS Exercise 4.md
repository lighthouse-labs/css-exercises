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
                <img src="http://placehold.it/200x133" alt="James">
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
              <p class="call-to-action">See <em class="yelling">Canada</em> on <a href="#S3">Page S3</a></p>
            </footer>
          </article>
```

### The header

With this semantic markup, we can start applying styles to match the design. Add these font styles for the heading and subhead of the article. The same trick from part 2 is used for the borders below the headings.

```css
/* Adds fixed width borders below header sections */
.article-author:after,
.article-heading:after,
.article-subhead:after {
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
  line-height: 1.2;
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


