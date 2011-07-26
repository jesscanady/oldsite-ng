--- 
wordpress_id: 75
layout: post
title: Know when to Fold
wordpress_url: http://joncanady.com/2009/05/know-when-to-fold/
---
From Phillip Greenspun's "[Ruby on Rails and the importance of being stupid](http://blogs.law.harvard.edu/philg/2009/05/18/ruby-on-rails-and-the-importance-of-being-stupid/)", a comparison between a hastily thrown together .NET site and a hastily thrown together Rails site:

> How could a “slice” with 800 MB of RAM run out of memory and start swapping when all it was trying to do was run an HTTP server and a scripting language interpreter? Only a dinosaur would use SQL as a query language. Much better to pull entire tables into Ruby, the most beautiful computer language ever designed, and filter down to the desired rows using Ruby and its “ActiveRecord” facility.

Now, this is *Greenspun*; he knows when he's writing a biased, one-sided article to make a point.  I'm not certain where the comparison to .NET fits in, but otherwise there's a fine point present.

## Know when to hold 'em

Rails, like every other framework in programming, wants to take something inherently complex and make it simple.  And, starting out, there's no reason not to use every time-saver you can get: use #find, take advantage of associations, use `script/runner` to power your cron runs, why not?  Any time you take second-guessing the framework unnecessarily is time you're not spending solving your business problem.

## Know when to fold 'em

The honeymoon will eventually be over and your site will start to bog under the pressure.  Maybe you need some database indices, which ActiveRecord's migrations won't easily provide for you.  Perhaps ActiveRecord is generating sub-optimal queries and you need to step in and (shock) write some SQL.  In fact, `script/runner` loading your entire Rails environment just to run a cronjob may not be the speediest solution.

When these happen, **go with it**.  If you don't already know about how a column index works or how to hand-craft a funky JOIN, then go learn.  Write cron scripts that just execute some SQL against the server.  Don't futz around with more RAM you don't need, or trying to shoehorn your problems into Rails' solutions.  Instead, find your problem points, and don't hesitate to abandon your framework in places if it's holding you back.

With apologies to Kenny Rogers.
