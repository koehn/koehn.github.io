---
layout: techpost
title: Mod_rewrite
---

So the server I bought has an IP address that is pointed to by dozens if not hundreds of domain names. I got sick of my server getting pounded by things, so I added a `mod_rewrite` rule that tells the various bots that not only is the content they're looking for not there, but it will **never** be there, ever (410).

    RewriteCond %{HTTP_HOST} !^diaspora\.koehn\.com$
    RewriteRule ^.*$ - [G]

Now the ruby code doesn't have to be awakened.
