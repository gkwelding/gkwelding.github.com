---
comments: true
date: 2010-02-07 16:03:40
layout: post
slug: codeigniter-cache-helper
title: CodeIgniter Cache Helper
summary: CodeIgniter Cache Helper
wordpress_id: 77
image: placeholder.png
tags:
- clients
- CodeIgniter
- exciting
- freelance
- new beginning
- optimisation
- php
- Plugins
- tips
---

#####  CodeIgniter Cache Helper

Whilst working on a project this weekend I came across the need to be able to delete a CodeIgniter cache file for a specific page at the instance of a database INSERT/UPDATE/DELETE. Surprisingly there is no other way of doing this than finding the cache file itself in the file system and deleting it manually. Kind of sucks really.

Not surprisingly I decided to fix this little oversight. I have attached to the bottom of this post a link to a file containing a helper (this goes into you system/helpers directory) that will allow the easy deleting of cache pages from the CodeIgniter cache.

There are two ways this helper can be used once it has been loaded. To load the helper you either need to add the word 'cache' to your autoload.php file in the helpers array, or you need to call '$this->load->helper('cache');'.

Once you have done this you will have access to 1 extra function, yes, only 1... Get over it. This function is called, wait for it, delete_cache(). However, delete_cache() can be called in 2 separate ways.

**1st way:** If you want to delete the cache for the current page then in your controller file just call 'delete_cache();' this is all you need to do to delete the cache file for the current page.

**2nd way:** If you want to delete the cache file for another page, or for more than one page then you need to do the following.

    <?php
    $pages = array(
                    '/cms/page1',
                    '/cms/page2',
                    '/cms/page3',
                    '/cms/page4',);
    delete_cache($pages);

It has to be the full URL to the page as CodeIgniter creates a cache file name that is the md5 hash for the full path to the page. A dynamic way of writing the paths above would be as follows (this allows you to change your site's base path without having to go through and change all of the calls to delete cache files).

    $base = $this->config->item('base_url').$this->config->item('index_page');
    $pages = array(
                    $base.'/page1',
                    $base.'/page2',
                    $base.'/page3',
                    $base.'/page4',);
    delete_cache($pages);

As you can see it also creates much more compressed, clean code.

Enjoy people.

## [CODEIGNITER CACHE HELPER (2kb zip)](/img/posts/cache_helper.zip)
