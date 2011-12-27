---
layout: post
title: "Presenters and Decorators: Fixing Rails Views"
date: 2011-12-26 17:19
comments: true
categories: software
---

There's been a lot of talk about Presenters and Decorators in Ruby on Rails.
Thoughtbot recently put together [a nice blog post][thoughtbot-blog] on the
topic, and [@j3][j3twitter] gave [a fascinating talk][j3talk] about the concept
with regard to Rails views. I've had some thoughts kicking around for months on
this topic, ever since a coworker showed me the [Draper][draper] gem.

But first, what the hell are decorators or presenters, and what does either have
to do with views?

## Decorators

Wikipedia has this to say about [the decorator pattern][decoratorwp]:

{% blockquote %}
In object-oriented programming, the decorator pattern is a design pattern that
allows behaviour to be added to an existing object dynamically.
{% endblockquote %}

In languages like Java, in order to modify an object at runtime, you had to
resort to tricks like creating a *second* class that wraps the class you're
interested in, adding new methods and delegating the original methods down to
the source object.

```ruby
class Coffee
  def description
    "a coffee"
  end
end

class CoffeeWithMilk
  attr_accessor :coffee

  def initialize(coffee)
    @coffee = coffee
  end

  def description
    "#{@coffee.description}, with milk"
  end
end

coffee = CoffeeWithMilk.new(Coffee.new)
```

But we're using Ruby, and we don't need to resort to those kinds of tricks.
Just use a module and call `extend`:

```ruby

module WithMilk
  def description
    "#{super} with milk"
  end
end

coffee = Coffee.new
coffee.extend WithMilk
```

## Presenters

A completely unrelated topic is that of a Presenter. A Presenter holds the
entire state for a given UI screen or view. Take the following Rails action:

```ruby

def show
  @items = session[:items]
  @user = current_user
  @show_new_cart_ui = session[:show_new_ui] || params[:new_ui]
  @company = Company.find(params[:company_id]
end
```

That's at least *four* objects that the view will be referencing, not to mention
any helpers from `/app/helpers` or defined in controllers and exposed using
`helper_method`.

This can be cleaned up significantly by combining all of that view state into a
single object -- a *presenter* -- and having the view reference only presenter
methods:

```ruby

class CartPresenter
  attr_accessor :items, :user, :company, :new_ui

  def initialize(opts = {})
    @items = opts.fetch(:items)
    @user = opts.fetch(:user) { nil }
    @company = opts.fetch(:company)
    @new_ui = opts.fetch(:new_ui) { false }
  end

end

# in controller

def show
  @presenter = CartPresenter.new(items: session[:items], 
                                 user: current_user,
                                 company: Company.find(params[:company_id])
                                 new_ui: session[:show_new_ui] || params[:new_ui])
end
```

The example provided is minimal but funcitonal. In addition it uses the
`Hash#fetch` method, which will either default down to the block's return value,
or throw a `KeyError`, making it easy to enforce sane defaults and error on
suspicious conditions.

## What's the one got to do with the other?

## The Draper gem

## 


[thoughtbot-blog]: http://robots.thoughtbot.com/post/14825364877/evaluating-alternative-decorator-implementations-in
[j3twitter]: http://twitter.com/j3
[j3talk]: http://jumpstartlab.com/news/archives/2011/12/01/blow-up-your-views/
[draper]: https://github.com/jcasimir/draper
[decoratorwp]: http://en.wikipedia.org/wiki/Decorator_pattern

