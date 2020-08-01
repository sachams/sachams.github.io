---
layout: post
title: Turning a Raspberry Pi into a Samsung AirPrint server
date: 2020-08-01 00:00:00 +0000
description: 
img: airprint.png 
fig-caption: AirPrint image
tags: [Raspberry Pi]
---
This is my ageing Samsung M2026W printer. I quite like it - it was cheap to buy and is cheap to run. There's loads of things I really hate about it too: it's meant to be AirPrint compatible, but the WiFi setup and drivers are so flaky that it drops out of Wifi all the time, assuming you have managed to get it set up on WiFi in the first place. And the latest Mac OSX drivers from Samsung (now HP) don't support WiFi setup at all.

A friend mentioned that he had recently got CUPS set up on his RPi and so as I love messing around with RPis and don't like throwing away things if I can help it, this could be the perfect solution.

## Balena-CUPS
The first Google led me to (balena-cups)[https://www.balena.io/blog/wifi-enable-usb-printers-with-a-raspberry-pi-and-share-it-over-your-network/]. I set this up on my RPI 3b and it looked very promising indeed! The Balena setup was very slick - a single click on the "Deploy with Balena" button worked really well.

The AirPrint-compatible server appeared, but unfortunately my venerable Samsung wasn't one of the supported printers. After trying pretty much every generic driver, the best I could find was a generic one that printed fairly well but always followed up with an error page. 6/10 for that one.

## Splix
A bit more Googling took me to (Splix)[https://openprinting.org/printer/Samsung/Samsung-M2022W] but unfortunately the PPD file was empty, despite the discount-code-like "Works perfectly" comment.

But a bit more searching led me to (this thread)[https://www.reddit.com/r/linuxadmin/comments/cvt23c/print_via_rpi_cups_with_samsung_m2026_very_cheap/]. I ssh'ed into my Balena container and installed it....and it worked perfectly!

## Containerising it
There were a few manual steps involved, so I thought I'd fork the Balena-CUPS repo and add in Samsung support - here it is:

https://github.com/sachams/balena-cups
