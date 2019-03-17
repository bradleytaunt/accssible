---
layout: post
title: Animated card tiles
description: Implement animated card tiles with pure CSS
summary: In this tutorial we explain step-by-step how to build out tiled cards that animate with user interaction using pure CSS.
tags:
    - html
    - css
    - design
---

<style>
    .card-tiles-container {
        display: flex;
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
        font-size: 14px;
        margin: 20px 0;
    }

    /* Shared transitions */
    .card-tile,
    .card-tile .text-content {
        transition: .3s ease all;
    }

    /* Default card tile styles */
    .card-tile {
        border: 1px solid;
        border-radius: 10px;
        cursor: pointer;
        height: 150px;
        margin: 0 10px;
        overflow: hidden;
        position: relative;
        width: 33.33%;
    }

    /* Blue Card */
    .card-tile.blue {
        background-color: #0093E9;
        background-image: linear-gradient(0deg, #0093E9 0%, #80D0C7 100%);
        border-color: #0093E9;
        box-shadow: 0 4px 12px rgba(128,208,199,0.7), inset 0 2px 1px rgba(255,255,255,0.6);
    }
    .card-tile.blue:hover {
        box-shadow: 0 8px 18px rgba(128,208,199,0.4), inset 0 2px 1px rgba(255,255,255,0.6);
    }

    /* Orange Card */
    .card-tile.orange {
        background-color: #FAD961;
        background-image: linear-gradient(180deg, #FAD961 0%, #F76B1C 100%);
        border-color: #F76B1C;
        box-shadow: 0 4px 12px rgba(247,107,28,0.7), inset 0 2px 1px rgba(255,255,255,0.6);
    }
    .card-tile.orange:hover {
        box-shadow: 0 8px 18px rgba(247,107,28,0.4), inset 0 2px 1px rgba(255,255,255,0.6);
    }

    /* Green Card */
    .card-tile.green {
        background-color: #096e40;
        background-image: linear-gradient(0deg, #096e40 0%, #2AF598 100%);
        border-color: #096e40;
        box-shadow: 0 4px 12px rgba(9,110,64,0.7), inset 0 2px 1px rgba(255,255,255,0.6);
    }
    .card-tile.green:hover {
        box-shadow: 0 8px 18px rgba(9,110,64,0.4), inset 0 2px 1px rgba(255,255,255,0.6);
    }



    /* Card tile text content */
    .card-tile .text-content {
        background: linear-gradient(rgba(0,0,0,0.4) 0%, rgba(0,0,0,0.6) 100%);
        bottom: 10px;
        border: 1px solid rgba(0,0,0,0.4);
        border-radius: 5px;
        box-shadow: inset 0 1px 1px rgba(255,255,255,0.8), 0 2px 4px rgba(0,0,0,0.5);
        height: 65px;
        left: 10px;
        opacity: 0;
        padding: 10px;
        position: absolute;
        width: calc(100% - 20px);
        z-index: -1;
    }
    .card-tile .text-content h4,
    .card-tile .text-content p {
        color: #fff;
        margin: 0;
        text-shadow: 1px 1px 1px rgba(0,0,0,0.6);
    }

    /* All animations on hover */
    .card-tile:hover {
        transform: scale(1.1);
    }
    .card-tile:hover .text-content {
        opacity: 1;
        z-index: 1;
    }

    @media(max-width: 600px) {
        .card-tiles-container {
            flex-direction: column;
        }
        .card-tile {
            margin: 0 0 10px 0;
            width: 100%;
        }
    }
</style>

The design trend of using "cards" or "tiles" to display interactive sections/article headings in an app or website remains a popular choice among designers. So, let's build a set of animated cards with only HTML &amp; CSS. 

## What we will be building (live demo)

This is the set of animated card tiles we will be creating:<br> 
*(try hovering)*

<div class="message">
    <div class="card-tiles-container">
        <div class="card-tile blue">
            <div class="text-content">
                <h4>Card Title</h4>
                <p>Inner card content text</p>
            </div>
        </div>
        <div class="card-tile orange">
            <div class="text-content">
                <h4>Card Title</h4>
                <p>Inner card content text</p>
            </div>
        </div>
        <div class="card-tile green">
            <div class="text-content">
                <h4>Card Title</h4>
                <p>Inner card content text</p>
            </div>
        </div>
    </div>
</div>

## The HTML

For the base skeleton of these cards we only need:

- a `flexbox` main container to hold everything
- a `.card-tile` parent element
- the inner child element that will display on `:hover`
- proper `h4` and `p` tags inside that child element

```html
<!-- Flexbox parent container -->
<div class="card-tiles-container">

    <!-- Parent container -->
    <div class="card-tile">

        <!-- Inner child text content -->
        <div class="text-content">

            <!-- Proper tags for accessibility -->
            <h4>Card Title</h4>
            <p>Inner card content text</p>

        </div>

    </div>

</div>
```

That's all that is needed - for now. We will be returning to this code shortly to add some extra classes to make our lives easier.

## The CSS

First we set the main housing container to use `flex` so we save ourselves the headache of aligning all the cards in a nice row:

```css
.card-tiles-container {
    display: flex;
    font-size: 14px;
    margin: 20px 0;
}
```

Next we create the default styling for our tile cards and set the `transform` property to scale the card on `:hover`:

```css
/* Default card tile styles */
.card-tile {
    border: 1px solid;
    border-radius: 10px;
    cursor: pointer;
    height: 150px;
    margin: 0 10px;
    overflow: hidden;
    position: relative;
    width: 33.33%;
}
.card-tile:hover {
    transform: scale(1.1);
}
```

### Where are my cards?!

Don't panic if you can't *visually* see any card elements in your demo yet - that's to be expected. We will be  styling these card elements momentarily.

Our next step is to hide the default inner `text-content` and only show it on hover. We achieve this by setting it's position to `absolute`, placing it's opacity at 0 and pushing it's z-index back to -1.

When the user hovers over a main card tile, we change the `text-content` values of both the opacity and z-index to 1.

```css
/* Card tile text content */
.card-tile .text-content {
    background: linear-gradient(rgba(0,0,0,0.4) 0%, rgba(0,0,0,0.6) 100%);
    bottom: 10px;
    border: 1px solid rgba(0,0,0,0.4);
    border-radius: 5px;
    box-shadow: inset 0 1px 1px rgba(255,255,255,0.8), 
                0 2px 4px rgba(0,0,0,0.5);
    height: 65px;
    left: 10px;
    opacity: 0;
    padding: 10px;
    position: absolute;
    width: calc(100% - 20px);
    z-index: -1;
}
.card-tile:hover .text-content {
    opacity: 1;
    z-index: 1;
}
```

Finally we add some minor styling for the inner header and paragraph tags:

```css
.card-tile .text-content h4,
.card-tile .text-content p {
    color: #fff;
    margin: 0;
    text-shadow: 1px 1px 1px rgba(0,0,0,0.6);
}
```

### Don't forget mobile

We want out UI to stack the cards if users are viewing them on smaller devices:

```css
@media(max-width: 600px) {
    .card-tiles-container {
        flex-direction: column;
    }
    .card-tile {
        margin: 0 0 10px 0;
        width: 100%;
    }
}
```

## Customizing each card

Remember how I mentioned that we would be adding more classes to the original HTML? Now is the time. We will be including a simple class on each card tile to provide it's own custom coloring:

```html
<div class="card-tiles-container">
    <!-- `Blue` class -->
    <div class="card-tile blue">
        <div class="text-content">
            <h4>Card Title</h4>
            <p>Inner card content text</p>
        </div>
    </div>
    <!-- `Orange` class -->
    <div class="card-tile orange">
        <div class="text-content">
            <h4>Card Title</h4>
            <p>Inner card content text</p>
        </div>
    </div>
    <!-- `Green` class -->
    <div class="card-tile green">
        <div class="text-content">
            <h4>Card Title</h4>
            <p>Inner card content text</p>
        </div>
    </div>
</div>
```

And these color classes correlate to some new CSS styling:

```css
/* Blue Card */
.card-tile.blue {
    background-color: #0093E9;
    background-image: linear-gradient(0deg, #0093E9 0%, #80D0C7 100%);
    border-color: #0093E9;
    box-shadow: 0 4px 12px rgba(128,208,199,0.7), 
                inset 0 2px 1px rgba(255,255,255,0.6);
}
.card-tile.blue:hover {
    box-shadow: 0 8px 18px rgba(128,208,199,0.4), 
                inset 0 2px 1px rgba(255,255,255,0.6);
}

/* Orange Card */
.card-tile.orange {
    background-color: #FAD961;
    background-image: linear-gradient(180deg, #FAD961 0%, #F76B1C 100%);
    border-color: #F76B1C;
    box-shadow: 0 4px 12px rgba(247,107,28,0.7), 
                inset 0 2px 1px rgba(255,255,255,0.6);
}
.card-tile.orange:hover {
    box-shadow: 0 8px 18px rgba(247,107,28,0.4), 
                inset 0 2px 1px rgba(255,255,255,0.6);
}

/* Green Card */
.card-tile.green {
    background-color: #096e40;
    background-image: linear-gradient(0deg, #096e40 0%, #2AF598 100%);
    border-color: #096e40;
    box-shadow: 0 4px 12px rgba(9,110,64,0.7), 
                inset 0 2px 1px rgba(255,255,255,0.6);
}
.card-tile.green:hover {
    box-shadow: 0 8px 18px rgba(9,110,64,0.4), 
                inset 0 2px 1px rgba(255,255,255,0.6);
}
```

### Adding transitions

We can now see the actual cards visually and have the ability to interact with them, but there is a problem - they don't animate.

Lucky we can target all elements we wish to animate with the `transition` property, like so:

```css
/* Shared transitions */
.card-tile,
.card-tile .text-content {
    transition: .3s ease all;
}
```

Done and done.

## The final code

To make things easier for reference, I have included all the `html` and `css` below. Please feel free to use these cards anywhere you like and change them as you see fit!

### HTML

```html
<div class="card-tiles-container">
    <div class="card-tile blue">
        <div class="text-content">
            <h4>Card Title</h4>
            <p>Inner card content text</p>
        </div>
    </div>
    <div class="card-tile orange">
        <div class="text-content">
            <h4>Card Title</h4>
            <p>Inner card content text</p>
        </div>
    </div>
    <div class="card-tile green">
        <div class="text-content">
            <h4>Card Title</h4>
            <p>Inner card content text</p>
        </div>
    </div>
</div>
```

### CSS

```css
.card-tiles-container {
    display: flex;
    font-size: 14px;
    margin: 20px 0;
}

/* Shared transitions */
.card-tile,
.card-tile .text-content {
    transition: .3s ease all;
}

/* Default card tile styles */
.card-tile {
    border: 1px solid;
    border-radius: 10px;
    cursor: pointer;
    height: 150px;
    margin: 0 10px;
    overflow: hidden;
    position: relative;
    width: 33.33%;
}

/* Blue Card */
.card-tile.blue {
    background-color: #0093E9;
    background-image: linear-gradient(0deg, #0093E9 0%, #80D0C7 100%);
    border-color: #0093E9;
    box-shadow: 0 4px 12px rgba(128,208,199,0.7),
                inset 0 2px 1px rgba(255,255,255,0.6);
}
.card-tile.blue:hover {
    box-shadow: 0 8px 18px rgba(128,208,199,0.4), 
                inset 0 2px 1px rgba(255,255,255,0.6);
}

/* Orange Card */
.card-tile.orange {
    background-color: #FAD961;
    background-image: linear-gradient(180deg, #FAD961 0%, #F76B1C 100%);
    border-color: #F76B1C;
    box-shadow: 0 4px 12px rgba(247,107,28,0.7), 
                inset 0 2px 1px rgba(255,255,255,0.6);
}
.card-tile.orange:hover {
    box-shadow: 0 8px 18px rgba(247,107,28,0.4), 
                inset 0 2px 1px rgba(255,255,255,0.6);
}

/* Green Card */
.card-tile.green {
    background-color: #096e40;
    background-image: linear-gradient(0deg, #096e40 0%, #2AF598 100%);
    border-color: #096e40;
    box-shadow: 0 4px 12px rgba(9,110,64,0.7), 
                inset 0 2px 1px rgba(255,255,255,0.6);
}
.card-tile.green:hover {
    box-shadow: 0 8px 18px rgba(9,110,64,0.4), 
                inset 0 2px 1px rgba(255,255,255,0.6);
}



/* Card tile text content */
.card-tile .text-content {
    background: linear-gradient(rgba(0,0,0,0.4) 0%, rgba(0,0,0,0.6) 100%);
    bottom: 10px;
    border: 1px solid rgba(0,0,0,0.4);
    border-radius: 5px;
    box-shadow: inset 0 1px 1px rgba(255,255,255,0.8), 
                0 2px 4px rgba(0,0,0,0.5);
    height: 65px;
    left: 10px;
    opacity: 0;
    padding: 10px;
    position: absolute;
    width: calc(100% - 20px);
    z-index: -1;
}
.card-tile .text-content h4,
.card-tile .text-content p {
    color: #fff;
    margin: 0;
    text-shadow: 1px 1px 1px rgba(0,0,0,0.6);
}

/* All animations on hover */
.card-tile:hover {
    transform: scale(1.1);
}
.card-tile:hover .text-content {
    opacity: 1;
    z-index: 1;
}

@media(max-width: 600px) {
    .card-tiles-container {
        flex-direction: column;
    }
    .card-tile {
        margin: 0 0 10px 0;
        width: 100%;
    }
}
```

# ✌️
