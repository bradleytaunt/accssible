---
layout: post
title: "TypeTip 02: Character unit"
description: Set the length of text elements by using the helpful character unit CSS attribute
summary: Set the minimum or maximum length of text elements by using the helpful character unit CSS attribute.
tags: 
    - design
    - typetips
---

When it comes to proper readability with large portions of text, the golden standard is to have no more than [75 characters per line](http://webtypography.net/2.1.2). This is easy to achieve in the world of print but on the responsive, ever-changing web - statically defined typography becomes a little more difficult.

You could go through the long process of setting up media queries for every possible screen size, adjusting text size and padding accordingly - but there is a *better way*.

## Introducing character units

By setting your main containers or text elements with the CSS character unit (`ch`), you need to set the character length only once. Let's look at a simple example for reference.

Let's say you have an article which will fill the entire length of the screen. Something like this:

```html
<div class="container">
    <p>Reprehenderit aliqua in quis eiusmod ea culpa aliquip. Velit duis est irure voluptate occaecat labore laborum ut pariatur ex veniam deserunt esse est. Esse sunt exercitation id reprehenderit deserunt elit commodo sit ullamco amet commodo magna consequat. Excepteur voluptate tempor consectetur eu aliqua aliquip laboris aliquip veniam excepteur labore.</p>
    <p>Voluptate excepteur sint magna ipsum occaecat irure sit. In occaecat excepteur in id ullamco id est incididunt irure et. Consectetur veniam exercitation occaecat exercitation labore nulla excepteur irure ex anim. Commodo sint anim non ad excepteur exercitation eiusmod Lorem nisi. Tempor ut ipsum do adipisicing dolore.</p>
</div>
```

With this structure, you might normally set the default `max-width` property with your desired maximum width (whatever you believe is the best reading length):

```css
.container {
    max-width: 38em;
}
```

This works - but it isn't ideal. Time for character units to save the day! You will still target the `max-width` property but this time we set it to use the `ch` value like so:

```css
.container {
    max-width: 66ch;
}
```

This setting makes sure content will not exceed more than 66 characters per line, making for a better reading experience with little effort.

## Browser support

The character unit attribute has pretty great support - even partial IE11! Check out the supported browsers [here](https://caniuse.com/#feat=ch-unit).