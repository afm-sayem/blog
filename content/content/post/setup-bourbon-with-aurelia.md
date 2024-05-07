+++
date = "2016-08-20T04:03:46-06:00"
draft = false
title = "Setup Bourbon with Aurelia"

+++

I &#9829; [Bourbon](http://bourbon.io). I &#9829; [Aurelia](http://aurelia.io).

To use Bourbon with Aurelia, we will first create a project with [aurelia-cli](http://aurelia.io/hub.html#/doc/article/aurelia/framework/latest/the-aurelia-cli). Use SCSS as the preprocessor when the project asks for configuration values.

Done? Now let's install bourbon and neat from npm.

`npm install bourbon bourbon-neat --save`

Go to the `aurelia_project/tasks` directory and open up `process-css.js` and add these lines

```
import bourbon from 'bourbon';
import neat from 'bourbon-neat';
```

Modify the `.pipe(sass().on('error', sass.logError))`
line to the following:

```
    .pipe(sass({
      includePaths: [].concat(bourbon.includePaths, neat.includePaths)
    }).on('error', sass.logError))
```

Done! Let's test things out now shall we?

Create app.scss in `src`

```
@import "bourbon";
@import "neat";

section {
  @include outer-container;
  header { @include span-columns(3); }
  section { @include span-columns(9); }
}
```

Replace app.html to this

```
<template>
  <require from="./app.css"></require>
  <section>
    <header>What is it about?</header>
    <section>Neat is an open-source semantic grid framework built with Sass…</section>
  </section>
  <section>
    <header>Where do we go from here?</header>
    <section>Far</section>
  </section>
</template>
```

Run the Aurelia application and you should have the contents organized in a grid.

#### Bonus: Bitters and How to structure your project

[Bitters](bitters.bourbon.io) provides the scaffolding and structure for your `scss` files in your project.

Install the bitters gem and run `bitter install` in your `src` directory. You'll see a folder named 'base'(with contents) will be created. I usually rename `base` to `style` but it's a matter of personal taste.

Now to start using the scaffolded styles, import `base.scss` from your `style`/`base` directory after the import of `bourbon` and `neat`.

```
@import "bourbon";
@import "neat";
@import "style/base";
```

In all of your views/components style files, require the `app.scss` and you will have all the mixins and sweet things from bourbon and neat.

Neat! No?
