---
layout: post
title: "TypeTip 03: First letter pseudo element"
description: Set specific styling for the first letter of a text element with CSS
summary: Set specific styling for the first letter of a text element with this handy and fully supported CSS pseudo element.
tags: 
    - design
    - typetips
---

In today's TypeTip&trade; we will be taking a look at the often overlooked `:first-letter` CSS pseudo element. Though you might only use this for specific article-format web pages, it's still a nice-to-have in your web dev toolset.

## The HTML

Like most pseudo elements, nothing has to change with your pre-existing HTML structure:

```html
<article>
    <p>It was a bright cold day in April, and the clocks were striking thirteen.</p>
</article>
```

## The CSS

Here's where the magic happens:

```css
p:first-letter {
    color: orangered;
    font-size: 250%;
}
```

## Live CodePen

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="result" data-user="bradleytaunt" data-slug-hash="gJYbev" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="First Letter Pseudo Element">
  <span>See the Pen <a href="https://codepen.io/bradleytaunt/pen/gJYbev/">
  First Letter Pseudo Element</a> by Bradley Taunt (<a href="https://codepen.io/bradleytaunt">@bradleytaunt</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

