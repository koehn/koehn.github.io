---
layout: techpost
title: Attempting to fix audio and video
---

After reading a bunch, I'm trying a few new things to get the video and audio to use their respective hardware components:

The intel VAAPI drivers install into `/usr/lib/dri`, which isn't on the default library path. So I put a new file `/etc/ld.so.conf.d/intel-drivers` containing only the line, "`/usr/lib/dri`" (without quotes) in an attempt to get it loaded.

The audio situation has been more complicated. There are a million devices available to the ALSA framework, as shown here:

    $ aplay -l
    **** List of PLAYBACK Hardware Devices ****
    card 0: PCH [HDA Intel PCH], device 0: ALC889 Analog [ALC889 Analog]
      Subdevices: 1/1
      Subdevice #0: subdevice #0
    card 0: PCH [HDA Intel PCH], device 1: ALC889 Digital [ALC889 Digital]
      Subdevices: 1/1
      Subdevice #0: subdevice #0
    card 0: PCH [HDA Intel PCH], device 3: HDMI 0 [HDMI 0]
      Subdevices: 1/1
      Subdevice #0: subdevice #0

    $ aplay -L
    null
        Discard all samples (playback) or generate zero samples (capture)
    pulse
        PulseAudio Sound Server
    sysdefault:CARD=PCH
        HDA Intel PCH, ALC889 Analog
        Default Audio Device
    front:CARD=PCH,DEV=0
        HDA Intel PCH, ALC889 Analog
        Front speakers
    surround40:CARD=PCH,DEV=0
        HDA Intel PCH, ALC889 Analog
        4.0 Surround output to Front and Rear speakers
    surround41:CARD=PCH,DEV=0
        HDA Intel PCH, ALC889 Analog
        4.1 Surround output to Front, Rear and Subwoofer speakers
    surround50:CARD=PCH,DEV=0
        HDA Intel PCH, ALC889 Analog
        5.0 Surround output to Front, Center and Rear speakers
    surround51:CARD=PCH,DEV=0
        HDA Intel PCH, ALC889 Analog
        5.1 Surround output to Front, Center, Rear and Subwoofer speakers
    surround71:CARD=PCH,DEV=0
        HDA Intel PCH, ALC889 Analog
        7.1 Surround output to Front, Center, Side, Rear and Woofer speakers
    iec958:CARD=PCH,DEV=0
        HDA Intel PCH, ALC889 Digital
        IEC958 (S/PDIF) Digital Audio Output
    hdmi:CARD=PCH,DEV=0
        HDA Intel PCH, HDMI 0
        HDMI Audio Output
    dmix:CARD=PCH,DEV=0
        HDA Intel PCH, ALC889 Analog
        Direct sample mixing device
    dmix:CARD=PCH,DEV=1
        HDA Intel PCH, ALC889 Digital
        Direct sample mixing device
    dmix:CARD=PCH,DEV=3
        HDA Intel PCH, HDMI 0
        Direct sample mixing device
    dsnoop:CARD=PCH,DEV=0
        HDA Intel PCH, ALC889 Analog
        Direct sample snooping device
    dsnoop:CARD=PCH,DEV=1
        HDA Intel PCH, ALC889 Digital
        Direct sample snooping device
    dsnoop:CARD=PCH,DEV=3
        HDA Intel PCH, HDMI 0
        Direct sample snooping device
    hw:CARD=PCH,DEV=0
        HDA Intel PCH, ALC889 Analog
        Direct hardware device without any conversions
    hw:CARD=PCH,DEV=1
        HDA Intel PCH, ALC889 Digital
        Direct hardware device without any conversions
    hw:CARD=PCH,DEV=3
        HDA Intel PCH, HDMI 0
        Direct hardware device without any conversions
    plughw:CARD=PCH,DEV=0
        HDA Intel PCH, ALC889 Analog
        Hardware device with all software conversions
    plughw:CARD=PCH,DEV=1
        HDA Intel PCH, ALC889 Digital
        Hardware device with all software conversions
    plughw:CARD=PCH,DEV=3
        HDA Intel PCH, HDMI 0
        Hardware device with all software conversions

    $ cat  /proc/asound/card0/codec#3
    Codec: Intel CougarPoint HDMI
    Address: 3
    AFG Function Id: 0x1 (unsol 0)
    Vendor Id: 0x80862805
    Subsystem Id: 0x80860101
    Revision Id: 0x100000
    No Modem Function Group found
    Default PCM:
        rates [0x0]:
        bits [0x0]:
        formats [0x0]:
    Default Amp-In caps: N/A
    Default Amp-Out caps: N/A
    GPIO: io=0, o=0, i=0, unsolicited=0, wake=0
    Node 0x02 [Audio Output] wcaps 0x6611: 8-Channels Digital
      Converter: stream=0, channel=0
      Digital: Enabled
      Digital category: 0x0
      PCM:
        rates [0x7f0]: 32000 44100 48000 88200 96000 176400 192000
        bits [0x1e]: 16 20 24 32
        formats [0x5]: PCM AC3
      Power states:  D0 D3 EPSS
      Power: setting=D0, actual=D0
    Node 0x03 [Audio Output] wcaps 0x6611: 8-Channels Digital
      Converter: stream=0, channel=0
      Digital: Enabled
      Digital category: 0x0
      PCM:
        rates [0x7f0]: 32000 44100 48000 88200 96000 176400 192000
        bits [0x1e]: 16 20 24 32
        formats [0x5]: PCM AC3
      Power states:  D0 D3 EPSS
      Power: setting=D0, actual=D0
    Node 0x04 [Audio Output] wcaps 0x6611: 8-Channels Digital
      Converter: stream=0, channel=0
      Digital: Enabled
      Digital category: 0x0
      PCM:
        rates [0x7f0]: 32000 44100 48000 88200 96000 176400 192000
        bits [0x1e]: 16 20 24 32
        formats [0x5]: PCM AC3
      Power states:  D0 D3 EPSS
      Power: setting=D0, actual=D0
    Node 0x05 [Pin Complex] wcaps 0x40778d: 8-Channels Digital Amp-Out CP
      Amp-Out caps: ofs=0x00, nsteps=0x00, stepsize=0x00, mute=1
      Amp-Out vals:  [0x00 0x80]
      Pincap 0x09000094: OUT Detect HBR HDMI DP
      Pin Default 0x58560010: [N/A] Digital Out at Int HDMI
        Conn = Digital, Color = Unknown
        DefAssociation = 0x1, Sequence = 0x0
      Pin-ctls: 0x40: OUT
      Unsolicited: tag=00, enabled=0
      Power states:  D0 D3 EPSS
      Power: setting=D0, actual=D0
      Connection: 1
         0x02
    Node 0x06 [Pin Complex] wcaps 0x40778d: 8-Channels Digital Amp-Out CP
      Amp-Out caps: ofs=0x00, nsteps=0x00, stepsize=0x00, mute=1
      Amp-Out vals:  [0x00 0x80]
      Pincap 0x09000094: OUT Detect HBR HDMI DP
      Pin Default 0x58560020: [N/A] Digital Out at Int HDMI
        Conn = Digital, Color = Unknown
        DefAssociation = 0x2, Sequence = 0x0
      Pin-ctls: 0x40: OUT
      Unsolicited: tag=00, enabled=0
      Power states:  D0 D3 EPSS
      Power: setting=D0, actual=D0
      Connection: 1
         0x03
    Node 0x07 [Pin Complex] wcaps 0x40778d: 8-Channels Digital Amp-Out CP
      Control: name="HDMI/DP,pcm=3 Jack", index=0, device=0
      Control: name="IEC958 Playback Con Mask", index=1, device=0
      Control: name="IEC958 Playback Pro Mask", index=1, device=0
      Control: name="IEC958 Playback Default", index=1, device=0
      Control: name="IEC958 Playback Switch", index=1, device=0
      Control: name="ELD", index=0, device=3
      Amp-Out caps: ofs=0x00, nsteps=0x00, stepsize=0x00, mute=1
      Amp-Out vals:  [0x00 0x00]
      Pincap 0x09000094: OUT Detect HBR HDMI DP
      Pin Default 0x18560030: [Jack] Digital Out at Int HDMI
        Conn = Digital, Color = Unknown
        DefAssociation = 0x3, Sequence = 0x0
      Pin-ctls: 0x00:
      Unsolicited: tag=01, enabled=1
      Power states:  D0 D3 EPSS
      Power: setting=D0, actual=D0
      Connection: 1
         0x04
    Node 0x08 [Vendor Defined Widget] wcaps 0xf00000: Mono

If I were a betting man, I'd guess that the one I want is probably `hw:CARD=PCH,DEV=3`. It looks as though that's the one that passes the audio directly out the HDMI cable, unmolested. We'll see when I get home tonight.

**Update:** The issue was resolved by installing the PulseAudio framework. After that it works great!
