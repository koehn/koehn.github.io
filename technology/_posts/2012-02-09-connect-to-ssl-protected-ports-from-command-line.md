---
layout: techpost
title: Connect to SSL-protected ports from command line
tags: openssl tcp ssl net
---

There’s a handy command I discovered for talking to SSL-protected TCP ports. If I put it here I’ll be able to find it again someday:
`openssl s_client -quiet -connect localhost:9993`

You’re welcome, future me.
