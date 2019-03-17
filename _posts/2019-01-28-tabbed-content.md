---
layout: post
title: Tabbed content without JavaScript
description: Quick demo on how build tabular content sections with only CSS
summary: Learn how to implement tabbed navigation content without the need to use plugins or any kind of JavaScript.
tags:
    - css
    - javascript
---

<style>
    .tab-container {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
        margin: 0 auto;
        width: 100%;
    }
    .tabs {
        height: 100%;
        min-height: 250px;
        position: relative;
    }
    .tab-item {
        display: inline;
    }
    .tab-input {
        position: absolute;
        visibility: hidden;
    }
    .tab-label {
        background: white;
        box-shadow: inset 0 -4px 4px rgba(0,0,0,0.02);
        color: lightgrey;
        cursor: pointer;
        display: inline-block;
        font-weight: 600;
        margin: 0 5px 0 0;
        padding: 10px 20px;
        position: relative;
        text-align: center;
        z-index: 0;
    }
    .tab-content {
        background: white;
        bottom: 0;
        box-shadow: 0 6px 8px rgba(0,0,0,0.02);
        left: 0;
        overflow: scroll;
        padding: 20px;
        position: absolute;
        right: 0;
        top: 50px;
        z-index: 0;
    }
    .tab-input:checked + .tab-label {
        border: 1px solid #eee;
        border-bottom: 0;
        box-shadow: 0 -6px 8px rgba(0,0,0,0.02);
        color: #268bd2;
        z-index: 2;
    }
    .tab-input:checked ~ .tab-content {
        border: 1px solid #eee;
        z-index: 1;
    }
    @media(max-width:38em) {
        .tab-label {
            display: block;
            width: 100%;
        }
        .tab-content {
            display: none;
        }
        .tab-input:checked ~ .tab-content {
            bottom: auto;
            display: block;
            position: relative;
            top: auto;
        }
    }
</style>

Creating tabs is a fairly trivial and common practice in web design, but many times it requires JavaScript to properly implement. Fortunately it *is* possible to create tabbed content with only using CSS.

<h3><a href="#demo">View live demo</a></h3>

---

<div class="message">
<p><strong>Sidenote:</strong></p>
<p>While this method is semantic and accessible, you might consider using a pre-existing plugin for tabbed data.</p> 
<p>This component tends to feel a little "stiff" compared to more fleshed out variations available. This pure CSS version is better suited as a fallback for when users have disabled JavaScript.</p>
</div>

<h2 id="demo">The final product (embedded demo)</h2>

This is what we will be building:

<div class="message">
<div class="tab-container">
    <div class="tabs">
        <div class="tab-item">
            <input class="tab-input" type="radio" name="tabs" id="tab-1" checked>
            <label class="tab-label" for="tab-1">Tab 1</label>
            <div class="tab-content">
                <p>You really think you can fly that thing? Yes, Yes, without the oops! You're a very talented young man, with your own clever thoughts and ideas. Do you need a manager? Life finds a way. Life finds a way. Eventually, you do plan to have dinosaurs on your dinosaur tour, right?</p>
            </div>
        </div>
        <div class="tab-item">
            <input class="tab-input" type="radio" name="tabs" id="tab-2">
            <label class="tab-label" for="tab-2">Tab 2</label>
            <div class="tab-content">
                <p>God creates dinosaurs. God destroys dinosaurs. God creates Man. Man destroys God. Man creates Dinosaurs. Checkmate... Is this my espresso machine? Wh-what is-h-how did you get my espresso machine?</p>
                <p>So you two dig up, dig up dinosaurs? Remind me to thank John for a lovely weekend.</p>
            </div>
        </div>
        <div class="tab-item">
            <input class="tab-input" type="radio" name="tabs" id="tab-3">
            <label class="tab-label" for="tab-3">Tab 3</label>
            <div class="tab-content">
                <p>Yeah, but John, if The Pirates of the Caribbean breaks down, the pirates don’t eat the tourists. Jaguar shark! So tell me - does it really exist? I gave it a cold? I gave it a virus. A computer virus. Yeah, but your scientists were so preoccupied with whether or not they could, they didn't stop to think if they should.</p>
            </div>
        </div>
    </div>
</div>
</div>

## The HTML

The skeleton for this component is fairly basic - we just need the following structure:

1. Parent element for each tab item
2. Default radio input
3. Label linked to corresponding input
4. Inner content associated with each tab item

```html
<!-- Simple main container for all elements -->
<div class="tabs">

    <!-- Parent container holding for individual tab item -->
    <div class="tab-item">

        <!-- Default radio input -->
        <input class="tab-input" type="radio" name="tabs" id="tab-1">

        <!-- Label connected to radio input via `id` and `for` attributes -->
        <label class="tab-label" for="tab-1">Tab 1</label>

        <!-- Full inner content of current tab item -->
        <div class="tab-content">Content goes here</div>

    </div>

</div>
```

Full HTML for reference:

```html
<div class="tabs">

    <div class="tab-item">
        <input class="tab-input" type="radio" name="tabs" id="tab-1">
        <label class="tab-label" for="tab-1">Tab 1</label>
        <div class="tab-content">Content goes here</div>
    </div>

    <div class="tab-item">
        <input class="tab-input" type="radio" name="tabs" id="tab-2">
        <label class="tab-label" for="tab-2">Tab 2</label>
        <div class="tab-content">Content goes here</div>
    </div>

    <div class="tab-item">
        <input class="tab-input" type="radio" name="tabs" id="tab-3">
        <label class="tab-label" for="tab-3">Tab 3</label>
        <div class="tab-content">Content goes here</div>
    </div>

</div>
```

## The CSS

First, we need to set each `input`, `label` and inner content into their own parent containers:

```css
/* Main parent that holds all contents */
.tabs {
    height: 100%;
    min-height: 250px;
    position: relative;
}

/* Each tab items (includes heading & content) */
.tab-item {
    display: inline;
}
```

Next, we will hide the default `radio` input and design our labels to resemble a basic web tab element. The `z-index` property on the label is important for how we will be stacking our content on the z-axis (labels above inner content for example).

```css
/* Hide the default radio inputs */
.tab-input {
    position: absolute;
    visibility: hidden;
}

/* The main tab headings */
.tab-label {
    background: white;
    box-shadow: inset 0 -4px 4px rgba(0,0,0,0.02);
    color: lightgrey;
    cursor: pointer;
    display: inline-block;
    font-weight: 600;
    margin: 0 5px 0 0;
    padding: 10px 20px;
    position: relative;
    text-align: center;
    z-index: 0;
}
```

The main inner content of each tab needs to have an `absolute` position set as it's default, since the one currently selected will switch to `relative` on mobile (more on that in a moment):

```css
/* The inner tab content */
.tab-content {
    background: white;
    bottom: 0;
    box-shadow: 0 6px 8px rgba(0,0,0,0.02);
    left: 0;
    overflow: scroll;
    padding: 20px;
    position: absolute;
    right: 0;
    top: 50px;
    z-index: 0;
}
```

The final step is just telling the browser to style both the `label` and inner content of the currently selected radio `input`:

```css
/* Style the currently selected tab label */
.tab-input:checked + .tab-label {
    border: 1px solid #eee;
    border-bottom: 0;
    box-shadow: 0 -6px 8px rgba(0,0,0,0.02);
    color: #268bd2;
    z-index: 2;
}

/* Show the currently selected tab content */
.tab-input:checked ~ .tab-content {
    border: 1px solid #eee;
    z-index: 1;
}
```

It's as simple as that! For reference, here is the entire CSS file for easier access:

```css
/* Main parent that holds all contents */
.tabs {
    height: 100%;
    min-height: 250px;
    position: relative;
}

/* Each tab items (includes heading & content) */
.tab-item {
    display: inline;
}

/* Hide the default radio inputs */
.tab-input {
    position: absolute;
    visibility: hidden;
}

/* The main tab headings */
.tab-label {
    background: white;
    box-shadow: inset 0 -4px 4px rgba(0,0,0,0.02);
    color: lightgrey;
    cursor: pointer;
    display: inline-block;
    font-weight: 600;
    margin: 0 5px 0 0;
    padding: 10px 20px;
    position: relative;
    text-align: center;
    z-index: 0;
}

/* The inner tab content */
.tab-content {
    background: white;
    bottom: 0;
    box-shadow: 0 6px 8px rgba(0,0,0,0.02);
    left: 0;
    overflow: scroll;
    padding: 20px;
    position: absolute;
    right: 0;
    top: 50px;
    z-index: 0;
}

/* Style the currently selected tab label */
.tab-input:checked + .tab-label {
    border: 1px solid #eee;
    border-bottom: 0;
    box-shadow: 0 -6px 8px rgba(0,0,0,0.02);
    color: #268bd2;
    z-index: 2;
}

/* Show the currently selected tab content */
.tab-input:checked ~ .tab-content {
    border: 1px solid #eee;
    z-index: 1;
}
```

## Don't forget about mobile

With only a few extra lines of CSS we can ensure that our custom tabs will stack on top of each other and look solid on mobile devices:

```css
@media(max-width:38em) {
    .tab-label {
        display: block;
        width: 100%;
    }
    .tab-content {
        display: none;
    }
    .tab-input:checked ~ .tab-content {
        bottom: auto;
        display: block;
        position: relative;
        top: auto;
    }
}
```

## One minor caveat

Even though I'm a pretty big fan of implementing tabs this way, there is a small drawback:

The `height` of the inner content doesn't grow dynamically since it defaults as `absolute`, so a `min-height` or `height` value is required on the parent element. This could become a problem in certain situations where you don't have the luxury of setting a static height.

Other than that, enjoy building some JavaScript-free tabs!
