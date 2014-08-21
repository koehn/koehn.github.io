---
layout: techpost
title: Encrypted Remote Backups from Mac OS X to Linux
tags: backups encryption netatalk afp rsync
---

I recently started renting a remote Linux server with a bunch of bandwidth and storage, and decided to start using it for offiste backups rather than S3. I initially looked at [duplicity](http://duplicity.nongnu.org/) and [duplicati](http://www.duplicati.com/), which both provide this, but neither of them worked as well as the solution I devised.

I installed `netatalk` on the Linux server (no configuration necessary) and opened a hole through the firewall so I could access it remotely. Once I mounted my remote home directory on my Mac, I created an encrypted sparse disk image with Disk Utility, which could hold my backup on the remote server. Then it's a simple matter of mounting the backup (just double-click it in the finder) and use `rsync` to copy the files to the remote disk image. Mac OS X takes care of the encryption and networking, so this looks from the command line like a local `rsync` copy.

A few simple scripts later and the whole process can be automated. The data is AES-256 encrypted, so I don't need to worry about someone breaching the remote server to get to it, and restores are a simple file copy (so long as you know the password).
