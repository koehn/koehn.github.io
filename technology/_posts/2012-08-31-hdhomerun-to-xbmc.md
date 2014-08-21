---
layout: techpost
title: HDHomeRun to XBMC
---

I've purchased a [Raspberry Pi](http://www.raspberrypi.org/) and installed an [XBMC](http://www.xbmc.org/) [distro](http://www.raspbmc.com/) on it. So far I love it: my family can easily get to a variety of media with a minimum of effort. I even [bought a license](http://www.raspberrypi.com/license-keys/) to enable on-board MPEG-2 decoding in hardware. 

I also bought an [HDHomeRun Prime](http://www.silicondust.com/products/hdhomerun/prime/), which is basically a box with a cable TV input, three cable tuners, and an Ethernet interface. There's a straightforward command-line interface to tune a tuner to a particular channel, and receive an MPEG-2 stream containing whatever that tuner tunes in. It turns out that digital cable is simply a series of MPEG-2 streams, so the device doesn't need to do all that much work.

XBMC knows about the HDHomeRun, and, through a [fairly kludgy interface](http://wiki.xbmc.org/index.php?title=HDHomeRun "HDHomeRun"), can tune a channel and display the results. But for one reason or another, it cannot keep up with an HD stream coming from the HDHomeRun Prime, even the Pi’s MPEG-2 hardware decoder enabled. 

So I've started looking at alternate ways to get the data to the Prime in a way that it can consume it. Here's what I've come up with so far:

1.  Have the Pi send a message via HTTP to my MacBook Pro when it wants to tune a channel. The message only needs to contain the channel it wishes to choose; the MacBook will handle tuner allocation.
2.  Have the MBP find an available tuner and use the HDHomeRun command line tool to tune it to the appropriate channel.
3.  Have the MBP use the HDHR command line tool to get an MPEG-2 stream from the tuner and send it to ffmpeg.
4.  Have ffmpeg transcode the MPEG-2 to H.264 and output the result to an RTSP server (running on ffserver).
5.  Return an HTTP response to XBMC indicating the URL over which to get the H.264-encoded stream.&nbsp;If another tuner is already tuned to the channel that the Pi wants to watch, simply return the RTSP of that tuner. Might need multicast to achieve this. Also, the H.264 settings will need to be tweaked to optimize (read: downgrade) the stream to the point where the Pi can consume it.

I don't know if this is feasible at all, but I'll start poking around with it. Maybe around the time I'm done somebody on the RaspBMC team will release a patch enabling the Pi to stream the HD MPEG-2 streams directly from the HDHomeRun Prime. 