---
title: Over-nesting
summary: The drawbacks of over-nesting your CSS classes and selectors
date: 2019-01-06
tags:
    - CSS
---

I think since our design industry moves so quickly and exciting new technologies get released almost daily, that we often forget some of the basics when writing CSS. I bring this up because I've recently worked on a few projects that show a slight disregard for proper class/selector nesting.

Now it's completely understandable why designers and teams alike shrug off the concept of "over-nesting":

- As a team we know the structure of our code (no outside party needs to interact with it)
- Everything is written in `insert pre-processor here` - so it's cleaner/compiled anyway
- It's *technically* DRY

I personally believe these are all weak excuses that don't justify the poor experience future maintainers of your code will face. *You should always write your code with idea that someone completely new to the project will have to maintain it*.

Let's look at an average example of poor nesting that I've seen out in the wild:

```css
/* These children elements can't be used outside 
of the parent - not very flexible */
.main-container {
    .child-container {
        /* This class specificity is too deep */
        .sub-child-container {}
    }
}
```

Even if you know a child element will never be structured outside of it's parent, what harm does it cause to still place it out of such deep specificity?

```css
/* This code is far more reusable */
.main-container {}
.child-container {}
.sub-child-container {}
```

### Exceptions

As with anything, there are exceptions to the *rule*. If the nested elements pertain to the parent itself, it makes complete sense to group these stylings together. A button or link item are excellent examples of this:

```css
.btn-lg {
    &:hover {}
    &:active {}
    &:disabled{}
}

.link-item {
    &:hover{}
    &:focus{}
}
```

Of course, this is all easier said than done. Limitations exist within teams or even on an individual level that might make this impossible to change. Maybe you don't have the authority to rework your current CSS or it would eat up too many cycles and time is valuable - especially in the world of startups. 

I'm not saying this is **the only way to structure CSS** - I'm only trying to make the lives of future designers/developers easier moving forward. 