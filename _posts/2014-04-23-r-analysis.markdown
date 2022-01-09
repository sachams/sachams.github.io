---
layout: post
title: Analysing heart rate and diabetes data using R
date: 2014-04-23 00:00:00 +0000
description: 
img: r-project.png
tags: [Diabetes]
---
At the start of the project I thought I would be spending all of my time using Hadoop and other Big Data technologies to analyse my data. The conclusion that I rapidly came to is that if you don’t have huge amounts of data then Hadoop is probably not the best option. Once I have a better idea about what functions I want to run on my data I’ll come back to Hadoop as it is a fun technology to experiment with, but for the initial analysis I need something a bit more flexible and interactive.

A colleague mentioned R. It describes itself as “a free software environment for statistical computing and graphics” – sounds perfect. I like free. It was very easy to get started with, both on a Mac and on Linux. It is slightly confusing to work out how to make it do things, but it’s not too bad. My approach is to end up with CSV files containing the following summarised data for each day:

* Mean blood glucose level
* Std Dev of blood glucose level readings
* Number of glucose readings above and below a threshold
* Total bolus per day
* TRIMP calculated using [exponential method](http://fellrnr.com/wiki/TRIMP#TRIMPexp_Exponental_Heart_Rate_Scaling)
* TRIMP calculated using [total duration method](http://fellrnr.com/wiki/TRIMP#Training_Volume)

After a couple of nights figuring things out I came up with a set of R scripts to do this. R is pretty cool for king ad-hoc analysis, but I’m not familiar enough with it to build a robust system – if there are any errors processing the input files it tends to bomb out with an obscure and hard-to-diagnose error message. Again, I’ll add the scripts to GitHub as soon as I can.

Now that I’ve finally got some data to play with, it’s time to do some analysis!