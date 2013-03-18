---
comments: true
date: 2013-03-18 14:30:00
layout: post
slug: the-getfingerprint-method
title: The getFingerPrint Method
summary: 'Sometimes I hate being a developer...'
image: 'the-getfingerprint-method/getfingerprint.jpg'
tags:
- php
- work
- development
---

Read the comment, then the code... If you can't see what's so fundamentally wrong with this then please, never come here again, you're barred!

    /**
    * getFingerPrint
    * 
    * The getFingerPrint method allows us to create a string based 
    * on the users HTTP_USER_AGENT and a SALT.
    * 
    * By checking this we can ensure that we are dealing with the 
    * same user each time.
    * 
    */
    public static function getFingerPrint() { 
        return md5($_SERVER['HTTP_USER_AGENT'] . "|primo");        
    }

I found this wonder of modern development today... Luckily an extensive search of the codebase found it wasn't used, anywhere! What strikes me as concerning is that some monkey wrote it in the first place with the intention of using it.