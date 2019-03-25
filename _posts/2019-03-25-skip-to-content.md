---
layout: post
title: Skip to content button
description: Improve your site's accessibility by including a skip to content button
summary: A quick demo on how to improve your site's overall accessibility by including a skip to content button.
tags: 
    - design
    - accessibility
---

One of the golden rules for testing your website's accessibility is the "keyboard-only" audit. This is where you test navigating through your entire site without the use of a mouse, but instead rely solely on tabbing through your content.

Unfortunately, one item is normally overlooked during this audit - a "skip to content" context button. Including a "skip to content" navigation item in your project is extremely useful because:

- speeds up user interaction with the content you **want** them to see
- on subsequent pages the user shouldn't need to tab through the entire navigation each time

If you would like to see a live "skip to content" button in action, simply tab through this site with your keyboard.

## The HTML

For the sake of this demo we will assume that we currently have the following navigation setup in our project:

```html
<nav role="navigation">
    <a href="/">Home</a>
    <a href="/about">About</a>
    <a href="/archive">Archive</a>
    <a href="/atom.xml">RSS</a>
</nav>
```

Now for the easy part - adding our simple content skip link with it's own custom `skip-content` class:

```html
<nav role="navigation">
    <!-- Skip to content button -->
    <a class="skip-content" href="#main">Skip to Content (Press Enter)</a>
    <a href="/">Home</a>
    <a href="/about">About</a>
    <a href="/archive">Archive</a>
    <a href="/atom.xml">RSS</a>
</nav>
```
<div class="message">
    <strong>Sidenote:</strong> in this demo we are making the assumption that the main content block has an <code>id</code> of "main" associated with it. Hence the skip content button linking to <code>#main</code>.
</div>

## The CSS

Our first task is to make sure this new link isn't visible or interactive by default unless the user explicitly tabs through the navigation. We do so my positioning the link outside of the main content view. It is important to use this `absolute` position style instead of setting the display property to `none`, since the display property technique will fully remove the element from the DOM (bad accessibility practices).

```css
a.skip-content {
    background: grey;
    color: white;
    left: -9999px;
    padding: 0.5rem;
    position: absolute;
    top: 0;
}
```

### Almost there

Now we just re-position the element when the user focuses on the link with a keyboard tab:

```css
a.skip-content:focus {
    left: 1rem; /* Whatever desired position */
}
```

## See it in action

As I stated before, simply tab through this current site to see the "skip to content" button appear.

This is a very basic accessibility win you can implement in your current projects with next to zero effort. Enjoy!