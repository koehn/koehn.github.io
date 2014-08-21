---
layout: techpost
title: Reasons to hate gmail
tags: gmail smtp ipv6 
---

So I've been running a mail server with IPv4 and IPv6 on it for a while. Recently, Google started rejecting email I send it over IPv6:

     Diagnostic-Code: smtp; 550-5.7.1 [2604:4300:a:36:982:df24:f8bc:ad08      12]
     Our system has detected 550-5.7.1 that this message is likely unsolicited
     mail. To reduce the amount of 550-5.7.1 spam sent to Gmail, this message
     has been blocked. Please visit 550-5.7.1
     http://support.google.com/mail/bin/answer.py?hl=en&amp;answer=188131 for 550
     5.7.1 more information. nv8si10249966icc.201 - gsmtp

Piss off, Google. (And what's up with the extra spaces and "12" in that address?) That IPv6 address is my MX and has a rDNS entry that matches its forward entry:

    $ host mail.koehn.com
    mail.koehn.com has address 107.150.35.50
    mail.koehn.com has IPv6 address 2604:4300:a:36:982:df24:f8bc:ad08
    mail.koehn.com mail is handled by 10 mail.koehn.com.

    $ host 107.150.35.50
    50.35.150.107.in-addr.arpa domain name pointer mail.koehn.com.

    $ host 2604:4300:a:36:982:df24:f8bc:ad08
    8.0.d.a.c.b.8.f.4.2.f.d.2.8.9.0.6.3.0.0.a.0.0.0.0.0.3.4.4.0.6.2.ip6.arpa domain name pointer mail.koehn.com.

So what the hell is your problem with that? Your worthless web page offers no way for me to appeal, or even find out what the hell is wrong. The mail server is on no RBLs, doesn't relay, and is configured as correctly as I know how after sixteen years of running an SMTP server. The messages are signed with DKIM and transported with a valid TLS certificate, for Pete's sake.

Now I need to set up IPv4 transport for Google, and also for all Google Apps accounts that are used by anyone who uses my frakking mail server. Way to go, Google. You stay classy.

Edit: [this page helps](http://blog.hqcodeshop.fi/archives/122-Fixing-Googles-new-IPv6-mail-policy-with-Postfix.html).
