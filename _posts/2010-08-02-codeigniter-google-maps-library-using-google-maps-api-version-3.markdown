---
comments: true
date: 2010-08-02 22:41:42
layout: post
slug: codeigniter-google-maps-library-using-google-maps-api-version-3
title: CodeIgniter Google Maps Library Using Google Maps API Version 3
summary: A new Google Maps v3 API library for CodeIgniter including some examples.
wordpress_id: 118
image: 'codeigniter-google-maps-library-using-google-maps-api-version-3/google.png'
tags:
- api
- CodeIgniter
- google api
- google maps
- library
- php
---

#####  CodeIgniter Google Maps Library Using Google Maps API Version 3

Ok, it's finally here. My Code Igniter library using Google Maps API version 3.

Once again, the php code beghind the API isn't actually mine, kudos for that goes to the incredibly talent guys at the php-google-map-api project which can be found here... http://code.google.com/p/php-google-map-api/

I have modified their code slightly and put it in a nice, pretty CodeIgniter wrapper.

I will also be sorting out some example scripts but for now you'll just have to figure it out yourself. This library is compatible with the old style gmap cache database structure from my Google Map API version 2 wrapper. But in case you missed it the SQL to create the database should be...

    CREATE TABLE geocode_cache (
        id int(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
        lng double NOT NULL,
        lat double NOT NULL,
        query varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL
    );

Then, all you need to do is copy the GMap.php and JSMin.php files to your code igniter library directory.

A quick tutorial. To generate a very basic map, with a marker generated from an address...

    $this->load->library('GMap');

    $this->gmap->GoogleMapAPI();

    // valid types are hybrid, satellite, terrain, map
    $this->gmap->setMapType('hybrid');

    // you can also use addMarkerByCoords($long,$lat)
    // both marker methods also support $html, $tooltip, $icon_file and $icon_shadow_filename
    $this->gmap->addMarkerByAddress("Some Street, Some Town, Some City, Some Country","Marker Title", "Marker Description");

    $data['headerjs'] = $this->gmap->getHeaderJS();
    $data['headermap'] = $this->gmap->getMapJS();
    $data['onload'] = $this->gmap->printOnLoad();
    $data['map'] = $this->gmap->printMap();
    $data['sidebar'] = $this->gmap->printSidebar();

    $this->load->view('template',$data);

Your template file should look similar to the following...

    <html>
        <head>
            <title>Map Test</title>
            <?php echo $headerjs; ?>
            <?php echo $headermap; ?>
        </head>
        <body>
            <?php echo $onload; ?>
            <?php echo $map; ?>
            <?php echo $sidebar; ?>
        </body>
    </html>

This library supports almost every feature present in the new google maps api version 3 and as such is incredibly full featured, over time I will be writing tutorials on how to do certain thing using this library so please stay tuned.

#####  [CODEIGNITER GMAPS LIBRARY GITHUB PAGE](https://github.com/gkwelding/GoogleMapsV3CI)
