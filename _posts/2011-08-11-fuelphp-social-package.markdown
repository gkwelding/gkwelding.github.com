---
comments: true
date: 2011-08-11 20:18:20
layout: post
slug: fuelphp-social-package
title: FuelPHP Social Package
summary: A FuelPHP Social Package. Simples.
wordpress_id: 181
image: 'fuelphp-social-package/fuel.png'
tags:
- api
- fuelphp
- library
- optimisation
- php
- Plugins
- Sociable
- social
- social media
- tips
- work
---

#####  A FuelPHP Social Package. Simples.

I got to the point this week where I finally started work on my latest project, I'm not giving anything away just yet but stay tuned. However, a few things I decided for this project were as follows; the project should be built in FuelPHP, the project will be built with scalability in mind (memcache was installed before I'd even written a line of code), and finally I didn't want to mess around with authorisation.

The first two caveats were no problem. The final one was the issue. Mainly because I wanted all of my auth to be handled by Facebook. The intention of this project was for it to be a facebook app and a regular website all in one. As such, the only auth system I wanted to use was Facebook's. Now the problem started.

Fuel is a young framework, but and damn good one. The problem with it being young is that nothing's actually built for it yet. There's not much 3rd party stuff kicking around for a developer to use. So I decided to build something myself.

I could have gone down the Auth/Driver route but that seemed overly complicated for what I wanted. I also wasn't exactly sure how I would achieve this although I do have a better idea of that now. After doing some searching around the FuelPHP forums I happened across [Dan Horrigan](https://twitter.com/#!/dhorrigan)'s Twitter package in his scrapyd code base.

To cut a long story short I took the Facebook PHP SDK, put a wrapper around it and packaged it up along with Dan's twitter code and I'm now releasing it as a Social package for FuelPHP.

[https://github.com/gkwelding/FuelPHP-Social-Package](https://github.com/gkwelding/FuelPHP-Social-Package)

Firstly, start off with a login page. Here's one I made earlier...

[![app login](/img/posts/fuelphp-social-package/login.png)](/img/posts/fuelphp-social-package/login.png)

The href for the login button is created and assigned within the controller and roughly consists of the following:

    <?php
    /**
    * The Index Controller.
    *
    * Shows register page or logs the user in depending on app permission.
    *
    * @package app
    * @extends Controller
    */
    namespace index;
    use \Social\Facebook;
    
    class Controller_Index extends \Controller {
        /**
        * The index action.
        *
        * @access public
        * @return void
        */
        public function action_index() {
            $data= array();
            $fbl_params = array("scope" => "email");
            $data['fb_login_url'] = Facebook::instance()->getLoginUrl($fbl_params);
            $this->response->body = \View::factory('index', $data);
        }
    }

This code sits within action_index in my index controller, which is the default controller for my application.

Now the magic bit. Insite app/bootstrap.php look for the following line: Fuel::init(include(APPPATH.'config/config.php'));

This is where you're going to add your auth checks. Now, probably the best thing to do here is create a new class and have a mthod within that class that performs the check, however, because my auth check was so simple I bypassed this and added the code directly. My app/bootsrap.php file now looks like this:

    <?php
    // Bootstrap the framework DO NOT edit this
    require_once COREPATH.'bootstrap.php';
    
    Autoloader::add_classes(array(
        // Add classes you want to override here
        // Example: 'View' => APPPATH.'classes/view.php',
    ));
    
    // Register the autoloader
    Autoloader::register();
    
    // Initialize the framework with the config file.
    Fuel::init(include(APPPATH.'config/config.php'));
    
    if($_SERVER['REQUEST_URI'] == '/') {
        if(\Social\Facebook::instance()->check_login()) {
            \Response::redirect('/dashboard');
        }
    } else {
        if(!\Social\Facebook::instance()->check_login()) {
            \Response::redirect('/');
        }
    }
    /* End of file bootstrap.php */

And that my friends is that. Those few lines of code handle all of the authentication on the site. If you don't have a valid FB session you get bounced back to the index controller and the index action (Response::redirect('/')) and you have to click the login button again. Failing that you're free to go where ever you wish. In this case if you're logged in you get redirected to the page below:

[![logged in view](/img/posts/fuelphp-social-package/loggedin.png)](/img/posts/fuelphp-social-package/loggedin.png)

This process is the same for twitter too, just take a look around the package, it's really very simple. Pretty much the only major API calls my code does at the moment is `Facebook::instance()->api('/me');` to return the current user and `Facebook::instance()->api('/me/friends');` to return the current users friends list (cached in memcache by the way).

If you're stuck the only other thing I can recommend is read the docs. The Facebook and Twitter implementations here are nothing more than glorified wrapper for the development tools provided by Twitter and Facebook.
