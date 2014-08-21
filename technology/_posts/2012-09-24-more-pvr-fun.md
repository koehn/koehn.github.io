---
layout: techpost
title: More PVR Fun
tags: raspbmc raspberrypi mythbuntu mythtv
---

I've been pretty impressed with the performance of the [RaspberryPi](http://www.raspberrypi.org/) as a digital TV endpoint. Using off-the-shelf distros like [RaspBMC](http://www.raspbmc.com/), the Pi can download and display standard-def and 720P HDTV video with few hiccups. It still cannot handle 1080p HD-TV (even with the MPEG-2 license installed) and so isn't _quite_ ready for prime time. But it's awfully close. RC5 of RaspBMC promises to help with performance and might be enough to get full HD video.

I decided to set up a PVR in the house to manage the three tuners on my HDHomeRun Prime, and to record and transcode video. A friend helped me configure a custom system at a local [PC shop](http://microcenter.com/) onto which I installed [MythBuntu](http://www.mythbuntu.org/), a [MythTV](http://www.mythtv.org/) Linux distro. I ended up with the following hardware:

*   FX 4100 Black Edition 3.6GHz Quad-Core Processor
*   GA-78LMT-S2P Socket AM3+ 760G mATX AMD Motherboard
*   8GB DDR3-1333 (PC3-10666) Enhanced Latency Dual Channel Desktop Memory (Two 4GB DIMMs)
*   2TB Barracuda SATA 3.5" Internal Hard Drive
*   Elite 430 Mid Tower Computer Case
*   430 Watt ATX Power Supply

All that set me back about $300 after taxes and rebates. It took about thirty minutes to assemble it all (not bad for a first-timer) and another twenty to get Mythbuntu installed (largely because I didn't install a CD-ROM drive). Once configured it doesn't need a monitor/keyboard/mouse for anything and you can easily access it using SSH, VNC, etc.

Once the base system was up and running I needed to configure Mythbuntu to play nice with the HDHomeRun Prime. Mostly this involved following instructions on [MythTV's wiki](http://www.mythtv.org/wiki/Silicondust_HDHomeRun_Prime). An important thing to note is that in order to get MythTV to tune the HDHomeRun Prime (and get TV schedule data) you **must** have an account on [Schedules Direct](http://schedulesdirect.org/), which costs $25/year. It's a bargain, believe me: I wrote an app to get the channel info from the Prime itself and just that was a PITA, to say nothing of schedules.

Back on the Pi, I can configure it to access MythTV using the [myth://](http://wiki.xbmc.org/?title=MythTV "MythTV") protocol. From there I can access recordings and Live TV. To set up recordings I still need to use the web, but a PVR front-end for RaspBMC and MythTV is coming soon.
