---
comments: true
date: 2010-08-20 12:29:04
layout: post
slug: codeigniter-google-map-library-and-html5-geolocation
title: CodeIgniter Google Map Library And HTML5 Geolocation
summary: Want to use some cool new HTML5 features with my Google Maps library for CodeIgniter? Look here!
wordpress_id: 125
image: 'codeigniter-google-map-library-and-html5-geolocation/google.png'
tags:
- api
- CodeIgniter
- google api
- google maps
- javascript
- jQuery
- library
- php
---

#####  CodeIgniter Google Map Library And HTML5 Geolocation

I was asked in this forum topic, [http://codeigniter.com/forums/viewthread/164367/](http://codeigniter.com/forums/viewthread/164367/), for recommendations on integration the HTML 5 geolocation functionality with this Google Maps API Library for CI. I have posted a response to that thread, but I guess I'll repeat myself here too...

There isn't actually much I can add to the library itself but to do it you need to add the following javascript to your html page. I use jQuery so in jQuery I would do the following...

    $(document).ready(function(){
        get_location();
    });

    function get_location() {
        if (Modernizr.geolocation) {
            navigator.geolocation.getCurrentPosition(register_coords);
        } else {
            // no native support; maybe try Gears?
        }
    }

    function register_coords(position) {
        var latitude = position.coords.latitude;
        var longitude = position.coords.longitude;

        // use jquery or your own preference to send the values to CI
        $.post('http://www.your_url.com/savecoords/', { latitude:latitude, longitude:longitude }, function(){
            // some optional callback
        });
    }

The savecoords controller would then look like the following...

    $latitude = $this->input->post('latitude');
    $longitude = $this->input->post('longitude');

    $this->load->library('GMap');
    $this->gmap->GoogleMapAPI();

    // valid types are hybrid, satellite, terrain, map
    $this->gmap->setMapType('hybrid');

    //Set Mobile Parameters
    $this->gmap->mobile = true;
    $this->gmap->width = "100%";
    $this->gmap->height = "100%";

    $this->gmap->addMarker($longitude,$latitude);

    $this->gmap->disableSidebar();

    $data['headerjs'] = $this->gmap->getHeaderJS();
    $data['headermap'] = $this->gmap->getMapJS();
    $data['onload'] = $this->gmap->printOnLoad();
    $data['map'] = $this->gmap->printMap();

    $this->load->view('template',$data);

I hope this helps you in some small way.
