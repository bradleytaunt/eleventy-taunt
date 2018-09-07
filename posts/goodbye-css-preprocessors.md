---
title: Goodbye CSS preprocessors
summary: A deep dive into why I believe vanilla CSS is the ultimate CSS
date: 2017-08-07
tags:
    - css
    - tutorial
---

I've been using preprocessors across all my side projects since they first popped onto the scene. Sass, Stylus, LESS — you name the CSS preprocessor and I've most likely used it because CSS preprocessors are awesome.

But that all changes moving forward. I'm going back to basics with CSS. Straight vanilla, man.

<figure>
    <picture>
        <img src="http://bradleytaunt.com/static/images/articles/sass-cancel_rl1fsw_c_scale,w_800.jpg"
        alt="Sass">
    </picture>
</figure>

## Why? And who cares?

Let's start by breaking down the main positives about preprocessors:

- Nested syntax
- Definable variables
- Advanced mathematical functions
- Reusable mixins

All of these features are great and I completely understand the draw (I was also sucked into the hype) - but now let's see the negatives.

### 1. Debugging is a chore

So you found some weird padding clobbering an element's default styles on line 255 of your main complied CSS file? Excellent! Now you just need to figure out which file that property comes from.

This might sound trivial or that you can fix this with rendered comments but if you ever work on a project with hundreds of Sass/Stylus/LESS files all importing and compiling into each other - it can get out of hand.

Solution: Using plain CSS makes using browser dev tools a breeze. See a bug on line 255? No problem, let me fix line 255.

### 2. Dependencies for development

Building a project with a preprocessor brings with it unnecessary baggage; dependencies. You'll need to be running some sort of task runner (see grunt or gulp) that will compile and minify your CSS. I see this as extra overhead both during the initial setup of the project for new team members and the testing environment.

By using plain CSS, you avoid including an extra package in your package.json file (if applicable) or having to rely on third party compilers such as codekit (although I do recommend this app).

### 3. Variables &amp; mixins become unwieldily

Both variables and mixins are great in small doses, but if your project has any real size to it these helpers become a hinderance. By using comma-delimited CSS selectors you can achieve the same outcome without the horror of needing a specific preprocessor file to handle just variables and mixins.

Basic example:

```css
selector, selectTwo, .css-class {
    /// shared styling ///
}
```

### 4. Welcome to nesting hell

Honestly, I've never been a fan of nesting. From a file structure perspective it is indeed very "clean", but you sacrifice that cleanliness in the final compiled production code. You're making your development environment easier to glance at and work through at the cost of your production-ready, customer facing code.

You also run into another big no-no in my eyes: extreme selector specificity. The DOM target search starts to get out of control once you start having classes and selectors building up towards 10 or more steps.

Bad:

```css
body #home .container .modal nav .inner-nav > ul > li > a {
    color: red;
}
```

Good:

```css
.inner-nav a {
    color: red;
}
```

Don't forget the amount of work needed to override styling with such deep selector specificity. That's where you end up diving into the world of <i>!important</i> tags.

## Final thoughts

It should go without saying that this is just my personal preference, there is no law behind this. If you use and absolutely love preprocessors - more power to you. All I suggest is using plain old vanilla CSS for your next project and see how it works out.

And do you know what I've learned to appreciate after switching back to vanilla? <strong>CSS is more beautiful when developed in it's rawest form</strong>.
