---
comments: true
date: 2013-08-09 18:39:00
layout: post
slug: why-its-important-to-know-how-to-use-your-tools
title: "Why It's Important To Know Your Tools Inside And Out"
summary: "Here's some good examples why, from one specific area but I think this rings true across multiple areas."
image: 'why-its-important-to-know-how-to-use-your-tools/cover.png'
tags:
- development
- image editing
- website optimisation
---

So. I happened upon an interesting website/toolset today, [JPEGmini] [1]. Interesting because it looks like some tool that bundles up a standard image compressor with some settings tweaked that people don't normally touch, and they're charging $20 for that honour... Let take a look shall we.

Disclaimer! I'm not an image expert. I'm a developer/code monkey. When I announce that "I can't see a discernable difference in the quality" it doesn't mean one doesn't exist, it just means I'm too stupid/inexperienced to see it. Also, I'd like to get the legalities out of the way right here at the top. The red flower image used in this post is from [Rene Mensen's Flickr] [2] and the picture of the dog is from [Edward Simpson's Flickr] [3], both images are released on the [Creative Commons 2.0 License] [4]. Phew...

The first example by [JPEGmini] [1] is a picture of a dog by a river. Lets take a look at the original, then the [JPEGmini] [1] optimised version and then some that have been fiddled with by me in GIMP2.

* [dog by a river original] [5] (2.11mb)
* [dog by a river processed with JPEGmini] [6] (380kb)
* [dog by a river GIMP defaults 80% compression] [7] (483 kb)
* [dog by a river GIMP defaults 70% compression] [8] (363 kb)
* [dog by a river GIMP defaults 60% compression] [9] (297 kb)
* [dog by a river GIMP tweaked 50% compression] [10] (193 kb)

Now, [JPEGmini] [1] manages a quite respectable 380kb, and with a quality factor of 80 GIMP2 can only manage 483kb with the default settings. However, if we knock it down a further 10, to a quality factor or 70, then the resulting GIMP2 filesize is 363kb, a full 17kb smaller than [JPEGmini] [1]'s effort. And, to my untrained eye, I can see no difference between the two either. But how low can we go? Apparently as low as a quality factor of 50 apparently, and throwing in some tweaks to smoothing (cranked it up to 0.1) and turning some subsampling option down to "4:2:0 chroma quartered", whatever the hell that means, got the file size down to a miniscule 193 kb. And again, I may be commiting designer blasphemy here, I couldn't really see a difference between the [JPEGmini] [1] version and my heavily compressed version.

Maybe that example image was a fluke? Lets try another image, something completely different.

* [red flower original] [11] (7.88 mb)
* [red flower processed with JPEGmini] [12] (1.14 mb)
* [red flower GIMP defaults 80% compression] [13] (1.45 mb)
* [red flower GIMP defaults 70% compression] [14] (1.01 mb)
* [red flower GIMP defaults 60% compression] [15] (808 kb)
* [red flower GIMP tweaked 50% compression] [16] (483 kb)

This image is a much higher resolution image, and I think, if I zoom in far enough on the uber compressed version (with smoothing and subsampling tweaked) I might eb starting to see some kind of distortion and/or visible loss of quality. However, this tool markets itself as a tool for optimising images for web sites. Who in their right mind is going to be hosting a 4928x3264 image as a web site asset at full resolution?

> So far, 18 patent applications have been submitted for various technologies included in JPEGmini, and two papers describing the technology have been accepted and presented at the prestigious SPIE Electronic Imaging 2011 conference in San Francisco.

They have technology that can be patented (doesn't really say much about the product though as the US patent office would patent a cheese sandwich if someone paid them enough) and a couple of published papers so there must be something in the technology that's worthy. However, I'm sturggling to see the benefit this would give a web designer.

My advice? Save your $20 and learn about the options available to you when compressing images. The other draw back is [JPEGmini] [1] only works on jpeg files. Your image editors compression tools will work on any file format. Learn the tools you use, learn how to use them effectively.

[1]: http://www.jpegmini.com/ "JPEGmini"
[2]: http://www.flickr.com/photos/renemensen/8634798653/sizes/o/in/photostream/ "Rene Mensen's Flickr"
[3]: http://www.flickr.com/photos/king-edward/2687248016/sizes/o/in/photostream/ "Edward Simpson's Flickr"
[4]: http://creativecommons.org/licenses/by/2.0/ "Creative Commons 2.0 License"
[5]: http://in-the-attic.com/img/posts/why-its-important-to-know-how-to-use-your-tools/Ed.ward.jpg "dog by a river original"
[6]: http://in-the-attic.com/img/posts/why-its-important-to-know-how-to-use-your-tools/Ed.ward_mini.jpg "dog by a river processed with JPEGmini"
[7]: http://in-the-attic.com/img/posts/why-its-important-to-know-how-to-use-your-tools/Ed.ward_gimp80.jpg "dog by a river GIMP defaults 80% compression"
[8]: http://in-the-attic.com/img/posts/why-its-important-to-know-how-to-use-your-tools/Ed.ward_gimp70.jpg "dog by a river GIMP defaults 70% compression"
[9]: http://in-the-attic.com/img/posts/why-its-important-to-know-how-to-use-your-tools/Ed.ward_gimp60.jpg "dog by a river GIMP defaults 60% compression"
[10]: http://in-the-attic.com/img/posts/why-its-important-to-know-how-to-use-your-tools/Ed.ward_gimp50s.jpg "dog by a river GIMP tweaked 50% compression"
[11]: http://in-the-attic.com/img/posts/why-its-important-to-know-how-to-use-your-tools/ReneMensen.jpg "red flower original"
[12]: http://in-the-attic.com/img/posts/why-its-important-to-know-how-to-use-your-tools/ReneMensen_mini.jpg "red flower processed with JPEGmini"
[13]: http://in-the-attic.com/img/posts/why-its-important-to-know-how-to-use-your-tools/ReneMensen_gimp80.jpg "red flower GIMP defaults 80% compression"
[14]: http://in-the-attic.com/img/posts/why-its-important-to-know-how-to-use-your-tools/ReneMensen_gimp70.jpg "red flower GIMP defaults 70% compression"
[15]: http://in-the-attic.com/img/posts/why-its-important-to-know-how-to-use-your-tools/ReneMensen_gimp60.jpg "red flower GIMP defaults 60% compression"
[16]: http://in-the-attic.com/img/posts/why-its-important-to-know-how-to-use-your-tools/ReneMensen_gimp50s.jpg "red flower GIMP tweaked 50% compression"