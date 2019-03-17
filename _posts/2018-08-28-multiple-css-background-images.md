---
layout: post
title: Using multiple CSS background images
description: Set multiple background images on an element in CSS
summary: Somewhat unknown in the CSS community is the ability to have multiple background images set on an element.
tags:
    - css
    - design
---

It isn't something developers have a need to do very often, but you *can* set multiple background images on a single element.

Example:

```css
.element {
    background: url('image_path') center repeat, linear-gradient(transparent 0%, #000 100%) no-repeat;
}
```

What can you do with this? It's only limited by your imagination, but I'm personally a fan of always using as few elements as possible when working on a project.