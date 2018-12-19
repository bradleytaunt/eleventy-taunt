---
title: Using parent selectors in CSS
date: 2018-12-19
summary: Let's take a simpler look at how to implement the jsincss-parent-selector plugin
permalink: /posts/using-parent-selectors/
tags:
  - CSS
  - JavaScript
---

I recently saw a Twitter thread posted by <a href="https://twitter.com/innovati/status/1068998114491678720">Tommy Hodgins</a> on implementing highly requested styling features in CSS with only a minimal amount of JavaScript. Many of his examples are great, but the `parent` selector instantly peaked my interest.

Being able to target an element's parent always becomes a minor annoyance (since vanilla CSS does not support it) - so you always end up having to do something a little ugly like:

```js
var el = document.getElementById('custom-div');
var parent = el.closest(selectors);
```

And then add any custom styling to the parent element directly in JavaScript - or toggle a class which opens a whole other can of worms.

## Save the day with <a href="https://www.npmjs.com/package/jsincss-parent-selector">jsincss-parent-selector</a> and <a href="https://github.com/tomhodgins/qaffeine">qaffeine</a>

By using the `jsincss-parent-selector` and `qaffeine` plugins we can target an element's parent in CSS without breaking a sweat. Let's break it down:

### Import the packages

```js
npm install jsincss-parent-selector qaffeine
```

### HTML (ex. index.html)

```html
<!doctype html>
<html>
    <head>
        <link rel="stylesheet" href="output.css">
    </head>
    <body>
        <header>
            <main>
                <h2>This is a header</h2>
            </main>
        </header>
    </body>
    <script src=output.js></script>
</html>
```

### JavaScript (ex. input.js)

```js
const qaffeine = require('qaffeine')
const parent = require('jsincss-parent-selector')

qaffeine(
  {
    stylesheet: {},
    rules: {
      parent
    }
  },
  'input.css',
  'output.js',
  'output.css'
)
```

### CSS (ex. input.css)

```css
header {
    display: block;
}
main[--js-parent] {
    background: blue;
}
```

Then simply run `node` against your `js` file. That's it! I would also suggest checking out Tommy's <a href="https://www.youtube.com/watch?v=rG8cLe7VbW0">video covering this topic</a> if you prefer to follow along.
