---
layout: post
title: Better box-shadows
description: Creating better box-shadows with simple CSS and pseudo elements
summary: Further improving on the default browser box-shadow styling with a little help from well-placed pseudo elements.
tags:
  - css
  - design
---

<style>
  .box-container,
  .box-container-depth {
    background: white;
    box-shadow: 0 4px 8px rgba(0,0,0,0.3);
    border: 1px solid #eee;
    border-radius: 10px;
    margin: 2rem auto;
    padding: 10px;
    position: relative;
    height: 200px;
    width: 250px;
  }
  .box-container-depth { box-shadow: none; }
  .box-container-depth-inner {
    bottom: 0;
    box-shadow: 0 4px 12px rgba(0,0,0,0.3);
    position: absolute;
    width: 94%;
    height: 94%;
    left: 3%;
    z-index: -1;
  }
  .blur { filter: blur(6px); }
</style>

Box shadow on <abbr title="hypertext markup language">HTML</abbr> elements has been widely supported across most browsers for a while now, but I find the default options don't allow for much visual manipulation of the shadows in general.

Let's take a look at a default configuration of `box-shadow`:

```css
.box-container {
  box-shadow: 0 4px 8px rgba(0,0,0,0.3);
}
```

In the example above the first property number is the origin of the *x-axis*, the second number is the origin of the *y-axis* and the third is the amount of *blur*.

We should also add some minimal styling to cleanup the `.box-container` a little bit for our example:

```html
<div class="box-container"></div>
```

```css
.box-container {
  box-shadow: 0 4px 8px rgba(0,0,0,0.3);

  /* Styles to make it less ugly */
  background: white;
  border-radius: 10px;
  border: 1px solid #eee;
  height: 200px;
  padding: 10px;
  position: relative;
  width: 250px;
}
```

Which would render as this:

<div class="box-container"></div>

Not bad - but we can do a lot better than this.

## Please sir, I want some more (depth)

We just need to add a simple child `div` inside our main element we want to apply the shadow to:

```html
<div class="box-container">
  <div class="box-container-inner"></div>
</div>
```

Now we make our inner child element `absolute` and set it's `height` and `width` dynamically to be slightly smaller than it's parent (percentages work best for this). Remember to set this child element behind it's parent by adding `z-index: -1`.

```css
.box-container {
  /* No box-shadow needed on this element anymore */
  /* Styles to make it less ugly */
  background: white;
  border-radius: 10px;
  border: 1px solid #eee;
  height: 200px;
  padding: 10px;
  position: relative;
  width: 250px;
}

.box-container-inner {
  bottom: 0;
  /* The box-shadow is added here now */
  box-shadow: 0 4px 12px rgba(0,0,0,0.3);
  height: 94%;
  left: 3%;
  position: absolute;
  width: 94%;
  z-index: -1;
}
```

Which will make the drop-shadow render with a little more realistic depth:

<div class="box-container-depth">
  <div class="box-container-depth-inner"></div>
</div>

## But wait - there's more!

We could stop now and have a decent drop-shadow that is certainly easier on the eyes - but we can make this even better with one extra property - `filter:blur();`. 

So your final code would look like this:

```css
.box-container {
  /* Styles to make it less ugly */
  background: white;
  border-radius: 10px;
  border: 1px solid #eee;
  height: 200px;
  padding: 10px;
  position: relative;
  width: 250px;
}

.box-container-inner {
  bottom: 0;
  box-shadow: 0 4px 12px rgba(0,0,0,0.3);
  filter: blur(6px);
  height: 94%;
  left: 3%;
  position: absolute;
  width: 94%;
  z-index: -1;
}
```

Which renders out into a much smoother blend of a drop-shadow, creating a more realistic illusion of depth:

<div class="box-container-depth">
  <div class="box-container-depth-inner blur"></div>
</div>
