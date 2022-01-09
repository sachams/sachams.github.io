---
layout: post
title: Processing diasend CGM and insulin data
date: 2014-04-21 00:00:00 +0000
description: 
img: diasend.png
tags: [Diabetes]
---
As part of my project to correlate exercise and insulin usage in type 1 diabetes I need to get hold of my blood glucose and insulin usage data. I use an [insulin pump](http://www.animascorp.co.uk/animasVibe) with an embedded [continuous glucose monitoring](http://www.animascorp.co.uk/animasVibe/animas-vibe-and-cgm-system) (CGM) sensor. Periodically I upload all the data from the pump to [Diasend](http://www.diasend.com/en). Diasend is quite a nice site – it allows me to upload all my diabetes data and share it with my clinician at Guys Hospital. I can extract all sorts of reports from the site too, making it possible to review my glucose levels and insulin usage.

You can download all data as an Excel file, but for further processing it would be most convenient in CSV format. So I used [Apache POI](http://poi.apache.org/) to write a Java utility to turn the Excel documents into CSV files. I’ll upload the code to GITHub later. Apparently Diasend are bringing out API access later this year – this will make data access a bit more straightforward.

Combined with the heart rate data, I now have everything I need to start looking for correlations between exercise and insulin usage/blood glucose levels. More soon!