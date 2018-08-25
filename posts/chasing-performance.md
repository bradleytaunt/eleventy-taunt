---
title: Chasing performance
summary: Updating my personal website for performance, accessibility and speed
description: Updating my personal website for performance, accessibility and speed
date: 2017-11-20
tags:
    - performance
    - accessibility
---

So I decided to participate in Smashing Mag's <a href="https://www.smashingmagazine.com/2017/10/front-end-performance-challenge/">Front End Performance Challenge</a>, not only for the potential of winning the prize but to further experiment with optimizing my site. (Web performance is a passion of mine)

Below I will breakdown the before &amp; after statistics of my personal site and what changes I made in great detail.

I will be using both my homepage and the image-heavy article I recently wrote, <a href="{{ site.baseurl }}/the-death-of-personality/">The Death of Personality</a>, as the basis for my tests.

### Lighthouse Score - Homepage

<a href="https://bradleytaunt.com/images/articles/lighthouse-homepage-original.png">Full source original stats</a> // <a href="https://bradleytaunt.com/images/articles/lighthouse-homepage-updated.png">Full source updated stats</a>

<table>
    <thead>
        <tr>
            <th>Stats</th>
            <th>Before</th>
            <th>After</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>Performance</th>
            <td>82</td>
            <td>98</td>
        </tr>
        <tr>
            <th>Accessibility</th>
            <td>100</td>
            <td>100</td>
        </tr>
        <tr>
            <th>Best Practices</th>
            <td>75</td>
            <td>94</td>
        </tr>
    </tbody>
</table>

### Lighthouse Score - Article Page

<a href="https://bradleytaunt.com/images/articles/lighthouse-article-original.png">Full source original stats</a> // <a href="https://bradleytaunt.com/images/articles/lighthouse-article-updated.png">Full source updated stats</a>

<table>
    <thead>
        <tr>
            <th>Stats</th>
            <th>Before</th>
            <th>After</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>Performance</th>
            <td>39</td>
            <td>96</td>
        </tr>
        <tr>
            <th>Accessibility</th>
            <td>97</td>
            <td>100</td>
        </tr>
        <tr>
            <th>Best Practices</th>
            <td>69</td>
            <td>94</td>
        </tr>
    </tbody>
</table>

### Web Page Test - Homepage

<a href="https://bradleytaunt.com/images/articles/webpagetest-homepage-original.png">Full source original stats</a> // <a href="https://bradleytaunt.com/images/articles/webpagetest-homepage-updated.png">Full source updated stats</a>

<table>
    <thead>
        <tr>
            <th>Stats</th>
            <th>Before</th>
            <th>After</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>Initial Load Time</th>
            <td>0.91s</td>
            <td class="after bar">0.41s</td>
        </tr>
        <tr>
            <th>Visually Complete</th>
            <td>0.9s</td>
            <td>0.7s</td>
        </tr>
        <tr>
            <th>Fully Loaded</th>
            <td>0.94s</td>
            <td>0.65s</td>
        </tr>
    </tbody>
</table>

### Web Page Test - Article Page

<a href="https://bradleytaunt.com/images/articles/webpagetest-article-original.png">Full source original stats</a> // <a href="https://bradleytaunt.com/images/articles/webpagetest-article-updated.png">Full source updated stats</a>

<table>
    <thead>
        <tr>
            <th>Stats</th>
            <th>Before</th>
            <th>After</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>Initial Load Time</th>
            <td>4.7s</td>
            <td>0.5s</td>
        </tr>
        <tr>
            <th>Visually Complete</th>
            <td>3.1s</td>
            <td>0.8s</td>
        </tr>
        <tr>
            <th>Fully Loaded</th>
            <td>4.8s</td>
            <td>0.67s</td>
        </tr>
    </tbody>
</table>

### Quick Look
Though my homepage only made some minor speed performance enhancements, my article post's initial load time was slimmed down by a **whopping 4.2 seconds!** That's pretty incredible and very noticeable from an end-user's perspective.

### So - What Changed?

Webfonts

I'm not using any webfonts but instead defaulting to the user's OS System Fonts. I love custom typefaces but performance takes just too much of a hit on my personal site to bother with them.

```html
body {
font-family: -apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Oxygen,Ubuntu,Cantarell,"Open Sans","Helvetica Neue",sans-serif,"Sans Serif",Icons;
}
```

For reference, there are some things you should to look out for when using custom typefaces:

- Readability and accessibility
- Possible extra overhead loading in a custom @font-face
- Try to avoid any <a href="https://css-tricks.com/fout-foit-foft/">FOUT, FOIT, FOFT</a>
- Don't go down the rabbit hole of using 3rd party plugins to optimize something as basic as a typeface

### Critical CSS

This part was easy. In order to avoid the weird styling 'pops' present on some websites when initially loading with slow connections, it's best to place all your most critical styling inline and then load your external CSS once everything else has loaded.

On top of that, I decided to also implement Filament Group's <a href="https://github.com/filamentgroup/loadCSS">loadCSS</a> function to load my CSS asynchronously. If you are not currently using this in any of your projects; stop reading this and go do it! It's a game changer.

### Critical JavaScript

My personal site only uses a small amount of JavaScript on the article post Jekyll template pages. By using the <code>defer</code> property I can be sure to load the <code>IntersectionObserver</code> API polyfill after the rest of the DOM as finished loading.

```html
<script src="https://cdn.polyfill.io/v2/polyfill.min.js?features=IntersectionObserver" defer>
```

I could probably optimize this further by only calling these scripts if an image is actually present in the article post, but this fits my needs nicely as is.

### Responsive Images

The only images I use are those included in supported blog posts, so the first step was making sure to only call <code>iolazy.min.js</code> on those specific template pages. The next step was defaulting to <code>webp</code> image formats with a lossless <code>jpg</code> fall-back with the help of the <code>picture</code> element:

<span class="sidenote">I've also included responsive image sizes for further optimization based on screen size and loading speeds.</span>

```html
<figure>
<picture
    <source type="image/webp"
    data-srcset="
    /images/articles/webp/flat-design-toggles_p0v2hv_c_scale,w_200.webp 200w,
    /images/articles/webp/flat-design-toggles_p0v2hv_c_scale,w_1400.webp 1400w"
    class="lazyload"/>
    <img
    sizes="(max-width: 1400px) 100vw, 1400px"
    data-srcset="
    /images/articles/flat-design-toggles_qfre51_c_scale,w_200.jpg 200w,
    /images/articles/flat-design-toggles_qfre51_c_scale,w_727.jpg 727w,
    /images/articles/flat-design-toggles_qfre51_c_scale,w_1065.jpg 1065w,
    /images/articles/flat-design-toggles_qfre51_c_scale,w_1400.jpg 1400w"
    src="/images/placeholder.png"
    alt="Toggles Comparison"
    class="lazyload"/>
</picture>
</figure>
```

What about users with JavaScript disabled I hear you ask? It's time for <code>noscript</code> to save the day:

```html
<noscript>
    <picture>
        <source type="image/webp"
        srcset="
        /images/articles/webp/flat-design-toggles_p0v2hv_c_scale,w_200.webp 200w,
        /images/articles/webp/flat-design-toggles_p0v2hv_c_scale,w_1400.webp 1400w">
        <img
        sizes="(max-width: 1400px) 100vw, 1400px"
        srcset="
        /images/articles/flat-design-toggles_qfre51_c_scale,w_200.jpg 200w,
        /images/articles/flat-design-toggles_qfre51_c_scale,w_727.jpg 727w,
        /images/articles/flat-design-toggles_qfre51_c_scale,w_1065.jpg 1065w,
        /images/articles/flat-design-toggles_qfre51_c_scale,w_1400.jpg 1400w"
        src="/images/articles/flat-design-toggles_qfre51_c_scale,w_1400.jpg"
        alt="Toggles Comparison"/>
    </picture>
</noscript>
```

### HTTPS &amp; Caching

The Lighthouse audit also suggested implementing an SSL certificate (something I've been meaning to do for a while anyway) and also utilize CDN caching. So it was Cloudflare to the rescue!

Since my website is hosted through Github, setting up a *free* SSL certificate and enabling site-wide caching was a breeze. If you're interested in setting this up yourself, step-by-step instructions can be found <a href="https://gist.github.com/cvan/8630f847f579f90e0c014dc5199c337b">here</a>.

This simple update helped boost my best practices score from a 69 to a 94. Yet another performance enhancement you should be enabling for all your current and future projects!


## Performance Happiness

Overall I'm pretty content with the **major** performance boost my site has received from these fairly *minor* updates and I hope this article inspires other designers and developers to jump into updating their own site/app performance speeds. The pay-off is truly worth it!

### Some Extra Reading Material
- <a href="https://www.amazon.ca/Web-Performance-Action-Building-Faster/dp/1617293776/ref=sr_1_1?ie=UTF8&qid=1510585897&sr=8-1&keywords=web+performance+in+action">Web Performance in Action</a> by <i>Jeremy Wagner</i>


- <a href="https://www.amazon.ca/Responsible-Responsive-Design-Scott-Jehl/dp/1937557162/ref=sr_1_1?s=books&ie=UTF8&qid=1510585972&sr=1-1&keywords=responsible+responsive+design">Responsible Responsive Design</a> by <i>Scott Jehl</i>
- <a href="https://www.amazon.ca/Designing-Progressive-Enhancement-Building-Everyone/dp/0321658884/ref=sr_1_1?s=books&ie=UTF8&qid=1510586005&sr=1-1">Designing with Progressive Enhancement: Building the Web that Works for Everyone</a> by <i>Todd Parker, Scott Jehl,‎ Maggie Costello Wachs,‎ Patty Toland</i>