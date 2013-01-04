---
comments: true
date: 2010-08-03 09:15:52
layout: post
slug: google-map-library-for-codeigniter-example-usage-update
title: Google Map Library For CodeIgniter Example Usage Update
summary: Ok, a little update the to how to's for the new Google maps library. Including; directions, geolocated RSS feeds, KML overlays and maps for mobile.
wordpress_id: 122
image: 'google-map-library-for-codeigniter-example-usage-update/google.png'
tags:
- api
- CodeIgniter
- google api
- google maps
- library
- php
---

#####  Google Map Library For CodeIgniter Example Usage Update

Ok, a little update the to how to's for the new Google maps library.

##### # Directions? No problem...

    <?php 
    $this->load->library('GMap');
    $this->gmap->GoogleMapAPI();

    // valid types are hybrid, satellite, terrain, map
    $this->gmap->setMapType('hybrid');

    $this->gmap->addDirections("Some Street, Some Town, Some City, Some Country", "57 Cardigan Lane, Leeds, UK", 'map_directions', $display_markers=true);

    $this->gmap->disableSidebar();

    $data['headerjs'] = $this->gmap->getHeaderJS();
    $data['headermap'] = $this->gmap->getMapJS();
    $data['onload'] = $this->gmap->printOnLoad();
    $data['map'] = $this->gmap->printMap();
     
    $this->load->view('template',$data);

You would then modify the template file from before to look like this...

    <?php echo $headerjs; ?>
    <?php echo $headermap; ?>


    <?php echo $onload; ?>
    <?php echo $map; ?>
    <div id="map_directions"></div>

Geo located RSS feeds? No problem...

    <?php
    $this->load->library('GMap');
    $this->gmap->GoogleMapAPI();

    // valid types are hybrid, satellite, terrain, map
    $this->gmap->setMapType('hybrid');

    $this->gmap->addKMLOverlay('http://api.flickr.com/services/feeds/geo/?g=322338@N20〈=en-us&format;=feed-georss');

    $this->gmap->disableSidebar();

    $data['headerjs'] = $this->gmap->getHeaderJS();
    $data['headermap'] = $this->gmap->getMapJS();
    $data['onload'] = $this->gmap->printOnLoad();
    $data['map'] = $this->gmap->printMap();
     
    $this->load->view('template',$data);

You would then modify the template file from before to look like this...

    <?php echo $headerjs; ?>
    <?php echo $headermap; ?>

    <?php echo $onload; ?>
    <?php echo $map; ?>

A KML overlay on your google map? ok...

    <?php
    $this->load->library('GMap');
    $this->gmap->GoogleMapAPI();

    // valid types are hybrid, satellite, terrain, map
    $this->gmap->setMapType('hybrid');

    $this->gmap->addKMLOverlay('http://gmaps-samples.googlecode.com/svn/trunk/ggeoxml/cta.kml');

    $this->gmap->disableSidebar();

    $data['headerjs'] = $this->gmap->getHeaderJS();
    $data['headermap'] = $this->gmap->getMapJS();
    $data['onload'] = $this->gmap->printOnLoad();
    $data['map'] = $this->gmap->printMap();
     
    $this->load->view('template',$data);

You would then modify the template file from before to look like this...

    <?php echo $headerjs; ?>
    <?php echo $headermap; ?>

    <?php echo $onload; ?>
    <?php echo $map; ?>

A map suitable for a mobile device? Hmmm.... Alrighty then...

    <?php
    $this->load->library('GMap');
    $this->gmap->GoogleMapAPI();

    // valid types are hybrid, satellite, terrain, map
    $this->gmap->setMapType('hybrid');

    //Set Mobile Parameters
    $this->gmap->mobile = true;
    $this->gmap->width = "100%";
    $this->gmap->height = "100%";

    $this->gmap->addMarkerByAddress("Some Street, Some Town, Some City, Some Country","Marker Title", "Marker Description", $tooltip="", $filename="");

    $this->gmap->disableSidebar();

    $data['headerjs'] = $this->gmap->getHeaderJS();
    $data['headermap'] = $this->gmap->getMapJS();
    $data['onload'] = $this->gmap->printOnLoad();
    $data['map'] = $this->gmap->printMap();
     
    $this->load->view('template',$data);

You would then modify the template file from before to look like this...

    <?php echo $headerjs; ?>
    <?php echo $headermap; ?>

    <?php echo $onload; ?>
    <?php echo $map; ?>

Geocoding...

    <?php
    $this->load->library('GMap');
    $this->gmap->GoogleMapAPI();

    // this method checks the cache and returns the cached response if available
    $geocodes = $this->gmap->getGeoCode("Some Street, Some Town, Some City, Some Country");

    // this method bypasses the cache and returns the full xml object from google
    $geocodes_full = $this->gmap->geoGetCoordsFull("Some Street, Some Town, Some City, Some Country");

If you want to change the default icon that google maps uses without specifying it every time you add a marker then do this...

    <?php
    $this->gmap->setMarkerIcon("some_default_icon.png");
