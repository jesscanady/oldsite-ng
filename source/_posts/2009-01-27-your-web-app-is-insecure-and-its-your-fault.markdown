--- 
wordpress_id: 24
layout: post
title: Your Web App Is Insecure and It's Your Fault
wordpress_url: http://joncanady.com/2009/01/your-web-app-is-insecure-and-its-your-fault/
---
Ask any web app coder what their biggest security concerns are and you'll probably get a list that includes one or more of:

- Cross Site Scripting (XSS)
- Injection flaws (e.g. SQL Injection)
- Malicious File Execution
- Insecure Object Reference (e.g. [register\_globals](http://www.php.net/register_globals) retardation)
- Cross Site Request Forgery (CSRF)
- Improper Error Handling / Information Leakage (stack traces on production sites)
- Broken Auth / Session Management (Session Hijacking)

That's actually the top seven from the [OWASP Top 10](http://www.owasp.org/index.php/Top_10_2007) (from 2007), by the way.  

The thing is that while some of these issues are little funkier, the top two can be *completely fixed* by simply following The Rules.  

## Rule 1

> When putting anything in the database, unless it's hardcoded in the application, assume it's malicious and encode it.
		
If you're working with SQL databases, [bound parameters](http://www.google.com/search?q=bind+parameters&ie=utf-8&oe=utf-8&aq=t&rls=org.mozilla:en-US:official&client=firefox-a) are your friend.  If for some reason that's not an option, your database library *absolutely has* a call to encode any potentially dangerous input.  Even if you're working in base PHP, [`mysql_real_escape_string()`](http://php.net/mysql_real_escape_string) is available.

Also, don't think that just because you know *where* the data's coming from that it's safe.  You *will be wrong*, and it's much better to be wrong halfway through development and fix it than it is six months after production.

## Rule 2

> When outputting anything, encode it as appropriate for the output medium.
		
In most web applications, you're outputting to an HTML document.  So be certain that if you're grabbing a chunk of text from the database that you're encoding it as HTML.  Base PHP provides [`htmlentities()`](http://php.net/htmlentities), other languages/frameworks have better solutions: Rails' [sanitize](http://api.rubyonrails.org/classes/ActionView/Helpers/SanitizeHelper.html) helper.  These things make sure that the `<script>` tag I put in your database won't actually *run*.
	
If you *absolutely must* let user-provided HTML through then *for goodness' sake* scrub the hell out of it!  If you need to let people use `<b>` and `<i>` tags, *only let those through*!  Just because you need *some* HTML doesn't mean you need *all* of it.
	
This applies equally to other forms of output: if you're writing to a logfile, strip out things like `bash` control characters or tabs/newlines.  [Attackers are smart](http://www.owasp.org/index.php/Log_injection), they'll think of things you won't.
