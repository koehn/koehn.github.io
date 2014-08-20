---
layout: techpost
title: RaspBMC RC5 et al
---

Today I installed [RaspBMC RC5](http://www.raspbmc.com/2012/10/raspbmc-release-candidate-5-released/) on my Raspberry Pi. The upgrade was [a bit bumpy](http://www.raspbmc.com/2012/10/rc5-release-update/), but I got it all worked out. Also learned that the source of my poor 1080p performance probably had nothing to do with the Raspberry Pi decoding the video (MPEG-2 is decoded in hardware), and more to do with the Raspberry Pi attempting to decode the AC3 audio (which is done in software on the Pi’s relatively wimpy ARM CPU). Tomorrow I’ll hook the Pi up to my HDMI receiver and test the hypothesis. I bet it works like a charm.