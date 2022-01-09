---
layout: post
title: Time crunched cyclist - the technology
date: 2014-08-24 00:00:00 +0000
description: 
img: tcc-technology.png
tags: [Diabetes]
---
This wouldn’t be a blog about technology without a thorough discourse on the technology involved. But before going through the design spec, let’s take a look at the user requirements:

* Only capture information once and automate as much as possible
* See calorie intake and calorie expenditure side-by-side to ensure I was eating correctly (after a long session I find it hard to eat enough food)
* Ability to plan out my sessions in advance on a calendar
* Have the training sessions show up on the calendar I use to schedule other things, to make sure I don’t double-book myself
* Make all training data easily available for analysis, both in a graphical UI and also the raw data for offline number crunching
* Capture heart rate and power data

After a bit of thinking I came up with the ecosystem above. I’m fairly happy with it apart from the Wattbike data upload – but more on this later.

## Scheduling
I use a premium edition of [TrainingPeaks](http://home.trainingpeaks.com/) to schedule my sessions. The sessions are things like 75-90 mins at Endurance Miles power (for me this is 184W), with three 10 minute intervals at Steady State power (for me this is 275W) and 5 mins recovery between each interval. There are a dozen or so sessions with different interval variations, so to make it easier to identify them, I enumerated them and assigned codes to each session. Here’s a subset of them:

* SS1 60-90 60-90 min EM with 3 x 10 min SS (5 min RBI)
* SS2 60-90 60-90 min EM with 3 x 8 min SS (5 min RBI)
* SS3 75-90 75-90 min EM with 3 x 12 min SS (6 min RBI)

I created standard workouts in TrainingPeaks called (eg) SS1 60-90, which I can drag onto the calendar to schedule sessions. The TrainingPeaks calendar has an iCal feed, which means my training appears in my normal iPhone calendar.

## Interval Timer
[Seconds Pro](http://www.secondsapp.com/) is a really neat iPhone app for creating timer-based workouts. It’s very flexible and allows you to create all sorts of sessions. I created sessions for all the workouts, indexed by code, with the power I have to work at for each interval. It means I can check my calendar to get the workout code I’m doing, start the workout in Seconds Pro, and follow the timings and power.

## Outdoor training
I ride a [Trek Domane 4.3](http://www.trekbikes.com/int/en/bikes/road/endurance_race/domane_4_series/domane_4_3/). It’s a sportive bike with a neat flexible coupling at the seat post which makes it very comfortable over long days. It lacks a bit of zip but at the moment it does me just fine.

I use a Garmin Edge 500 to record data from my rides. Although in this HD touchscreen day and age it does look a bit like a handheld Donkey-Kong game circa 1985, it does everything I want it to, and the battery lasts for ever. Once you get used to it, the navigation feature works quite well. It won’t allow you to Google the nearest bike-friendly cafe but you can navigate all day without completely hosing your iPhone battery. I think the more recent Edge 510 might automatically sync with your phone via Bluetooth, which looks quite nifty. One less manual step to do.

## Indoor training
When I’m training inside I use a [Wattbike](http://wattbike.com/uk/). WattBikes are like static bikes you get at the gym, but they measure a lot more. You can record cadence, speed, heart rate, and crucially, power – not just average power but instantaneous power at different parts of the pedal stroke, which is very useful for pedal stroke analysis.

As most of the interval sessions are very prescriptive of the power and duration of the workout, I found it much easier to do the interval sessions on the Wattbike – even if I had a power meter on my bike it would be hard to stick to 275W for 10 mins if I was on the road due to traffic light and other road users.

If I’m doing a Wattbike session, I record the sessions on a USB stick in the back of the Wattbike. (You can get the Wattbike to transmit power data over ANT+ and log it using your Garmin, but I found that if someone else is using a Wattbike and is also transmitting power data, the Garmin detects multiple transmitters and fails to log any data at all. I gave up on this route after a while). Once you have finished training, the next bit is messy. In order to upload the training data from the USB stick to TrainingPeaks, you have to use the [WattBike Expert software](https://wattbike.com/uk/wattbike/expert_software). This only works on PCs, and is a bit fiddly to use. If like me you are Mac-based, having to fire up a rusty old Windows laptop to upload data using fiddly software is highly annoying. But regardless, once done, the training data appears associated with the session you scheduled in TrainingPeaks.

For long endurance sessions on the Wattbike, Breaking Bad provides ample distraction. Go Heisenberg!

## Heart Rate Monitoring
I use the basic HR strap that came with my Garmin. It works fine, and connects via ANT+ to the Wattbike and Garmin.

## Synchronisation Tools
[Tapiriik](https://tapiriik.com/) synchronises data from Strava to TrainingPeaks. It works pretty well, and costs $2 a year, which is a bargain. I have also been using [SyncMetrics](http://blog.syncmetrics.com/home/) to sync FitBit Aria weight and body fat data with TrainingPeaks (it’s meant to be able to sync Strava with TrainingPeaks, but this doesn’t seem to work) but today I checked the website and apparently the system is down for maintenance for a while, which doesn’t look very promising.

The Garmin syncs to [Garmin Connect](http://connect.garmin.com/en-GB/) which then syncs with Strava and thence to TrainingPeaks, so all my ride data ends up in both Strava and TrainingPeaks.

## Weight, diet and calorie balance
As soon as I get up I weigh myself. Not every day, but when I do weigh myself, I do it at the same time each day. I use a [FitBit Aria](http://www.fitbit.com/uk/aria) scale, which also measures body fat percentage. This syncs automatically with the FitBit website, which then syncs with [MyFitnessPal](http://www.myfitnesspal.com/). All my ride data ends up in Strava, and as this syncs with MyFitnessPal as well, I can use MyFitnessPal to monitor weight, body fat, calories in and calories out.

## Post-ride Analysis
After each season I upload Garmin or Watrbike data to TrainingPeaks and take a look at the results and make a few notes about the session. First thing I chez is whether I have hit the correct average power for the session, and if not, make a mental note to push it a bit harder next time. If I crashed and burned (metaphorically, that is) and couldn’t compete the session, I would look to see if I had not given myself enough recovery time and look to change upcoming sessions. I also note down my carb intake and how my glucose levels faired before, during and after the session, and think about whether i should change my basal insulin rate.

Having all the exercise data in Strava makes it easy to download the raw numbers and crunch them using R (see my other blog posts). I do this as part of a project to explore the relationship between basal insulin rate and exercise.

_Disclaimer: I do not currently receive any cutting-edge electronics or bikes to test. Should you wish to send me some kit, please feel free._