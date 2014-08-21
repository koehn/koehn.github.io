---
layout: techpost
title: 'HTPC Upgrade: solved'
---

Okay, I have the whole thing working. Nearly soup to nuts.

I had to abandon RaspBMC on the Raspberry Pi. Even heavily overclocked it was not up to the task, no matter how many things I tried. So fine.

I built a small PC to act as a front-end to my MythTV Backend Server. The machine has a  very capable CPU and is more than capable of running the frontend. Here are the specs:

*   Gigabyte GA-H61N-USB3 LGA 1155 H61 Mini ITX Intel Motherboard
*   Pentium G2120 3.1GHz LGA 1155 Boxed Processor
*   8GB DDR3-1333 (PC3-10600) Desktop Memory Kit (Two 4GB Memory Modules)
*   Vertex Plus R2 Series Series 60GB SATA 3Gb/s 2.5" Solid State Drive (SSD)
*   ISK110 VESA Mini ITX 90W 78MM Wide mini-ITX case
*   ROSEWILL| RCX-Z775-LP fan
*   MediaGate MCE USB IR RemoteThis machine is small and very nearly silent. It has plenty of processing power, an onboard MPEG-2/H.264 decoder, HDMI output, and lots of speed. It runs MythFrontend as part of the Mythbuntu distribution (as does the backend server I use). Setting up the machine was fairly easy except for the sound, which required the CPU to mix and decode the audio (not sure why yet). The machine is easy to use for anyone via the Windows MCE remote, which Mythbuntu recognized out of the box. Video is stutter-free, MythTV commercial detection works nearly flawlessly, skipping is instantaneous, and life is, in a word, good.

There are a few minor changes I need to make to consider the setup complete:

1.  As mentioned, I haven't been able to get the onboard hardware decompression to work. Intel has an open-source VAAPI driver that I cannot get to initialize correctly.
2.  The CPU is decoding the audio in software and adjusting the volume. It should pass the HDMI audio to the receiver directly but that's not working (I get a periodic static hiss). This is using about 20% of the CPU on the machine.3.  While the MCE remote works well, I'd like to get the power button on the remote to suspend and wake the computer. That shouldn't be too hard.On the whole I'm very happy. I plan to install Mythfrontend on the server I'm using for the backend now and let that drive a large TV in the basement, and use the Mini-ITX box for the TV upstairs. Then I can return the overpriced DVRs I've been renting from Comcast.  
