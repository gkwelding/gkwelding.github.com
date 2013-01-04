---
comments: true
date: 2010-05-07 16:16:50
layout: post
slug: codeigniter-gmaps-library
title: CodeIgniter GMaps Library
summary: CodeIgniter GMaps Library
wordpress_id: 83
image: 'codeigniter-gmaps-library/google.png'
tags:
- CodeIgniter
- freelance
- google api
- google maps
- library
- php
- tips
---

#####  CodeIgniter GMaps Library

A project I completed recently was built pretty much from scratch in CI. This project required some pretty complex Google maps integration. Ok, cool I thought, I'll do a search and there'll be a great library for it in CI, there's got to be... Erm... Ok, no. So I utilised one from a project built around CI, Kohana. They had a Google maps library, but it wouldn't work in CI because they'd made some pretty fundamental changes to the way Kohana works. However, I've rebuilt the library so it works in CI and I've added in the database caching functionality as that's pretty critical to any Google maps tool, I was pretty surprised the Kohana's library didn't have one. Either way, I've given instructions on how to install it below along with some usage instructions. The files are included below as a zip file for download.

Put the contents of the config folder into your config directory, put the contents of the libraries folder into your libraries directory, and finally put the contents of the views folder into the views directory, easy. Next, run the included sql script on your MySQL database (this is necessary or else the library will fall over when it searches for cache entries).

Example usage:

    // load the library
    $this->load->library('Gmap');

    // Create a new instance of  Gmap with some default options.
    // Valid options are 'Dragging', 'InfoWindow', 'DoubleClickZoom', 'ContinuousZoom', 'GoogleBar', 'ScrollWheelZoom'
    $map = $this->gmap->init('map', array(
        'ScrollWheelZoom' => TRUE
    ));

    // Set the map center point, control size and map type
    // Valid map types are 'G_NORMAL_MAP', 'G_SATELLITE_MAP', 'G_HYBRID_MAP', 'G_PHYSICAL_MAP'
    $map->center(0, 0, 1)->controls('large')->types('G_PHYSICAL_MAP', 'add');

    // Add a custom marker icon
    $map->add_icon('tinyIcon', array
    (
        'image' => '/assets/icons/gmap_icon_1.jpg,
        'iconSize' => array('25', '25'),
        'iconAnchor' => array('6', '20'),
        'infoWindowAnchor' => array('5', '1')
    ));

    // Add a new marker
    $tag = 'In The Attic';
    $tag .= 'Tel: 07828 477 616';
    $tag .= 'Web: www.in-the-attic.co.uk';
    $tag .= 'Address: 42 Beanland Gardens, Wibsey, Bradford, West Yorkshire, United Kingdon, BD6 3PP';

    $map->add_marker('53.764243', '-1.7888458', $tag, array('icon' => 'tinyIcon', 'draggable' => true, 'bouncy' => true));

    $map->center('53.764243', '-1.7888458', 15);

    // define the variable for the view
    $data['api_url'] = $map->api_url();

    $data['map'] = $map->render();

Your view file should then have the following in it...

    <?php if(isset($map) && $api_url) { ?>
        <script src="<?php echo $api_url ?>" type="text/javascript"></script>
        <script type="text/javascript">
            <?php echo $map ?>
        </script>
        <div id="map" style="width: 600px; height: 500px"></div>
    <?php } ?>

Bingo, one Google map...

Enjoy people.

## [THIS LIBRARY IS NOW OUT OF DATE, GO TO THE V3 GITHUB PAGE INSTEAD](https://github.com/gkwelding/GoogleMapsV3CI)
