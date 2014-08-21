---
layout: techpost
title: DVD and BluRay ripping
tags: dvd bluray rip makemkv mythtv
---

I'm looking to move my (legally-owned) DVD and Blu-Ray media to MythTV. I'm using `makemkvcon` to get the decrypted bits off of the disc and onto my hard drive and that works OK, but outputs one or more files called `titlexx.mkv`, which I must then rename and move to the right folder in MythTV (usually `/var/lib/mythtv/videos`).

`$ makemkvcon --minlength=2400 -r --decrypt --directio=true mkv disc:0 all .`

What I'd like is some way to look up the name of the main track of the disc and make that into the filename. I can get the name of the disc using `lsdvd`, but that's pretty ugly.

I'm trying to figure out how to take the disc title (e.g., `BAND_BROTHERS_D5`) and get the name(s) of the title track(s) on the disc. I imagine this will require some kind of internet access, since the tracks themselves don't appear to have English-language titles. I've found some services that _should_ do it, but I can't find a way for them to work.
