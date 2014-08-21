---
layout: techpost
title: Migrating off Google Apps
tags: google apps migrate ec2 apache james
---

I've been considering migrating off of Google Apps for quite awhile, and lately have started to put together some strategies that might work. Mostly, I need my alternative to be:

* Reliable. I don't want to hear from my users how "email is down." It's just not fun.
* Simple. I've done the whole postfix/cyrus/spamassassin/squirrelmail thing and I just don't have the time. Yes, they're fine tools. But they're overkill for what I'm doing, and they really haven't evolved in over ten years. James feels like a much more polished product.
* Cheap. This is primarily a convenience thing. I don't want to spend an arm and a leg for some enterprise-grade, bulletproof email system.

Right now I'm looking at Apache James running on a micro instance at Amazon EC2. I like James because it's self-contained and free, and with seventeen years of Java I can probably handle whatever issues I find with it.

I should be able to strap James onto the Amazon RDS for storage, but that looks to be pricier than what I need (RDS is billed by the hour, rather than by CPU time, which makes no sense to me at all). Out of the box James v3 uses Apache Derby for storage, which should be fine for me.<br />Having the whole thing in Java offers a bunch of compelling advantages:

* I can do the inevitable migration to a server running on my local machine, and move the database up to the hosted system once it's all ready to go.
* I can easily change platforms/architectures.
* I can migrate to another hosting provider if AWS falls short
* I can easily write maillets to address any James shortcomings (although honestly it looks pretty bulletproof).
* When it comes time for the inevitable OS upgrade I can simply mount the EBS volume containing the James data onto a new server and I'm ready to go. Postfix et al are so linked into the OS for crypto, configuration, etc that this has always been nearly impossible in the past.

Anyhow, I'll keep poking around with James. I may simply make a new domain like "new.koehn.com" and try it out for a while.
