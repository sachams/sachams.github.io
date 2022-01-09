---
layout: post
title: Accessing heart rate data
date: 2014-04-19 00:00:00 +0000
description: 
img: strava-image.jpeg
tags: [Diabetes]
---
In my last post I looked at options for recording heart rate data. I settled on using a Garmin HRM strap, linked to my Garmin Edge 500 and Garmin FR70. I use the Edge while on my bike on the road and in the gym (you can [link the Edge to a Wattbike](http://wattbike.com/uk/wattbike/2013_performance_computer/ant_connectivity/linking_your_garmin), which is pretty neat – it then records all power/heart rate/cadence data) and my FR70 watch for non-bike workouts, then I upload all the data to Strava.

There’s a “[download all data](http://engineering.strava.com/bulk-activity-export/)” function from Strava which I was planning on using to access all my data in GPX format, but I discovered one problem: if the data doesn’t have an GPS information in it (which happens if you used a static bike in a gym) then the file is empty. This is a huge blocker, as I won’t then be able to build a complete picture of my activity.

My solution was slightly more long-winded – access the data from the [Strava API](http://strava.github.io/api/). This presented a bit more of a challenge as I’m not that familiar with accessing RESTful APIs like Strava’s. I also decided to try and do it in Java, which I hadn’t used before. I’ll post the code to GIThub (which I also haven’t used before) but here’s roughly what I did:

* Registered my application with Strava (from the Setting page in Strava, there is a “MY API Application” link at the bottom left. For the application URL and Authorisation Callback Domain I just put this WordPress URL. You can actually set it to anything – the callback domain is used during the OAuth process to get permissions from Strava users to use their data. If you just want to access your own data and some other basic stuff and not use OAuth you can set it to strava.com or whatever.
* Next, you need to follow the authorisation process. Log in to Strava and then follow the steps in the flow. Note that when you initially request authorisation the redirect_uri has to match the URI you specified when you registered your application.
* The end result should be a code which you can use in your application to retrieve activity data.
* Note, you should be able to do this all programatically but I struggled a bit so I used cURL instead to get the code.

My application consists of:

* [Java OLTU client](https://cwiki.apache.org/confluence/display/OLTU/Index) for performing authentication [couldn’t quite get this working – will come back to it!]
* [Java Wink](http://wink.apache.org/index.html) for accessing the Strava API
* [Minimal JSON](http://eclipsesource.com/blogs/2013/04/18/minimal-json-parser-for-java/) library for parsing the JSON results

And to summarise its functionality:

* Connect to Strava
* Get a list of all the activities
* For each activity, download the time and heartrate streams, then merge the streams
* Save each activity as a CSV file

The end result is that I have a directory containing all the heart rate vs time data for all my activities.

So that is one aspect of the project – the other aspect is to correlate it with insulin and blood glucose data. See my next post.