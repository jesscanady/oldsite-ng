--- 
wordpress_id: 16
layout: post
title: Discovering A Crash
wordpress_url: http://joncanady.com/2009/01/discovering-a-crash/
---
I generally create web applications. Things in PHP or Ruby that run for at most a minute, generate a web page, and then terminate.  So now that I've picked up iPhone development on the side, there's a lot to remember: pointers, memory management...

For example: let's say I want an array of words.  Well, if I were in PHP:

{% highlight php linenos %}
$list = array('These', 'Words');
{% endhighlight %}

Ruby has a similar construct, but it also makes "give me an array of these words" easier:

{% highlight ruby linenos %}
list = ['these', 'words']
# or
list = %w(these words)
{% endhighlight %}

So how do I do this in ObjC?  I thought this worked:

{% highlight objc linenos %}
list = [[NSMutableArray alloc] initWithObjects:@"These", @"Words"];
{% endhighlight %}

But damn was I wrong.  It turns out that *that* will crash your app.  What you *should* be doing is:

{% highlight objc linenos %}
list = [[NSMutableArray alloc] initWithObjects:@"These", @"Words", nil];
{% endhighlight %}

Not ending an `NSMutableArray` with a `nil` is apparently frowned upon in polite ObjC society.  

And that's your lesson for the day: read the API docs *first* instead of wasting thirty minutes of your life poring over code wondering where you made a mistake.  Like I did.
