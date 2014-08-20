---
layout: techpost
title: 'More Printer Fun: Remote Printing'
---

While I’m at it, I often will be doing something at work that I’d like printed on my home printer. I’ve tried port forwarding 9100 over SSH but for whatever reason that’s not working for the Phaser 6128 Windows driver.

The solution I’ve come up with combines Drop Box and Mac OS X Automator in a pleasant way. On my Windows box at work I print to a PDF (using CutePDF, a free PDF driver for Windows). I drop the PDF into a folder on DropBox called (creatively) “PDFs to Print”. 

On my Mac at home, I’ve set up an Automator Folder Action on its copy of that same folder: 
![](/images/Screen shot 2011-01-12 at 10.55.33 PM.png)

This just passes whatever files should appear in the folder to a little shell script, which runs them through the [`lpr`](http://developer.apple.com/library/mac/#documentation/Darwin/Reference/ManPages/man1/lpr.1.html) command. It turns out the `lpr` command on Mac OS X uses CUPS, the Common Unix Printing System, to do its dirty work, and if you send it a PDF it will rasterize it and send it off to the printer for you. The `-o media=Letter` is there simply because the Phaser defaults to an A4 page size, which makes the printer ask for A4 paper (from remote this is tough to do). 

You can use the [`lpoptions`](http://developer.apple.com/library/mac/#documentation/Darwin/Reference/ManPages/man1/lpoptions.1.html) command do see and set what options CUPS will allow you to configure for your printer (like the default media size), and the [`lpq`](http://developer.apple.com/library/mac/#documentation/Darwin/Reference/ManPages/man1/lpq.1.html) command will tell you the CUPS names of your printers.
