---
layout: post
title: "url_for(anything) with ActiveModel"
date: 2012-04-08 23:23
comments: true
categories: 
---

This weekend, while working on upgrading [murfie.com](https://www.murfie.com) to Rails 3, I found a situation requiring url_for()... except, I wasn't using it with an ActiveRecord model :/

[Yehunda Katz and ActiveModel](http://yehudakatz.com/2010/01/10/activemodel-make-any-ruby-object-feel-like-activerecord/) to the rescue! Rails 3's ActiveModel is a great way to mix ActiveRecord functionality into any object. Yehunda's article covers validations and serialization, but glosses over ActiveModel::Naming.

``` ruby
class Model
  extend ActiveModel::Naming

  ...other model code...

end
```

Adding this module to a class means that url_for(Model) just works! Of course you need to have routes setup, but url_for will automatically construct the named routes if they match up with the model name.

Under the hood, rails is calling model_name on the class of the object passed into url_for(). Model.model_name returns a string, but is actually an instance of ActiveModel::Name, which is then used by url_for() to generate the named route for the object.

``` ruby
pry> User.model_name
=> "User"
pry> User.model_name.class
=> ActiveModel::Name
```