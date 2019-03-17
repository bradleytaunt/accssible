---
layout: post
title: Easy custom radio inputs
description: Quick demo on how to create custom radio buttons with ease
summary: Let's face it - the default browser styling for radio inputs is terrible. In this article we breakdown how to create beautiful radio options with just CSS.
tags:
    - html
    - css
    - design
---

<style>
    .radio-container {
        margin: 0 auto;
        max-width: 400px;
        width: 100%;
    }
    .radio-label {
        background: white;
        border: 1px solid #eee;
        border-radius: 5px;
        box-shadow: 0 2px 4px rgba(0,0,0,0.05);
        cursor: pointer;
        display: inline-block;
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
        font-weight: 600;
        margin: 0 auto 10px;
        padding: 20px 20px 20px 65px;
        position: relative;
        transition: .3s ease all;
        width: 100%;
    }
    .radio-label:hover {
        box-shadow: 0 4px 8px rgba(0,0,0,0.05);    
    }
    .radio-label:before {
        background: #eee;
        border-radius: 50%;
        content:'';
        height: 30px;
        left: 20px;
        position: absolute;
        top: calc(50% - 15px);
        transition: .3s ease background-color;
        width: 30px;
    }
    .radio-label span {
        -webkit-user-select: none;
        -moz-user-select: none;
        user-select: none;
    }
    .radio-btn {
        position: absolute;
        visibility: hidden;
    }
    .radio-btn:checked + .radio-label {
        background: #ECF5FF;
        border-color: #4A90E2;
    }
    .radio-btn:checked + .radio-label:before {
        background-color: #4A90E2;
        background-image:  url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz48c3ZnIHdpZHRoPSIyNiIgaGVpZ2h0PSIyMCIgdmVyc2lvbj0iMS4xIiB2aWV3Qm94PSIyLjAyOTY4IC00MC4wOTAzIDI2IDIwIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIj48IS0tR2VuZXJhdGVkIGJ5IElKU1ZHIChodHRwczovL2dpdGh1Yi5jb20vaWNvbmphci9JSlNWRyktLT48cGF0aCBkPSJNMjcuOTc0MywtMzYuMTI3MmMwLDAuNDQ2NDI4IC0wLjE1NjI1LDAuODI1ODkzIC0wLjQ2ODc1LDEuMTM4MzlsLTEyLjEyMDUsMTIuMTIwNWwtMi4yNzY3OSwyLjI3Njc5Yy0wLjMxMjUsMC4zMTI1IC0wLjY5MTk2NCwwLjQ2ODc1IC0xLjEzODM5LDAuNDY4NzVjLTAuNDQ2NDI4LDAgLTAuODI1ODkzLC0wLjE1NjI1IC0xLjEzODM5LC0wLjQ2ODc1bC0yLjI3Njc5LC0yLjI3Njc5bC02LjA2MDI3LC02LjA2MDI3Yy0wLjMxMjUsLTAuMzEyNSAtMC40Njg3NSwtMC42OTE5NjUgLTAuNDY4NzUsLTEuMTM4MzljMCwtMC40NDY0MjkgMC4xNTYyNSwtMC44MjU4OTMgMC40Njg3NSwtMS4xMzgzOWwyLjI3Njc5LC0yLjI3Njc5YzAuMzEyNSwtMC4zMTI1IDAuNjkxOTY1LC0wLjQ2ODc1IDEuMTM4MzksLTAuNDY4NzVjMC40NDY0MjksMCAwLjgyNTg5MywwLjE1NjI1IDEuMTM4MzksMC40Njg3NWw0LjkyMTg4LDQuOTM4NjJsMTAuOTgyMSwtMTAuOTk4OWMwLjMxMjUsLTAuMzEyNSAwLjY5MTk2NCwtMC40Njg3NSAxLjEzODM5LC0wLjQ2ODc1YzAuNDQ2NDI4LDAgMC44MjU4OTMsMC4xNTYyNSAxLjEzODM5LDAuNDY4NzVsMi4yNzY3OCwyLjI3Njc5YzAuMzEyNSwwLjMxMjUgMC40Njg3NSwwLjY5MTk2NCAwLjQ2ODc1LDEuMTM4MzlaIiB0cmFuc2Zvcm09InNjYWxlKDEuMDAxOTgpIiBmaWxsPSIjZmZmIj48L3BhdGg+PC9zdmc+');
        background-repeat: no-repeat;
        background-position: center;
        background-size: 15px;
    }
    .radio-btn.positive:checked + .radio-label {
        background: #EAFFF6;
        border-color: #32B67A;
    }
    .radio-btn.positive:checked + .radio-label:before {
        background-color: #32B67A;
    }
    .radio-btn.neutral:checked + .radio-label:before {
        background-image: url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz48c3ZnIHZlcnNpb249IjEuMSIgdmlld0JveD0iMCAtMTUgMzAgOC41NzE0MyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayI+PCEtLUdlbmVyYXRlZCBieSBJSlNWRyAoaHR0cHM6Ly9naXRodWIuY29tL2ljb25qYXIvSUpTVkcpLS0+PHBhdGggZD0iTTMwLC0xMi4zMjE0djMuMjE0MjljMCwwLjczNjYwNyAtMC4yNjIyNzcsMS4zNjcxOSAtMC43ODY4MywxLjg5MTc0Yy0wLjUyNDU1NCwwLjUyNDU1NCAtMS4xNTUxMywwLjc4NjgzMSAtMS44OTE3NCwwLjc4NjgzMWgtMjQuNjQyOWMtMC43MzY2MDcsMCAtMS4zNjcxOSwtMC4yNjIyNzcgLTEuODkxNzQsLTAuNzg2ODMxYy0wLjUyNDU1MywtMC41MjQ1NTMgLTAuNzg2ODMsLTEuMTU1MTMgLTAuNzg2ODMsLTEuODkxNzR2LTMuMjE0MjljMCwtMC43MzY2MDcgMC4yNjIyNzcsLTEuMzY3MTkgMC43ODY4MywtMS44OTE3NGMwLjUyNDU1NCwtMC41MjQ1NTMgMS4xNTUxMywtMC43ODY4MyAxLjg5MTc0LC0wLjc4NjgzaDI0LjY0MjljMC43MzY2MDcsMCAxLjM2NzE5LDAuMjYyMjc3IDEuODkxNzQsMC43ODY4M2MwLjUyNDU1MywwLjUyNDU1NCAwLjc4NjgzLDEuMTU1MTMgMC43ODY4MywxLjg5MTc0WiIgZmlsbD0iI2ZmZiI+PC9wYXRoPjwvc3ZnPg==');
    }
    .radio-btn.negative:checked + .radio-label {
        background: #FFF2F2;
        border-color: #E75153;
    }
    .radio-btn.negative:checked + .radio-label:before {
        background-color: #E75153;
        background-image: url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz48c3ZnIHdpZHRoPSIyMCIgaGVpZ2h0PSIyMCIgdmVyc2lvbj0iMS4xIiB2aWV3Qm94PSIxLjg1MTg1IC0zOS42OTcgMjAgMjAiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiPjwhLS1HZW5lcmF0ZWQgYnkgSUpTVkcgKGh0dHBzOi8vZ2l0aHViLmNvbS9pY29uamFyL0lKU1ZHKS0tPjxwYXRoIGQ9Ik0yMS43Mjk5LC0yMy40NzFjMCwwLjQ0NjQyOCAtMC4xNTYyNSwwLjgyNTg5MyAtMC40Njg3NSwxLjEzODM5bC0yLjI3Njc5LDIuMjc2NzljLTAuMzEyNSwwLjMxMjUgLTAuNjkxOTY0LDAuNDY4NzUgLTEuMTM4MzksMC40Njg3NWMtMC40NDY0MjgsMCAtMC44MjU4OTMsLTAuMTU2MjUgLTEuMTM4MzksLTAuNDY4NzVsLTQuOTIxODcsLTQuOTIxODhsLTQuOTIxODgsNC45MjE4OGMtMC4zMTI1LDAuMzEyNSAtMC42OTE5NjQsMC40Njg3NSAtMS4xMzgzOSwwLjQ2ODc1Yy0wLjQ0NjQyOCwwIC0wLjgyNTg5MiwtMC4xNTYyNSAtMS4xMzgzOSwtMC40Njg3NWwtMi4yNzY3OSwtMi4yNzY3OWMtMC4zMTI1LC0wLjMxMjUgLTAuNDY4NzUsLTAuNjkxOTY1IC0wLjQ2ODc1LC0xLjEzODM5YzAsLTAuNDQ2NDI5IDAuMTU2MjUsLTAuODI1ODkzIDAuNDY4NzUsLTEuMTM4MzlsNC45MjE4OCwtNC45MjE4OGwtNC45MjE4OCwtNC45MjE4OGMtMC4zMTI1LC0wLjMxMjUgLTAuNDY4NzUsLTAuNjkxOTY0IC0wLjQ2ODc1LC0xLjEzODM5YzAsLTAuNDQ2NDI4IDAuMTU2MjUsLTAuODI1ODkzIDAuNDY4NzUsLTEuMTM4MzlsMi4yNzY3OSwtMi4yNzY3OGMwLjMxMjUsLTAuMzEyNSAwLjY5MTk2NCwtMC40Njg3NSAxLjEzODM5LC0wLjQ2ODc1YzAuNDQ2NDI5LDAgMC44MjU4OTMsMC4xNTYyNSAxLjEzODM5LDAuNDY4NzVsNC45MjE4OCw0LjkyMTg4bDQuOTIxODcsLTQuOTIxODhjMC4zMTI1LC0wLjMxMjUgMC42OTE5NjUsLTAuNDY4NzUgMS4xMzgzOSwtMC40Njg3NWMwLjQ0NjQyOSwwIDAuODI1ODkzLDAuMTU2MjUgMS4xMzgzOSwwLjQ2ODc1bDIuMjc2NzksMi4yNzY3OGMwLjMxMjUsMC4zMTI1IDAuNDY4NzUsMC42OTE5NjUgMC40Njg3NSwxLjEzODM5YzAsMC40NDY0MjkgLTAuMTU2MjUsMC44MjU4OTMgLTAuNDY4NzUsMS4xMzgzOWwtNC45MjE4OCw0LjkyMTg4bDQuOTIxODgsNC45MjE4OGMwLjMxMjUsMC4zMTI1IDAuNDY4NzUsMC42OTE5NjQgMC40Njg3NSwxLjEzODM5WiIgdHJhbnNmb3JtPSJzY2FsZSgxLjAwNTYxKSIgZmlsbD0iI2ZmZiI+PC9wYXRoPjwvc3ZnPg==');
    }
</style>

Default radio inputs are notoriously horrible looking and are something designers tend to over-think when trying to customize them. Let's walk through how to create custom radio buttons with *pure CSS*, while still preserving performance and accessibility.

## The final product (embedded demo)

This is what we will be designing:

<div class="message">
<div class="radio-container">
<input class="radio-btn" name="radio-collection" id="radio-1" type="radio">
<label class="radio-label" for="radio-1"><span>I am very satisfied</span></label>

<input class="radio-btn" name="radio-collection" id="radio-2" type="radio" checked>
<label class="radio-label" for="radio-2"><span>I am satisfied</span></label>

<input class="radio-btn" name="radio-collection" id="radio-3" type="radio">
<label class="radio-label" for="radio-3"><span>I am indifferent</span></label>

<input class="radio-btn" name="radio-collection" id="radio-4" type="radio">
<label class="radio-label" for="radio-4"><span>I am unsatisfied</span></label>

<input class="radio-btn" name="radio-collection" id="radio-5" type="radio">
<label class="radio-label" for="radio-5"><span>I am very unsatisfied</span></label>
</div>
</div>

---

## The bones of our radio inputs (HTML)

```html
<input class="radio-btn" name="radio-collection" id="radio-1" type="radio">
<label class="radio-label" for="radio-1"><span>I am very satisfied</span></label>

<input class="radio-btn" name="radio-collection" id="radio-2" type="radio">
<label class="radio-label" for="radio-2"><span>I am satisfied</span></label>

<input class="radio-btn" name="radio-collection" id="radio-3" type="radio">
<label class="radio-label" for="radio-3"><span>I am indifferent</span></label>

<input class="radio-btn" name="radio-collection" id="radio-4" type="radio">
<label class="radio-label" for="radio-4"><span>I am unsatisfied</span></label>

<input class="radio-btn" name="radio-collection" id="radio-5" type="radio">
<label class="radio-label" for="radio-5"><span>I am very unsatisfied</span></label>
```

I know it looks like a lot is going on here, but it's pretty straightforward so let's unpackage line by line:

### Radio inputs

```html
<input class="radio-btn" name="radio-collection" id="radio-1" type="radio">
```

This is the default `radio` input. We give it: 

- a `name` (inputs with a shared `name` are grouped together)
- an `id` (so our label can target this input)
- a `class` (so we can style it later)

**Important**: be sure to have a unique `id` for each input so your labels don't end up connected to multiple radios. In this demo we are simply incrementing them by one.

### Labels

Adding the labels is fairly straightforward, we just include the corresponding input's `id` in the label's `for` attribute. The label content is wrapped in a `span` - which I will explain the reasoning for later.

For styling purposes we also add the `radio-label` class.

```html
<label class="radio-label" for="radio-1"><span>I am very satisfied</span></label>
```

## What we have so far: (embedded demo)

<div class="message">
<div class="radio-container">
<input name="radio-collection-bad" id="radio-10" type="radio">
<label for="radio-10"><span>I am very satisfied</span></label>

<input name="radio-collection-bad" id="radio-20" type="radio">
<label for="radio-20"><span>I am satisfied</span></label>

<input name="radio-collection-bad" id="radio-30" type="radio">
<label for="radio-30"><span>I am indifferent</span></label>

<input name="radio-collection-bad" id="radio-40" type="radio">
<label  for="radio-40"><span>I am unsatisfied</span></label>

<input name="radio-collection-bad" id="radio-50" type="radio">
<label for="radio-50"><span>I am very unsatisfied</span></label>
</div>
</div>

This is looking pretty terrible - but that's nothing some good ol' CSS can't fix!

## The flesh of our radio inputs (CSS)

First we give some basic styling to our `label` and `input` classes (along with hover states). The `radio` element is actually hidden from view, but by using the `visibility` attribute we still keep it accessible for screen-readers.

```css
.radio-label {
    background: white;
    border: 1px solid #eee;
    border-radius: 5px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.05);
    cursor: pointer;
    display: inline-block;
    font-weight: 600;
    margin: 0 auto 10px;
    /* This 65px padding makes room for the custom input */
    padding: 20px 20px 20px 65px;
    position: relative;
    transition: .3s ease all;
    width: 100%;
}
.radio-label:hover {
    box-shadow: 0 4px 8px rgba(0,0,0,0.05);    
}
.radio-btn {
    position: absolute;
    visibility: hidden;
}
```

Remember that `span` element inside the label? We set it's `user-select` property to `none` so we avoid any possible issue with the user selecting the text on-click:

```css
.radio-label span {
    -webkit-user-select: none;
    -moz-user-select: none;
    user-select: none;
}
```

Next we include the default empty selection element (to mimic the original radio input) via a pseudo element:

```css
.radio-label:before {
    background: #eee;
    border-radius: 50%;
    content:'';
    height: 30px;
    left: 20px;
    position: absolute;
    /* Half the height of it's parent minus half of it's own height */
    top: calc(50% - 15px);
    transition: .3s ease background-color;
    width: 30px;
}
```

The final step is adding the custom styling for when an `input` item is selected (`:checked`).

You will notice the use of a `base64` element for the custom checkmark - feel free to subsitute this for an actual image or none at all (this is just my personal design preference).

```css
.radio-btn:checked + .radio-label {
    background: #ECF5FF;
    border-color: #4A90E2;
}
.radio-btn:checked + .radio-label:before {
    background-color: #4A90E2;
    background-image:  url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz48c3ZnIHdpZHRoPSIyNiIgaGVpZ2h0PSIyMCIgdmVyc2lvbj0iMS4xIiB2aWV3Qm94PSIyLjAyOTY4IC00MC4wOTAzIDI2IDIwIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIj48IS0tR2VuZXJhdGVkIGJ5IElKU1ZHIChodHRwczovL2dpdGh1Yi5jb20vaWNvbmphci9JSlNWRyktLT48cGF0aCBkPSJNMjcuOTc0MywtMzYuMTI3MmMwLDAuNDQ2NDI4IC0wLjE1NjI1LDAuODI1ODkzIC0wLjQ2ODc1LDEuMTM4MzlsLTEyLjEyMDUsMTIuMTIwNWwtMi4yNzY3OSwyLjI3Njc5Yy0wLjMxMjUsMC4zMTI1IC0wLjY5MTk2NCwwLjQ2ODc1IC0xLjEzODM5LDAuNDY4NzVjLTAuNDQ2NDI4LDAgLTAuODI1ODkzLC0wLjE1NjI1IC0xLjEzODM5LC0wLjQ2ODc1bC0yLjI3Njc5LC0yLjI3Njc5bC02LjA2MDI3LC02LjA2MDI3Yy0wLjMxMjUsLTAuMzEyNSAtMC40Njg3NSwtMC42OTE5NjUgLTAuNDY4NzUsLTEuMTM4MzljMCwtMC40NDY0MjkgMC4xNTYyNSwtMC44MjU4OTMgMC40Njg3NSwtMS4xMzgzOWwyLjI3Njc5LC0yLjI3Njc5YzAuMzEyNSwtMC4zMTI1IDAuNjkxOTY1LC0wLjQ2ODc1IDEuMTM4MzksLTAuNDY4NzVjMC40NDY0MjksMCAwLjgyNTg5MywwLjE1NjI1IDEuMTM4MzksMC40Njg3NWw0LjkyMTg4LDQuOTM4NjJsMTAuOTgyMSwtMTAuOTk4OWMwLjMxMjUsLTAuMzEyNSAwLjY5MTk2NCwtMC40Njg3NSAxLjEzODM5LC0wLjQ2ODc1YzAuNDQ2NDI4LDAgMC44MjU4OTMsMC4xNTYyNSAxLjEzODM5LDAuNDY4NzVsMi4yNzY3OCwyLjI3Njc5YzAuMzEyNSwwLjMxMjUgMC40Njg3NSwwLjY5MTk2NCAwLjQ2ODc1LDEuMTM4MzlaIiB0cmFuc2Zvcm09InNjYWxlKDEuMDAxOTgpIiBmaWxsPSIjZmZmIj48L3BhdGg+PC9zdmc+');
    background-repeat: no-repeat;
    background-position: center;
    background-size: 15px;
}
```

**And that's it.** 

For easier reference the entire CSS file can be found below:

```css
.radio-label {
    background: white;
    border: 1px solid #eee;
    border-radius: 5px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.05);
    cursor: pointer;
    display: inline-block;
    font-weight: 600;
    margin: 0 auto 10px;
    padding: 20px 20px 20px 65px;
    position: relative;
    transition: .3s ease all;
    width: 100%;
}
.radio-label:hover {
    box-shadow: 0 4px 8px rgba(0,0,0,0.05);    
}
.radio-label:before {
    background: #eee;
    border-radius: 50%;
    content:'';
    height: 30px;
    left: 20px;
    position: absolute;
    top: calc(50% - 15px);
    transition: .3s ease background-color;
    width: 30px;
}
.radio-label span {
    -webkit-user-select: none;
    -moz-user-select: none;
    user-select: none;
}
.radio-btn {
    position: absolute;
    visibility: hidden;
}
.radio-btn:checked + .radio-label {
    background: #ECF5FF;
    border-color: #4A90E2;
}
.radio-btn:checked + .radio-label:before {
    background-color: #4A90E2;
    background-image:  url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz48c3ZnIHdpZHRoPSIyNiIgaGVpZ2h0PSIyMCIgdmVyc2lvbj0iMS4xIiB2aWV3Qm94PSIyLjAyOTY4IC00MC4wOTAzIDI2IDIwIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIj48IS0tR2VuZXJhdGVkIGJ5IElKU1ZHIChodHRwczovL2dpdGh1Yi5jb20vaWNvbmphci9JSlNWRyktLT48cGF0aCBkPSJNMjcuOTc0MywtMzYuMTI3MmMwLDAuNDQ2NDI4IC0wLjE1NjI1LDAuODI1ODkzIC0wLjQ2ODc1LDEuMTM4MzlsLTEyLjEyMDUsMTIuMTIwNWwtMi4yNzY3OSwyLjI3Njc5Yy0wLjMxMjUsMC4zMTI1IC0wLjY5MTk2NCwwLjQ2ODc1IC0xLjEzODM5LDAuNDY4NzVjLTAuNDQ2NDI4LDAgLTAuODI1ODkzLC0wLjE1NjI1IC0xLjEzODM5LC0wLjQ2ODc1bC0yLjI3Njc5LC0yLjI3Njc5bC02LjA2MDI3LC02LjA2MDI3Yy0wLjMxMjUsLTAuMzEyNSAtMC40Njg3NSwtMC42OTE5NjUgLTAuNDY4NzUsLTEuMTM4MzljMCwtMC40NDY0MjkgMC4xNTYyNSwtMC44MjU4OTMgMC40Njg3NSwtMS4xMzgzOWwyLjI3Njc5LC0yLjI3Njc5YzAuMzEyNSwtMC4zMTI1IDAuNjkxOTY1LC0wLjQ2ODc1IDEuMTM4MzksLTAuNDY4NzVjMC40NDY0MjksMCAwLjgyNTg5MywwLjE1NjI1IDEuMTM4MzksMC40Njg3NWw0LjkyMTg4LDQuOTM4NjJsMTAuOTgyMSwtMTAuOTk4OWMwLjMxMjUsLTAuMzEyNSAwLjY5MTk2NCwtMC40Njg3NSAxLjEzODM5LC0wLjQ2ODc1YzAuNDQ2NDI4LDAgMC44MjU4OTMsMC4xNTYyNSAxLjEzODM5LDAuNDY4NzVsMi4yNzY3OCwyLjI3Njc5YzAuMzEyNSwwLjMxMjUgMC40Njg3NSwwLjY5MTk2NCAwLjQ2ODc1LDEuMTM4MzlaIiB0cmFuc2Zvcm09InNjYWxlKDEuMDAxOTgpIiBmaWxsPSIjZmZmIj48L3BhdGg+PC9zdmc+');
    background-repeat: no-repeat;
    background-position: center;
    background-size: 15px;
}
```

---

## But wait - we can get even fancier!

Since this demo is based off a survey-type questionaire, wouldn't it be interesting to give the different selectable options their own styling based on their context? Take a look at the further customized version below:

<div class="message">
<div class="radio-container">
<input class="radio-btn positive" name="radio-collection-survey" id="radio-1-survey" type="radio">
<label class="radio-label" for="radio-1-survey"><span>I am very satisfied</span></label>

<input class="radio-btn positive" name="radio-collection-survey" id="radio-2-survey" type="radio">
<label class="radio-label" for="radio-2-survey"><span>I am satisfied</span></label>

<input class="radio-btn neutral" name="radio-collection-survey" id="radio-3-survey" type="radio" checked>
<label class="radio-label" for="radio-3-survey"><span>I am indifferent</span></label>

<input class="radio-btn negative" name="radio-collection-survey" id="radio-4-survey" type="radio">
<label class="radio-label" for="radio-4-survey"><span>I am unsatisfied</span></label>

<input class="radio-btn negative" name="radio-collection-survey" id="radio-5-survey" type="radio">
<label class="radio-label" for="radio-5-survey"><span>I am very unsatisfied</span></label>
</div>
</div>

We can do so by adding `positive`, `neutral` and `negative` class names to the radio inputs with their own respective properties:

```css
.radio-btn.positive:checked + .radio-label {
    background: #EAFFF6;
    border-color: #32B67A;
}
.radio-btn.positive:checked + .radio-label:before {
    background-color: #32B67A;
}
.radio-btn.neutral:checked + .radio-label:before {
    background-image: url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz48c3ZnIHZlcnNpb249IjEuMSIgdmlld0JveD0iMCAtMTUgMzAgOC41NzE0MyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayI+PCEtLUdlbmVyYXRlZCBieSBJSlNWRyAoaHR0cHM6Ly9naXRodWIuY29tL2ljb25qYXIvSUpTVkcpLS0+PHBhdGggZD0iTTMwLC0xMi4zMjE0djMuMjE0MjljMCwwLjczNjYwNyAtMC4yNjIyNzcsMS4zNjcxOSAtMC43ODY4MywxLjg5MTc0Yy0wLjUyNDU1NCwwLjUyNDU1NCAtMS4xNTUxMywwLjc4NjgzMSAtMS44OTE3NCwwLjc4NjgzMWgtMjQuNjQyOWMtMC43MzY2MDcsMCAtMS4zNjcxOSwtMC4yNjIyNzcgLTEuODkxNzQsLTAuNzg2ODMxYy0wLjUyNDU1MywtMC41MjQ1NTMgLTAuNzg2ODMsLTEuMTU1MTMgLTAuNzg2ODMsLTEuODkxNzR2LTMuMjE0MjljMCwtMC43MzY2MDcgMC4yNjIyNzcsLTEuMzY3MTkgMC43ODY4MywtMS44OTE3NGMwLjUyNDU1NCwtMC41MjQ1NTMgMS4xNTUxMywtMC43ODY4MyAxLjg5MTc0LC0wLjc4NjgzaDI0LjY0MjljMC43MzY2MDcsMCAxLjM2NzE5LDAuMjYyMjc3IDEuODkxNzQsMC43ODY4M2MwLjUyNDU1MywwLjUyNDU1NCAwLjc4NjgzLDEuMTU1MTMgMC43ODY4MywxLjg5MTc0WiIgZmlsbD0iI2ZmZiI+PC9wYXRoPjwvc3ZnPg==');
}
.radio-btn.negative:checked + .radio-label {
    background: #FFF2F2;
    border-color: #E75153;
}
.radio-btn.negative:checked + .radio-label:before {
    background-color: #E75153;
    background-image: url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz48c3ZnIHdpZHRoPSIyMCIgaGVpZ2h0PSIyMCIgdmVyc2lvbj0iMS4xIiB2aWV3Qm94PSIxLjg1MTg1IC0zOS42OTcgMjAgMjAiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiPjwhLS1HZW5lcmF0ZWQgYnkgSUpTVkcgKGh0dHBzOi8vZ2l0aHViLmNvbS9pY29uamFyL0lKU1ZHKS0tPjxwYXRoIGQ9Ik0yMS43Mjk5LC0yMy40NzFjMCwwLjQ0NjQyOCAtMC4xNTYyNSwwLjgyNTg5MyAtMC40Njg3NSwxLjEzODM5bC0yLjI3Njc5LDIuMjc2NzljLTAuMzEyNSwwLjMxMjUgLTAuNjkxOTY0LDAuNDY4NzUgLTEuMTM4MzksMC40Njg3NWMtMC40NDY0MjgsMCAtMC44MjU4OTMsLTAuMTU2MjUgLTEuMTM4MzksLTAuNDY4NzVsLTQuOTIxODcsLTQuOTIxODhsLTQuOTIxODgsNC45MjE4OGMtMC4zMTI1LDAuMzEyNSAtMC42OTE5NjQsMC40Njg3NSAtMS4xMzgzOSwwLjQ2ODc1Yy0wLjQ0NjQyOCwwIC0wLjgyNTg5MiwtMC4xNTYyNSAtMS4xMzgzOSwtMC40Njg3NWwtMi4yNzY3OSwtMi4yNzY3OWMtMC4zMTI1LC0wLjMxMjUgLTAuNDY4NzUsLTAuNjkxOTY1IC0wLjQ2ODc1LC0xLjEzODM5YzAsLTAuNDQ2NDI5IDAuMTU2MjUsLTAuODI1ODkzIDAuNDY4NzUsLTEuMTM4MzlsNC45MjE4OCwtNC45MjE4OGwtNC45MjE4OCwtNC45MjE4OGMtMC4zMTI1LC0wLjMxMjUgLTAuNDY4NzUsLTAuNjkxOTY0IC0wLjQ2ODc1LC0xLjEzODM5YzAsLTAuNDQ2NDI4IDAuMTU2MjUsLTAuODI1ODkzIDAuNDY4NzUsLTEuMTM4MzlsMi4yNzY3OSwtMi4yNzY3OGMwLjMxMjUsLTAuMzEyNSAwLjY5MTk2NCwtMC40Njg3NSAxLjEzODM5LC0wLjQ2ODc1YzAuNDQ2NDI5LDAgMC44MjU4OTMsMC4xNTYyNSAxLjEzODM5LDAuNDY4NzVsNC45MjE4OCw0LjkyMTg4bDQuOTIxODcsLTQuOTIxODhjMC4zMTI1LC0wLjMxMjUgMC42OTE5NjUsLTAuNDY4NzUgMS4xMzgzOSwtMC40Njg3NWMwLjQ0NjQyOSwwIDAuODI1ODkzLDAuMTU2MjUgMS4xMzgzOSwwLjQ2ODc1bDIuMjc2NzksMi4yNzY3OGMwLjMxMjUsMC4zMTI1IDAuNDY4NzUsMC42OTE5NjUgMC40Njg3NSwxLjEzODM5YzAsMC40NDY0MjkgLTAuMTU2MjUsMC44MjU4OTMgLTAuNDY4NzUsMS4xMzgzOWwtNC45MjE4OCw0LjkyMTg4bDQuOTIxODgsNC45MjE4OGMwLjMxMjUsMC4zMTI1IDAuNDY4NzUsMC42OTE5NjQgMC40Njg3NSwxLjEzODM5WiIgdHJhbnNmb3JtPSJzY2FsZSgxLjAwNTYxKSIgZmlsbD0iI2ZmZiI+PC9wYXRoPjwvc3ZnPg==');
}
```

I hope this shows new designers that simple custom radio inputs aren't so hard to implement after-all and can actually be pretty fun to design. 

## 👍
