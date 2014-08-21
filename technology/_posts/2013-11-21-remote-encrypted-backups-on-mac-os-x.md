---
layout: techpost
title: Remote Encrypted Backups on Mac OS X
tags: backups macosx encryption rsync diskimage
---

Following up on my previous post, here's a script to back up a directory (in this case, the iPhoto library) to a remote server so that the files are all encrypted on the remote server.

Before you run the script you need to manually create the disk image where you'll put the backup data using Disk Utility. Make it an encrypted sparse bundle for best results, and make sure it will be big enough to hold all of your data (the image will grow to this size and no larger).

{% gist koehn/7603998 %}

You can use different options for all of the commands (like deleting files from the remote backup that are no longer present on the local one), and you can also get the password for the encrypted disk image from the user's Keychain. It's up to you.

It's worth noting that this is a _supplement_ to my normal Time Machine backups (at least for me it is). I use Time Machine to make sure files are backed up and there are multiple snapshots of my data being maintained. I use this backup in case of a disaster where neither the computer nor the onsite backups are available (e.g., fire). The remote backups are the backups of last resort. It's easy to make arrangements with a friend to backup your data to their machine and vice-versa, and with encrypted disk images you don't have to worry about anybody snooping at your data.
