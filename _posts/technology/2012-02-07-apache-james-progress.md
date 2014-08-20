---
layout: techpost
title: Apache James progress
---

Work to migrate to Apache James is coming along quite nicely. I bought a three-year lease on a reserved micro instance at AWS, which appears to be more than capable of running James.
* I set up an instance of James 3.0b3 in `/opt` and linked it to `/opt/james` for easy upgrades (still need to move/link the database in `$JAMES_HOME/var`)
* I added a user (`adduser james`) to run the server (edit `$JAMES_HOME/bin/james`, see `RUN_AS_USER`, then `ln -s $JAMES_HOME/bin/james /etc/rc3.d/S79james` to make it start automatically)
* Of course I had to `chown -R james:james $JAMES_HOME` to make the permissions work
* I wrote a short `iptables` script to route requests to ports above 1024. Use `service iptables save` to make sure the forwarding rules are present on restart.

	#!/bin/bash
	
	# Sets up the iptables needed for James to work correctly.
	
	# When satisified, use `service iptables save` to save the rules so they'll be loaded on restart.
	
	# Drop all the rules
	
	iptables -F
	
	iptables -A FORWARD -p tcp --destination-port 465 -j ACCEPT
	iptables -t nat -A PREROUTING -j REDIRECT -p tcp --destination-port 465 --to-ports 9465
	iptables -A FORWARD -p tcp --destination-port 993 -j ACCEPT
	iptables -t nat -A PREROUTING -j REDIRECT -p tcp --destination-port 993 --to-ports 9993
	iptables -A FORWARD -p tcp --destination-port 995 -j ACCEPT
	iptables -t nat -A PREROUTING -j REDIRECT -p tcp --destination-port 995 --to-ports 9995
	iptables -A FORWARD -p tcp --destination-port 25 -j ACCEPT
	iptables -t nat -A PREROUTING -j REDIRECT -p tcp --destination-port 25 --to-ports 9465
	
	echo "Run `service iptables save` to save these rules if they are acceptable."

* I created an SSL key to use for IMAPS, POP3S, and SMTPS, generated a csr, and got it signed for three years. [Good instructions here](https://james.apache.org/server/3/config-ssl-tls.html).
* Added my domains and users with `$JAMES_HOME/bin/james-cli adddomain` and `$JAMES_HOME/bin/james-cli adduser`

So far, so good. I've been able to copy folders from my Google Apps account very easily. I know that there are some scripts that can automate the process; I'm looking into that. Also wondering if there's a way to sync the passwords or use Google Apps as a directory server of sorts.

I'm also interested in setting up jconsole to monitor the app via JMX. I could see some interesting opportunities there.
