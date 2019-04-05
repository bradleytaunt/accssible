---
layout: post
title: "TypeTip 01: Indenting text"
description: Implement better typography styling by taking advantage of text-indent
summary: Implement better typography styling by taking advantage of the extremely useful CSS text-indent property.
tags: 
    - design
    - typetips
---

<div class="message">
<strong>TypeTip series:</strong><br>
In this small series I take a look at some useful yet less unknown typography specific CSS properties.
</div>

A lot of developers tend to do the bare minimum when it comes to implementing proper website typography. This isn't an insult - I'm happy that typography is given any thought at all during development, I just believe more can always be done to improve upon it.

In today's *TypeTip* we're going to play around with the `text-indent` property, look into when it's best to use it and how to implement it properly.

## The property and browser support

Browser support is actually pretty great for such a regularly over-looked CSS property. All major desktop and mobile browsers support it:

<figure>
    {% cloudinary /public/images/text-indent-compatibility.png alt="Text indent browser compatibility" %}
    <span class="marginnote">Full support across all browsers.</span>
</figure>

Now that doesn't mean you should just slap this property on all your type elements and call it a day - there are specific use cases for `text-indent` and some basic rules to follow:

#### Use Cases

1. Increasing readability of large text blocks that would otherwise overwhelm the reader
2. Replicating book or report typography layouts


#### Basic Rules

1. Best to set this property on inner type children only - meaning items like `p` or `blockquotes` instead of main headings
2. When used on paragraph tags it's best to target only `p` elements that directly follow a sibling tag (see "The CSS" below)

## The CSS

Adding the property is extremely trivial, all you need is the following:

```css
/* Best practice for paragraphs */
p + p {
    text-indent: 1rem; /* whatever you want */
}
```

## Let's see it in action

<p class="codepen" data-height="460" data-theme-id="0" data-default-tab="css,result" data-user="bradleytaunt" data-slug-hash="OGXLEd" data-preview="true" style="height: 460px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="Simple text-indent">
  <span>See the Pen <a href="https://codepen.io/bradleytaunt/pen/OGXLEd/">
  Simple text-indent</a> by Bradley Taunt (<a href="https://codepen.io/bradleytaunt">@bradleytaunt</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
