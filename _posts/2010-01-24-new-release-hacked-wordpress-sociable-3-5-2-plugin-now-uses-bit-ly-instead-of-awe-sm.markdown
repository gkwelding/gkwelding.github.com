---
comments: true
date: 2010-01-24 01:09:49
layout: post
slug: new-release-hacked-wordpress-sociable-3-5-2-plugin-now-uses-bit-ly-instead-of-awe-sm
title: New release, hacked Wordpress Sociable 3.5.2 plugin now uses bit.ly instead of awe.sm!
summary: New release, hacked Wordpress Sociable 3.5.2 plugin now uses bit.ly instead of awe.sm!
wordpress_id: 57
image: placeholder.png
tags:
- Hack
- Plugins
- Sociable
- Wordpress
---

#####  New release, hacked Wordpress Sociable 3.5.2 plugin now uses bit.ly instead of awe.sm!

I've had a surprising amount of interest in an old post on this site about hacking the sociable plugin to use bit.ly instead of awe.sm. Now the example used in the post was an older version of sociable and there have been a few releases since. In this post I will show you what to change in the latest version of sociable (3.5.2) and at the end I will provide a download link to the modifies plugin files that have been modified and released by myself.

Ok, firstly. We need to have a nice easy way to tell the sociable plugin that we want to enable bit.ly url shortening, just like we can with awe.sm at the moment. However, with bit.ly, to use their url shortening service in this way we need to have an API key and username, this is not optional. This is very straight forward, really. Open up the social.php file in your text editor of choice and find lines 1369-1376. They should look like this:

    <th scope="row" valign="top">
        <?php _e("awe.sm:", "sociable"); ?>
    </th>

    <td>
        <?php _e("You can choose to automatically have the links posted to certain sites shortened via awe.sm and encoded with the channel info and your API Key.", 'sociable'); ?><br/>
        <input type="checkbox" name="awesmenable" <?php checked( get_option('sociable_awesmenable'), true ); ?> /> <?php _e("Enable awe.sm URLs?", "sociable"); ?><br/>
        <?php _e("awe.sm API Key:", 'sociable'); ?> <input size="65" type="text" name="awesmapikey" value="<?php echo get_option('sociable_awesmapikey'); ?>" />
    </td>

Completely replace all of this with:

<th scope="row" valign="top">
    <?php _e("bit.ly:", "sociable"); ?>
</th>
<td>
    <?php _e("You can choose to automatically have the links posted to certain sites shortened via bit.ly and encoded with your API Key so you can view click stats etc....", 'sociable'); ?><br/>
    <input type="checkbox" name="bitlyenable" <?php checked( get_option('sociable_bitlyenable'), true ); ?> /> <?php _e("Enable bit.ly URLs?", "sociable"); ?><br/>
    <?php _e("bit.ly API Key:", 'sociable'); ?> <input size="65" type="text" name="bitlyapikey" value="<?php echo get_option('sociable_bitlyapikey'); ?>" /><br />
    <?php _e("bit.ly API Login:", 'sociable'); ?> <input size="65" type="text" name="bitlylogin" value="<?php echo get_option('sociable_bitlylogin'); ?>" />
</td>

If you now go into the plugins section of your wordpress admin and click on settings for the sociable plugin you should now see the option to enable bit.ly url shortening, enter a username and enter your api key. Do this now and click save.

Next. Go back to sociable.php. Go to lines 789-811, they should look like this:

    if (get_option('sociable_awesmenable') == true &! empty($site['awesm_channel']) ) {
        /**
        * if awe.sm is enabled and it is an awe.sm supported site, use awe.sm
        */
        $permalink = str_replace('&', '%2526', $permalink);
        $destination = str_replace('PERMALINK', 'TARGET', $url);
        $destination = str_replace('&amp;', '%26', $destination);
        $channel = urlencode($site['awesm_channel']);
    
        $parentargument = '';
        if ($_GET['awesm']) {
            /**
            * if the page was arrived at through an awe.sm URL, make that the parent
            */
            $parent = $_GET['awesm'];
            $parentargument = '&p=' . $parent;
        }

        if (strpos($channel, 'direct') != false) {
            $url = $sociablepluginpath.'awesmate.php?c='.$channel.'&t='.$permalink.'&d='.$destination.'&dir=true'.$parentargument;
        } else {
            $url = $sociablepluginpath.'awesmate.php?c='.$channel.'&t='.$permalink.'&d='.$destination.$parentargument;
        }
    }

Replace this entire block of code with the following:

    if (get_option('sociable_bitlyenable') == true)  {
        /**
        * if awe.sm is enabled and it is an awe.sm supported site, use awe.sm
        */
        $permalink = str_replace('&', '%2526', $permalink);
        $destination = str_replace('PERMALINK', 'TARGET', $url);
        $destination = str_replace('&amp;', '%26', $destination);

        $bitlyapikey      = get_option('sociable_bitlyapikey');
        $bitlylogin          = get_option('sociable_bitlylogin');

        $login = '&login='.$bitlylogin;
        $key = '&apiKey='.$bitlyapikey;

        $bitlyurl = 'http://api.bit.ly/shorten?version=2.0.1&longUrl='.$permalink.$login.$key;

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
    }

It's as easy as that. Save the sociable.php file and upload to your plugins/sociable folder again. Sorted. Now all url's that require shortening will be shortened using bit.ly rather than awe.sm. Not a big change, and not a big hack, but pleased me none the less. By the way, you can now also delete awesmate.php from your sociable folder.

## **[Sociable 3.5.2 Hacked Files (328k zip)](/img/posts/sociable3.5.2.zip)**
