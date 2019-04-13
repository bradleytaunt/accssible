---
layout: post
title: "CSS value: currentColor"
description: Taking a look at the very overlooked currentColor CSS value type
summary: Taking a look at how to best use the very overlooked currentColor CSS value type in your projects.
tags: 
    - design
    - css
---

There are a large number of nuanced and mostly unheard of CSS value types, but today we are going to focus on `currentColor`. So what is the `currentColor` value type anyway?

> The currentColor value type will apply the existing color value to other properties like background-color, etc.

## See it in action

Let's assume with have a single div with the following properties:

```css
div {
    color: dodgerblue;
}
```

If we wanted to use that same color for other properties on elements inside that initial `div`, it's simple - we just need to call `currentColor` like so:

```css
div {
    color: dodgerblue;
}

div header {
    background-color: currentColor;
}

div a {
    border-bottom: 1px solid currentColor;
}
```

**Sidenote**: If you re-declare the default `color` property further along in your CSS, the `currentColor` value will update according to the last color set.

And that's it. Best of all, this value type is supported across all major browsers!