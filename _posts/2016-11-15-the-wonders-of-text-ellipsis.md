---
layout: post
title: The wonders of text ellipsis
description: Learn how to use text ellipsis effectively in your projects
summary: The text ellipsis CSS property can be extremely useful for keeping your content contained without the use of ugly fixed widths or heights.
tags:
    - css
    - design
---

A common issue when working with constrained UI elements is text overflowing outside of it's parent or breaking into addition lines (thus breaking the layout).

This is most commonly seen with the direct and placeholder values for input fields on form elements. For example, the following input placeholder will be cutoff from the user's view:

<p data-height="265" data-theme-id="0" data-slug-hash="OgpzyY" data-default-tab="html,result" data-user="bradleytaunt" data-embed-version="2" data-pen-title="Text Ellipsis (Input Placeholders)" class="codepen">See the Pen <a href="https://codepen.io/bradleytaunt/pen/OgpzyY/">Text Ellipsis (Input Placeholders)</a> by Bradley Taunt (<a href="https://codepen.io/bradleytaunt">@bradleytaunt</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

Luckily, 3 simple CSS parameters can fix this.

```css
input::placeholder {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

This allows the user to understand there is more content cut out from their current view. It's not ideal to ever have content overflowing outside of the parent container, but if you need to the best workaround is to use text-overflow.
