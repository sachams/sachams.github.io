---
layout: post
title: Quantifying exercise - continuous heart rate monitoring
date: 2014-04-17 00:00:00 +0000
description: 
img: biopatch.jpeg
tags: [Diabetes]
---
One part of The Glucose Project is to try and quantify exercise so that it can be correlated with insulin usage and blood glucose level. The question I want to answer is, depending on the amount of exercise I have done, how should I adjust my insulin dose?

My first approach is to look at heart rate data logged during exercise and somehow quantify it. There are a number of methods of doing this, most falling under the banner of TRIMP (TRaining IMpulse). [This site](http://fellrnr.com/wiki/TRIMP) has a nice summary of popular methods. I’m going to use two methods – total duration and TRIMP exp (i.e., exponentially weighted heart rate times duration).

To do this I need to capture my heart rate. A bit of Googling revealed the following options:

|OPTION|PROS|CONS|
|[Basis B1 watch](http://www.dcrainmaker.com/2013/07/basis-b1-review.html)|Logs heart rate 24×7 as well as a lot of other metrics|Doesn’t work very well when exercising; data is hard to extract for offline analysis|
|[Mio Alpha](http://www.dcrainmaker.com/2013/02/monitor-bluetooth-smartant.html)|Works while exercising; is ANT+ compatible so can replace any other HRM sensor so you can upload your workouts directly to (e.g.) Strava|Doesn’t do 24×7 monitoring|
|[True Sense](http://op-innovations.com/en/TSKdesc)|Small; low-cost; looks very interesting; not 24×7 but with two of them you could get continuous coverage|Fairly experimental – would need a lot of work to productionise|
|[Actiheart](http://www.camntech.com/products/actiheart/actiheart-overview)|Looks really cool – just the ticket|Very expensive (>$1500)|
|[BioPatch](http://www.zephyranywhere.com/products/biopatch/) and [BioHarness](http://www.zephyranywhere.com/products/bioharness-3/)|Also looks pretty awesome|Also very expensive 😦|
|[Garmin ANT+ heart rate strap](http://www.amazon.co.uk/exec/obidos/ASIN/B0029M3NSS/dcraicom-21)|Cheap, reliable|Not 24×7|

I’m going to start by using the Garmin HRM strap – I’ve got one already and it works pretty well. Although it isn’t 24×7, it’s only really the periods of exercise that I am interested in, so this should be sufficient to investigate correlation of exercise and insulin usage. I’d love to come back later and investigate the True Sense products as they look really interesting.

Next job is to look at how to analyse the heart rate data.