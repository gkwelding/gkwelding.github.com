---
comments: true
date: 2010-05-07 16:33:08
layout: post
slug: google-maps-icon-generation
title: Google Maps Icon Generation
summary: Google Maps Icon Generation
wordpress_id: 89
image: 'google-maps-icon-generation/google.png'
tags:
- google api
- google maps
- php
---

#####  Google Maps Icon Generation

I recently published an article on a library I'd written for CodeIgniter for generating Google maps to display on your CI projects.

To take this one step further I also have a small, independent, php script that you can pass into the image parameter when generating a marker to use rather than having a static image file for every possible combination of numbers (1 or 2 digits, 0 - 99) and letters (1 or 2 characters, A - ZZ). To do this the static image way would require 152 separate image files. Doing it this way requires 1 php script, 1 true type font file and 1 web request. lol. win!

Usage is really simple. Upload the php script and ttf file to the same location on your webserver. Then call the following from your web browser, or add the full url to the image paramter of the gmaps marker call.

http://www.your_website.com/icon_gen.php?color=ff776b&text=1

You should then get a red'ish Google map marker with a 1 in the middle of it. Change the text to whatever you want. If the text is misaligned you can edit the alignment modifications in the icon_gen.php file, it's a hacky way of doing it but the best I could cobble together for now.

Enjoy people.

## [GMAPS ICON GEN SCRIPT (40kb zip)](/img/posts/icon_gen.zip)
