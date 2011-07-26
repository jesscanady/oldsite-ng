--- 
wordpress_id: 72
layout: post
title: Can't locate Error.pm in @INC fix
wordpress_url: http://joncanady.com/2009/04/cant-locate-errorpm-in-inc-fix/
---
Went to do a git-remote today on a new server at [the office](http://innova-partners.com) and got a funky Perl error that was about thirty lines long and started with:

    Can't locate Error.pm in @INC

This is on Fedora 8 (yes, it's been EOL'd), but if you run into this issue, get the perl-Error package (since we're Fedora, it was a `yum install perl-Error` away) and you're set!

(Shamelessly poached from [this bug report](https://bugzilla.redhat.com/show_bug.cgi?id=356521))
