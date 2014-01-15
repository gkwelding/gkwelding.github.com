---
comments: true
date: 2014-01-14 12:53:00
layout: post
slug: learning-fuelphp-for-effective-php-development-review
title: "A Review of Learning FuelPHP for Effective PHP Development"
summary: "Here's some good examples why, from one specific area but I think this rings true across multiple areas."
image: 'learning-fuelphp-for-effective-php-development-review/cover.jpg'
tags:
- development
- php
- fuelphp
- book review
---

Disclaimer! I have been asked to review [Learning FuelPHP for Effective PHP Development] [1] by Ross Tweedie, and given a free digital copy, by the books publisher Packt Publishing. However, as those of you that know me well will know any bias I may have extends to my immediate family and no further, not even to people who give me free stuff... If it's crap I'll tell you...

Before I even agreed to read this book I did some digging on the author, Ross. What I found convinced me that this book might be worth a quick read and that I wasn't going to end up in the awkward situation of having agreed to provide a review and then having to write something scathing about it because it was utter trash. My expectations were set.

# The Introduction #

Two pages in and I was starting to get worried. From my research on the author I was fully expecting this book to be a fantastic resource for the beginner FuelPHP developer however the introduction to Fuel was sketchy at best, poorly written and proof-read at the worst. Now I'm no professional writer myself but I was starting to get concerned about the rest of the book.

# The Technical Details #

Thankfully the technical details are what save this book. And luckily it's the technical details that matter. Now I'm not sure if the introduction to FuelPHP was written by somebody else, or whether it was just rushed as a last minute addition before the book went to print but there's certainly a big step change between the intro and the rest of the book.

## Installation ##

This book is aimed squarely at the absolute FuelPHP beginner. And it hits that market spot on. It maybe goes a bit too far in as much as it tells you how to set up/configure Apache, PHP and Git. I think maybe the Installation section would have been better off starting 4 sections later at 'Getting and installing FuelPHP with curl and Oil'. This section and the sections after this though are all fantastic explanatory resources for the FuelPHP novice, including the concept of Oil that people who have never used Ruby on Rails or FuelPHP before will find highly confusing.

The section on migrations disappointed me slightly as I feel it could have explained a little more the principles behind it, however I had high hopes for the 'migration examples' promised later on in the book.

## The Architecture & Demo Application ##

I'm going to skip over a lot of this as it's all fairly basic stuff, explaining MVC and the architecture of Fuel apps. The demo application is a good example, it demonstrates how to create a blog site but also includes user authentication which is always a great thing to include as so many get it so so wrong. But this is where we hit the promised section on Migrations, one concept I struggled with when I first came to FuelPHP. Although this section is short it explains the concepts of migrations very clearly, it does very little hand holding in this section but explains the concept of migrations in a way a complete novice would understand, something I imagine is quite hard to do.

## Packages & Advanced Topics ##

Now this is the bit of the book I really really liked. Rather than assuming new users of FuelPHP should just worry about getting to grips with the framework and nothing else, Ross introduces some of the PHP fundamentals rippling through the PHP community currently. Topics such as; Composer (including using pre-built packages and building your own), Unit testing, Profiling, Routing and Namespaces, all of which are topics that need to be introduced to new PHP developers as early as possible in the learning process to stop the creep of utterly rubbish PHP code available out there.

# In Summary #

This book is a brilliant resource for the beginner Fuel developer including those just starting out in the world of PHP. Ignore the poorly written background information and focus on Chapter 2 onwards and you'll have a very positive experience!

[1]: http://www.amazon.co.uk/Learning-FuelPHP-Effective-PHP-Development-ebook/dp/B00GTQD5O2 "Learning FuelPHP for Effective PHP Development"