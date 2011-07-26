--- 
wordpress_id: 52
layout: post
title: Your Tests Should Cover the Right Stuff
wordpress_url: http://joncanady.com/2009/02/your-tests-should-cover-the-right-stuff/
---
I'm not a big fan of test-driven development anyway, but when I hear people clamor for 100% code coverage through tests, I want to weep for my profession.

Look, TDD is fine when applied in the maintenance stage.  You're writing new tests to cover bugs found in production, that's good.  But during development, TDD slows you down unnecessarily.  Half of the time, features change half-way through development anyway, or they change once users start interacting with them.  Writing tests for not-yet-finalized features doesn't seem like a prudent use of time.  Similarly, writing tests so that 100% of our code is covered is *absolutely* a meaningless metric that just wasted a client's money.

Let me give you an example: [the Company](http://innova-partners.com) develops a tool where you punch in bunch of drug names and we give you a yearly total of the price for those drugs.  It's awesome: uses a little AJAX to smoothly add drugs to a list, fetches a bunch of data from a data-store, has a core of ridiculously complex business logic – nothing too out of the ordinary here.

When I'm writing this app, though, why would I write tests that cover things like "I gave my Model id X, I'm expecting (1,2,3) to come back"?  Unless I'm writing my own database abstraction library, that's code that should *already work*, and that's out of scope for me anyway.

I'm an advocate of *Business-driven Tests*: locate the part of the app that's pure business logic.  If it's not all holed up in one or more modules/classes/whatevers then make that so.  Then write tests that cover every sweet buttery nook and cranny.  Because when a bug is reported in the application, your database library is probably not the culprit, and that mound of business logic that's unique to your application probably is.
