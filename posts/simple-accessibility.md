---
title: Simple accessibility
date: 2018-09-07T16:53:51.088Z
summary: Learn how to implement some basic accessibility with little-to-no effort
tags:
  - accessibility
---
Implementing proper accessibility practices can seem a little daunting at first, but there are a few basic standards you can introduce into your project work-flow that are fairly straightforward:

## Basic design

1. Test that your project has the proper contrast color settings between type, backgrounds, icons etc.
2. Only use "fancy" grid-ordering for minor layout design - avoid rearranging important content via CSS

## Content

1. Use proper HTML structures (aside, header, main, footer elements as needed)
2. Make use of the [aria-label attribute](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-label_attribute)
3. Ensure your website/app can be navigated completely (and properly) with only a keyboard

## Images

1. Avoid using CSS backgrounds for content images (should only be used for patterns, layout design etc.)
2. Ensure proper `alt` attributes are provided on all images

It isn't much - but follow these basics and you'll be one step closer to providing better accessibility to your users.
