---
title: Setting up a free SSL
summary: Learn how to implement a free SSL on your site with Cloudflare
description: Learn how to implement a free SSL on your site with Cloudflare
date: 2018-08-07
tags:
    - tutorial
---

I never had to worry about SSL certificates when I originally hosted my blog through Github Pages, but since switching over to Surge.sh I lost my ability to utilize `https` protocol.

Luckily, Cloudflare offers a very simple way to implement SSL on your website - and it's free!

### SSL in 3 easy steps

1. You will need to have a Cloudflare account - <a href="https://dash.cloudflare.com/sign-up">you can setup one here</a>. Be sure to select the 'Free' pricing plan (unless you want some extras features)

2. Follow the process on updating your nameservers to the proper Cloudflare servers and wait for your domain to update the changes. (This can take up to 24 hours)

3. From the main Cloudflare dashboard navigate to the Crypto tab. Then under the SSL section, select "Flexible" from the dropdown.

### Enjoy your newly secure site

That's it! Give it a bit of time and soon your website will support `https` and best of all it costs you nothing!

I suggest checking out the other interesting features Cloudflare offers while your playing with the dashboard as well. They have a lot of impressive options that can really improve the overall performance of your site / web app.
