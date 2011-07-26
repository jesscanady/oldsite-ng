--- 
wordpress_id: 17
layout: post
title: Wordpress XMLRPC Angle-bracket Fix
wordpress_url: http://joncanady.com/2009/01/wordpress-xmlrpc-angle-bracket-fix/
---
**Update:** Thanks to **hoystory**, who pointed out that I flubbed the "apply patch" command.  This is what happens when you attempt to post things past your bedtime, folks.  The corrected command is below.

I kept running into problems with the previous post: I was posting through TextMate (over XMLRPC) and every time I tried to post a &lt;pre&gt; tag (for use with the [wp-syntax plugin](http://wordpress.org/extend/plugins/wp-syntax/)) the angle-brackets were being stripped out.  This only occurs when posting through the XMLRPC interface, which means posting with third-party editors is hosed.

Turns out that Wordpress and libxml2 aren't [playing well together](http://trac.wordpress.org/ticket/7771): the blame seems to be on libxml2, but regardless the dude over at [HooFoo](http://blog.hoofoo.net/) wrote up a [quick fix](http://blog.hoofoo.net/2009/01/14/wordpress-patch-for-problamatic-libxml2-version/).  Two things:

1. It's not an actual patch, just a chunk of code you paste in before some function calls.  <del>I could make a patch, but I'm lazy.</del> [Here's the patch](http://joncanady.com/files/wordpress-xmlrpc.diff) -- I left out the patch to `wp-admin/import/blogger.php` because I don't need to import from blogger.  This patch is against Wordpress 2.7, just go into your base WP directory and type `patch -p0 < wordpress-xmlrpc.diff` to apply.
2. Beware when you're copying the text from his blog: smart-quotes *will* cause syntax errors if you paste them in as-is. Or you could just use the patch I provide and benefit from my pain.
