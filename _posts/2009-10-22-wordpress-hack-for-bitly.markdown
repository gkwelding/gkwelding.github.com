---
comments: true
date: 2009-10-22 14:42:38
layout: post
slug: wordpress-hack-for-bitly
title: Wordpress hack for bit.ly
summary: Wordpress hack for bit.ly
wordpress_id: 12
image: placeholder.png
tags:
- exciting
- php
- Plugins
- Wordpress
---

#####  Wordpress hack for bit.ly

Wow, just spent 30min hacking the 'Sociable' plugin for Wordpress to use bit.ly instead of awe.sm. Harder than you might have thought! If anybody's interested then give me a shout and I'll take you through it. However, if you're content with just hacking the code and hard coding your bit.ly login name and API key into your sociable.php file then you can do the following...

Replace everything between line 735 and the } else { in sociable.php with the following...

    $bitlyapikey      = '{api_key}';
    $bitlylogin          = '{api_login'};

    $login = '&login;='.$bitlylogin;
    $key = '&apiKey;='.$bitlyapikey;

    $bitlyurl = 'http://api.bit.ly/shorten?version=2.0.1&longUrl;='.$permalink.$login.$key;

    $bitlyurl = file_get_contents($bitlyurl);
    $bitlyurl = (string) $bitlyurl;

    $find = '!"shortUrl": "(.+?)"!';
    $matches = array();
    preg_match($find, $bitlyurl , $matches);

    if(isset($matches['1'])) {
        $url = str_replace('PERMALINK', $matches['1'], $url);
    } else {
        $url = str_replace('PERMALINK', $permalink, $url);
    }
