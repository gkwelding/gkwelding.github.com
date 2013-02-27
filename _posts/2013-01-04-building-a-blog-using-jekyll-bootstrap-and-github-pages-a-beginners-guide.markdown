---
comments: true
date: 2013-01-04 12:55:00
layout: post
slug: building-a-blog-using-jekyll-and-github-pages
title: Building a blog using Jekyll, Bootstrap and Github pages. A beginners guide!
summary: An article about how I migrated away from a self hosted Wordpress blog. A wonderful tale of building a blog using Jekyll, Bootstrap and Github pages in 4 evenings and subsequently removing all of my expenditure on server costs and any worries about scalability.
image: 'building-a-blog-using-jekyll-and-github-pages/wp_github_jekyll.png'
tags:
- Jekyll
- Github
- Technology
- Blog
---

#####  An article about how I migrated away from a self hosted Wordpress blog. A wonderful tale of building a blog using Jekyll, Bootstrap and Github pages in 4 evenings and subsequently removing all of my expenditure on server costs and any worries about scalability.

First some background. My blog isn't popular by any stretch of the imagination. 
I have a few articles that are very popular though and they get a load of traffic. 
[Teaching my 5 year old daughter to code...](/2012/10/04/teaching-my-5-year-old-daughter-to-code/) 
and anything related to my Google Maps library for CodeIgniter draw in enough 
traffic that I had to have an Amazon EC2 micro instance and a separate micro RDS 
instance running constantly. This was all fine and the costs associated were 
easily affordable. The blog was a Wordpress blog, and this really bothered me. I 
felt like I was more of a plug-in manager than a developer. I found myself 
installing plug-in after plug-in to solve interesting problems such as social 
sharing, caching, and responsive design. This may be great for most people but 
it made me deeply unhappy with my blog.

This is when I started the search for an alternative. My original plan was never 
to close down my Amazon instances. I was initially looking for a light-weight 
blogging platform that supported a NoSQL database such as Mongo or Couch. What I 
really wanted was the above but with a decent integration into something like 
ElasticSearch or Solr. I threw all of these requirements out of the window when I 
read about Jekyll and Github pages. Instead I decided to focus on another area 
that deeply interested me. Responsive design, blisteringly quick page load 
times, and massive scalability.

For those of you who don't know what Jekyll is here's a quote from the 
[Jekyll Github page](https://github.com/mojombo/jekyll).

> _Jekyll is a simple, blog aware, static site generator. It takes a template directory (representing the raw form of a website), runs it through Textile or Markdown and Liquid converters, and spits out a complete, static website suitable for serving with Apache or your favourite web server. This is also the engine behind GitHub Pages, which you can use to host your project's page or blog right here from GitHub._

Jekyll is written in Ruby (I'm primarily a PHP developer so this was also a 
great opportunity to get my hands on another language) and basically converts 
markdown to be used in HTML templates and the Liquid templating engine. The 
resulting output is static HTML files. No _dynamic content_ in the usual sense 
of the word. As great as this is it does also pose a few problems, which I will 
also address in this article.

##### Getting started with Windows

I work via SSH and the command line on my Linux servers, I always have and 
always will. I have worked on large scale websites that run on Windows Server 
and I despise it, I felt dumber every time I used a GUI to administer a web 
server. However, my primary development environment is a Windows 7 laptop. 
Thankfully Ruby and Jekyll are really easy to setup and run even on Windows.

By far the easiest thing to do is go to 
[http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/) 
and download the latest version of Ruby (when I wrote this the latest stable 
version was 1.9.3-p362) and the Development Kit (you'll need this for installing 
Ruby Gems). Run the Ruby installer first followed by extracting the development 
kit. Once you've done that you need to go to `Start > All Programs > Ruby > Start Command Prompt With Ruby`. 
Once inside to command prompt navigate to your development kit installation. I 
extracted mine to C:\DevKit so I did `cd C:\DevKit`. Once in here run the 
following `ruby dk.rb init` and then `ruby dk.rb install`. You should now be set 
to go with gems in Ruby! `gem install jekyll` is all it should take. You're now 
good to go with a full Ruby and Jekyll install on your windows system!

##### Setting up your Github repository

If you nip over to [https://github.com/gkwelding](https://github.com/gkwelding) 
you will see, in there, exists a repository called gkwelding.github.com. That 
single repository is all that is needed to run github pages. Anything you now 
push to this repo will be parsed by Jekyll and Liquid and spat out as a rendered 
HTML page. You can simulate this process locally for testing and development.

As a starting point I would recommend cloning my github repository for 
[gkwelding.github.com](https://github.com/gkwelding/gkwelding.github.com). 
You can clone this to whatever directory you want, but I cloned mine to 
C:\gkwelding.github.com. Then go to `Start > All Programs > Ruby > Start Command Prompt With Ruby` 
and browse to the directory where you just cloned the repository to, 
`cd C:\gkwelding.github.com`. Now as you're in this directory run the following 
command `jekyll --server`. That's it. You'll see some output fly past and then 
you're ready to go. Head to your favourite browser and go to http://localhost:4000. 
You should now see a local version of this blog, complete with posts. This is 
basically all Github pages does every time you push, it runs the Jekyll server 
once to regenerate the static content, and then just serves up the static HTML 
files to the end user.

##### Credit where credit is due

I'm going to get this out of the way now before going into any more detail. My 
journey through the Jekyll universe has been made easier by a couple of sites in 
particular and some of what I post here may just be a re-hash of stuff from them. 
These sites are:

- [http://jekyllbootstrap.com/](http://jekyllbootstrap.com/)
- [http://erjjones.github.com/blog/How-I-built-my-blog-in-one-day/](http://erjjones.github.com/blog/How-I-built-my-blog-in-one-day/)
- [http://alexpearce.me/2012/04/simple-jekyll-searching/](http://alexpearce.me/2012/04/simple-jekyll-searching/)
- [http://developmentseed.org/blog/2011/09/09/jekyll-github-pages/](http://developmentseed.org/blog/2011/09/09/jekyll-github-pages/)

##### Getting a basic format that I liked

I tried using [http://jekyllbootstrap.com/](http://jekyllbootstrap.com/) as it 
looked pretty well written and fairly feature complete. However, it seems to be 
a little out of date and didn't seem to play nice with Bootstraps Glyphicons, 
it did some really odd repetition stuff that I couldn't fix. That's when I 
stumbled on Eric Jones' blog and post about building his blog in Jekyll. I 
decided to use his blog as a starting point for mine. I stripped out all of the 
random templates and stuck to just layout.html. I removed some of the JS 
duplication, cleared up some of the includes, removed ALL of the layouts that 
had been built using **TABLES**, removed the dependency on docs.css and much 
much more.

The most significant part for me was moving out so much of the hard coded 
nonsense that had crept in to Erics project. I have replaced it with a _config.yml 
file instead. Hopefully this should make the initial setup of a clone of this 
project much much easier for anyone wanting to use it.

I learnt some very useful things along the way about Jekyll and Liquid, these 
were summed up perfectly in Development Seed's blog post on Jekyll Github Pages.

> _Jekyll follows four simple rules when converting your source into a website:_
> 
> - _Any file in the source directory is copied directly into the site directory._
> - _Unless the file that has a YAML header. These files can make use of the Liquid templating language._
> - _Unless the file is in _posts. These files build up a data object representing all of your site's content that can be referenced when templating._
> - _Posts can specify a permalink to generate a page at a different location than where the post resides in the source directory._
> 
> _Once you get the hang of these four simple rules you can do some surprising things._

This is so so true, the last line in particular. I use these rules when creating 
the search.json file later on.

##### Writing posts

Writing posts couldn't be easier, as long as you know markdown and have an Iq higher 
than 60. The full syntax list can be found at [http://daringfireball.net/projects/markdown/syntax](http://daringfireball.net/projects/markdown/syntax). 
the best way to learn about writing posts is to go and look at examples. There's 
numerous examples in the source code for this site. The YAML header contains some 
basic information, the slug for the post, the title and summary, date and tags etc... 
Nothing complex or unusual. One thing I have done that is slightly different is 
the `comments: true` parameter. This allows you to turn off the comments for a 
particular post

##### Shit, what about comments?

That brings me on to my next section quite nicely. Shit, comments. This is a blog 
after all and user contribution is critical to me. However, static HTML files don't 
hosted on Github pages don't really lend themselves well to dynamic content such 
as comments. [Disqus](http://disqus.com/) to the rescue! The templates for posts 
contain the necessary JavaScript snippets to provide the articles with a lovely 
comment system provided by Disqus.

##### Migrating from Wordpress

The single most difficult part of the entire process was getting my posts out of 
Wordpress, comments and all, and importing them into a usable Jekyll format. None 
of the Wordpress to Jekyll plugins work on the newer versions of Wordpress. Instead 
I happened upon a lovely python script called [exitwp](https://github.com/thomasf/exitwp). 
Just follow the instructions and all will be good with the world!

For me it was a case of cloning this repo onto my Ubuntu box. Taking an export of 
ALL of my Wordpress data using the built in Wordpress export tool (you will also 
need this for Disqus), popping it into the necessary ExitWP folder and running 
the script. so beautifully simple.

Disqus are legends too. The export you took for ExitWP works a treat there too. 
Just import the full XML file and give Disqus 24 hours to do their magic.

##### Social interaction

Social interaction was a doddle too. Being static HTML files meant I could just 
use the standard widget provided by the likes of Twitter and Google.

##### Custom domain name

A big issue for me was my domain name and existing links. I was able to keep my 
perma-link structure the same which is nice, but I didn't want my URL changing 
to gkwelding.github.com. I'd had the in-the-attic.co.uk domain for years and years 
and had just recently managed to acquire the .com after many years of watching it 
sit idle in the hands of someone else. Github know this. they have provided a super 
easy method to let you use your own domain.

Create a CNAME file in the top level of your github repository for your site. In 
my CNAME file you will see it just contains in-the-attic.com. That's all it needs. 
Follow the advice at [https://help.github.com/articles/setting-up-a-custom-domain-with-pages](https://help.github.com/articles/setting-up-a-custom-domain-with-pages) 
for how to set up your DNS, however, as an example mine now looks like this:

    @       A 204.232.175.78
    www     A 204.232.175.78
    www     C gkwelding.github.com

And that's it. Give your DNS time to update and away you go.

One thing about this is you can only have one TLd pointing to your Github page. 
This was a problem for me because I've used the in-the-attic.co.uk domain for years. 
All of my traffic comes through the .co.uk domain, but i now wanted to use the .com 
domain for various reasons. I'd already set up all the 301 redirects on the .co.uk 
domain and I had to piggy back on a server I ran for other clients. I pointed my .co.uk 
domain there and redirected via HTACCESS to the .com, URI string and all.

For those interested the code in the .htaccess is as follows:

    RewriteEngine On
    RewriteBase /

    RewriteCond %{HTTP_HOST} ^(www\.)?in-the-attic\.co\.uk$ [NC]
    RewriteRule ^(.*)$ http://www.in-the-attic.com/$1 [R=301,L]

##### Combined CSS and JS

Short of manually combining the CSS and JS I could see no easy way of acheiving 
this simple optimisation technique. Until I remembered the rules above. Any file 
in the main directory is copied directly to the _site directory, **UNLESS** it has 
a YAML header (even a blank one) in which case it can make use of the Liquid templating 
engine. Queue all.css and all.js. These two files can eb found here:

[https://github.com/gkwelding/gkwelding.github.com/blob/master/css/all.css](https://github.com/gkwelding/gkwelding.github.com/blob/master/css/all.css)
[https://github.com/gkwelding/gkwelding.github.com/blob/master/js/all.js](https://github.com/gkwelding/gkwelding.github.com/blob/master/js/all.js)
    
Boom, aggregated CSS and JS. Just make sure the files you're including reside in 
the _includes folder.

##### Site search

- [http://alexpearce.me/2012/04/simple-jekyll-searching/](http://alexpearce.me/2012/04/simple-jekyll-searching/)
- [http://developmentseed.org/blog/2011/09/09/jekyll-github-pages/](http://developmentseed.org/blog/2011/09/09/jekyll-github-pages/)

These two amazing articles gave me pretty much everything I needed to create a 
pretty nifty site search. I stole the search.json idea and the underscore.js code 
for searching the JSON array and then plugged that into my own display mechanism. 
It's far from perfect and has some display bugs on the mobile, but hopefully, with time 
these features will mature and become more reliable.

##### Still to do

- My blog content isn't exactly a huge, vast library of information. However, I need to sort out a decent paging solution.
- Responsive images. Although the images resize as the browser window resizes, the quality and size of file does not change.
- Make search work on mobile. The search box size is an issue on mobile platforms and as such has been disabled for now.
- Fast scrolling between articles like on the desktop version. The fast switch buttons blocked content and UI on mobile/tablet versions.
- There appears to be an issue with JavaScript on the mobile pages. Once the page fully loads you can't scroll past the header.
- Make it look less like it was built using Bootstrap. The styles are still too Bootstrap for my liking. I love the functionality of Bootstrap, just not the overall look and feel.

##### Recommended reading

- [http://daringfireball.net/projects/markdown/syntax](http://daringfireball.net/projects/markdown/syntax)
- [https://github.com/mojombo/jekyll/blob/master/README.textile](https://github.com/mojombo/jekyll/blob/master/README.textile)
- [https://github.com/Shopify/liquid/wiki](https://github.com/Shopify/liquid/wiki)

I hope you guys enjoyed this article. Please feel free to comment below. Also, 
please feel free to use the code that powers this page for your own use. Feel 
free to modify it and expand it and contribute back to it should you feel the need to.