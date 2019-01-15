---
layout: post
title: Basic gulp build for Sass
description: A basic starting point for compiling Sass with Gulp
---

Some designers might shy away from build tools when first starting out and I can understand the reasoning - task runners like `gulp` and `grunt` can seem daunting at first. So, I've decided to showcase my go-to setup for `gulp` and explain what the heck it does step-by-step. 

Here is the final `gulp.js` file in all it's glory:

```js
var gulp = require('gulp');
var shell = require('gulp-shell');
var sass = require('gulp-sass');

/*
  Build and watch Jekyll (change this task to whatever you need)
*/
gulp.task('generate', shell.task('jekyll serve'));

/*
  Compile SCSS files to CSS
*/
gulp.task('styles', function () {
    return gulp.src('_includes/assets/sass/styles.scss')
        .pipe(sass({
            outputStyle: 'compressed'
        }).on('error', sass.logError))
        .pipe(gulp.dest('_includes/assets/css/'));
});

/*
  Compile the assets
*/
gulp.task('assets', gulp.parallel(
    'styles'
));

/*
  Build
*/
gulp.task('build', gulp.series(
    'assets',
    'generate'
));
```

Trust me, it's not complicated at all.

## Grabbing what we need

For our basic build file we are going to need only three modules: `gulp`, `gulp-shell` and `gulp-sass`.

```js
var gulp = require('gulp');
var shell = require('gulp-shell');
var sass = require('gulp-sass');
```

#### gulp
This is the streaming build system, without it we can't do anything else.

#### gulp-shell
A gulp command line interface for us to interact with our terminal.

#### gulp-sass
Required for gulp to compile Sass into vanilla CSS.

<div class="message">

<p><strong>Bonus tasks</strong></p>

<p>You can also toss in <code>gulp-minify</code> to clean-up any JavaScript you might be using, but for this example we're just going to keep things simple and focus on Sass only.</p>

<p class="no-margin">Maybe I'll write about my <code>js</code> build workflow in a future article.</p>

</div>

## Generating the build

Our first step is to create the default task that will generate our build. In this example we are making the assumption that we're building a Jekyll website (but you can place any build command here):

```js
gulp.task('generate', shell.task('jekyll serve'));
```

Don't worry if this `generate` isn't clear, we come back to that later.

## Processing our pre-processor

We will name this next task `styles` since that's what it outputs - our styling. We start by telling gulp where our main `scss` directory is:

```js
/* Change this directory to match yours */
return gulp.src('_includes/assets/sass/styles.scss')
```

This next piece tells the plugin to compress our final compiled CSS, log any errors if there are issues with the build and then export it to our destination directory:

```js
.pipe(sass({
    outputStyle: 'compressed'
}).on('error', sass.logError))

/* Change this to your destination directory */
.pipe(gulp.dest('_includes/assets/css/'));
```

## Building our assets

This step isn't 100% needed, but I like to include it for when more assets need to be added (minifying JavaScript, compressing images, etc)

```js
/*
  Compile the assets
*/
gulp.task('assets', gulp.parallel(
    'styles'
));
```

## Altogether now!

Now we add a task that runs all other tasks in our gulp file (in this case it will run both `assets` and `generate`)

```js
/*
  Build
*/
gulp.task('build', gulp.series(
    'assets',
    'generate'
));
```

And that's it - we're done! A very basic `gulp` build for compiling Sass.