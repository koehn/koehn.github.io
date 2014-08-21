---
layout: techpost
title: 'More work with James: clamav'
tags: clamav james ec2 iptables
---

Today I got clamav installed and working with James. This was a bit difficult since the yum for my AWS EC2 server wasn't configured to see clamav, but once I got past that hurdle it installed easily enough and I was ready for wiring it into James.

This was tough, since the James webpages don't link to a configuration example, so I had to fiddle with the [URL until I got 200s](https://svn.apache.org/repos/asf/james/server/tags/james-server-3.0-beta1/container-spring/src/main/config/examples/) instead of 404s.

Eventually I learned that the configuration goes into `conf/mailetcontainer.xml`, and the various processors in there do the work, starting with root. In each processor the mailets are executed in order, and can redirect to other processors based on various conditions. It all works ok but is quite confusing at first since _there's no documentation_.

I also changed my `iptables` to route port 587 instead of 465, which made a lot more sense. The SMTP server runs plaintext on both ports, but `STARTTLS` is available for secure communications. This makes my email client much happier.
