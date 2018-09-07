---
title: Using multiple CSS background images
date: 2018-08-28
summary: Learn how to set multiple background images on a single element
tags:
  - tutorial
  - css
---

It isn't something developers have a need to do very often, but you *can* set multiple background images on a single element.

Example:

```css
.element {
    background: url('image_path') center repeat, linear-gradient(transparent 0%, #000 100%) no-repeat;
}
```

What can you do with this? It's only limited by your imagination, but I'm personally a fan of always using as few elements as possible when working on a project.