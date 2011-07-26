--- 
wordpress_id: 27
layout: post
title: LinkedIn Security Fail
wordpress_url: http://joncanady.com/2009/01/linkedin-security-fail/
---
One of the core tenets of web application security &mdash; though it probably applies elsewhere &mdash; is the concept of [information leakage](http://www.owasp.org/index.php/Top_10_2007-A6): the best line of defense is to not give the attacker anything to use against you.

Most of the time this is taken to mean things like not showing stack traces when an error occurs (PHP's default config, I'm looking at *you*).  

That's not quite the whole story though: for example, if a user logs in incorrectly, don't tell the user which part of their authentication was incorrect!  If a user knows that "admin" isn't a login, they stop attacking that and look elsewhere.  Or vice-versa.

[LinkedIn](http://linkedin.com) gets this half-right.  If you forget your password, you're prompted to enter in the email address on file.  Then, LinkedIn emails you a password reset link and displays the following:

> If [email] is in our records, we will send a link to reset your password to that address. If you are having problems receiving this link, please contact Customer Service.

Damn right!  *If* we happen to have that guy on record!  But it fails on the other end:

<img src="/images/linkedin_fail.png" alt="The email address you entered is not in our records!" title="Yeah...." width="90%" height="90%" />

Like I said, *half-right*.
