---
title: Width or flex-basis?
summary: Breaking down when to use the width property or flex-basis with flexbox
date: 2018-11-28
tags:
  - CSS
---

Creating rows and columns of elements that adapt dynamically can be a little tricky depending on the desired outcome. Let's breakdown how to solve this issue using both `inline-block` paired with `width` and `flex-basis`.

## Width

Setting the width of the inner children to a divisible value and setting their display to `inline-block`, we are able to create self-wrapping elements:

```css
.width-container {
    display: block;
}
.width-container__item {
    display: inline-block;
    width: calc(33% - 3px); /* Fix for wonky inline-block margins */
}
```

### Pros
- <a href="https://caniuse.com/#search=inline-block">Full browser support</a> (as far back as IE6)
- No floats needed

### Cons
- Buggy `margin` workaround needed
- Wrapped elements cannot dynamically fill remaining empty parent space

## Flex-basis

This is my personal preference for dynamically wrapping inner children elements. Simply set the parent as `display: flex`, allow flex-wrapping and then set the `flex-basis` of the children to any percentage value.

```css
.flex-container {
    display: flex;
    flex-wrap: wrap;
}
.flex-container__item {
    flex: 1 1 auto;
    flex-basis: 33%;
}
```

You will also notice the `flex` property set to `1 1 auto`. This is important if you require your wrapped elements to fill the remaining space of the parent container.

### Pros
- No buggy margins to play with
- Dynamically renders children to fill parent container if `flex` is set
- Scales well across screen / device sizes

### Cons
- Some versions of IE struggle with <a href="https://caniuse.com/#search=flex-basis">browser support</a>

## CodePen Demo

Feel free to play around with a slightly more stylized version of both options below:

<p data-height="477" data-theme-id="0" data-slug-hash="JevaYQ" data-default-tab="css,result" data-user="bradleytaunt" data-pen-title="Width or flex-basis" class="codepen">See the Pen <a href="https://codepen.io/bradleytaunt/pen/JevaYQ/">Width or flex-basis</a> by Bradley Taunt (<a href="https://codepen.io/bradleytaunt">@bradleytaunt</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
