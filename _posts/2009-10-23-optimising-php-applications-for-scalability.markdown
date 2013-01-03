---
comments: true
date: 2009-10-23 14:37:23
layout: post
slug: optimising-php-applications-for-scalability
title: Optimising PHP Applications For Scalability
summary: Optimising PHP Applications For Scalability
wordpress_id: 37
image: placeholder.png
tags:
- optimisation
- php
- tips
---

#####  Optimising PHP Applications For Scalability

- **Tip Number 1** - Make http://www.phpbench.com/ your best friend, and remember, if your app needs to scale to large amount of simultaneous users then even the stuff that seems make very little difference on paper can actualy make a huge difference in real life scenarios.
- **Tip Number 2** - From PHPBench it is possible to see that the difference between single quotes (') and double quotes (") in string declaration now appear to be negligible, however, I'm a little wary of this so would recommend always using single quotes, it can't hurt can it, plus it'll still take some of the strain away from the server as the PHP parser won't have to scour strings for variables.
- **Tip Number 3** - Unset every variable you can as soon as you can. PHP's garbage collector can be a bit skittish sometimes, unset the variables where ever possible to mark them to be collected. Unset is a language construct rather than a function so you should see no impact on performance.
- **Tip Number 4** - Speaking of language constructs, use them where ever possible. Calling isset before is_array helps immensely as running is_array on an unset variable is 700% slower than running is_array on a variable that is set. And, while we're at it, rather than using strlen($var) use isset($var{0}).
- **Tip Number 5** - This is the biggest performance hit of all, doing crazy ass stuff like for($i = 0; $i<count($var); $i++), having the count function within the for loop makes the code run a whopping 5000% (yes that is 3 0's) slower then doing, $count = count($var); for($i = 0; $i<$count; $i++). You now know it, so you have no excuses.
- **Tip Number 6** - Make as few database calls as possible. Come on now, hands up, how many times have you done the following, and be honest:

    foreach($arrayVals as $arrayVal){
        $sql = 'INSERT INTO {Table} (value) VALUE ('.$arrayVal.')';
        mysql_query($sql);
    }

All I can say is DON'T! Do the following instead...

    $values = '';

    foreach($arrayVals as $arrayVal){
        $values .= '('.$arrayVal.'), ';
    }

    $values = substr(trim($values), 0, -1);

    $sql = 'INSERT INTO {Table} (value) VALUES '.$values;

    mysql_query();

Same result, only 1 query. And another point, if you're concatenating a variable in a loop like above, make sure you initialise the variable before hand!

That's pretty much it for now, a short list I know, but there will be more to come, I promise.
