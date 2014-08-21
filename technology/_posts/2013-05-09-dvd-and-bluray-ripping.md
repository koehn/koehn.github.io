---
layout: techpost
title: DVD and BluRay ripping
---

I'm looking to move my (legally-owned) DVD and Blu-Ray media to MythTV. I'm using <code>makemkvcon</code> to get the decrypted bits off of the disc and onto my hard drive and that works OK, but outputs one or more files called <code>titlexx.mkv</code>, which I must then rename and move to the right folder in MythTV (usually <code>/var/lib/mythtv/videos</code>).<br /><br /><code>$ makemkvcon --minlength=2400 -r --decrypt --directio=true mkv disc:0 all .</code><br /><br />What I'd like is some way to look up the name of the main track of the disc and make that into the filename. I can get the name of the disc using <code>lsdvd</code>, but that's pretty ugly. <br /><br />I'm trying to figure out how to take the disc title (e.g., <code>BAND_BROTHERS_D5</code>) and get the name(s) of the title track(s) on the disc. I imagine this will require some kind of internet access, since the tracks themselves don't appear to have English-language titles. I've found some services that <i>should</i> do it, but I can't find a way for them to work. 
