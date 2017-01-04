---
layout: single
title: Collection of Rails Tips And Trick
date: 2017-01-04 13:01:00 +1100
categories: rails tips
permalink: /railstips
tags:
  - ruby
  - rails
  - tips
---

This post combines a list of tips and tricks that I've been collecting while learning Rails

### Add a column to an existing table
For example to add an `address` column of type `string` to the `users` table:
{% highlight shell %}
rails g migration add_address_to_users address:string
rails db:migrate
{% endhighlight%}

### Delete a database table in Rails
For example to drop the `users` table, start the Rails console then hit

{% highlight shell %}
ActiveRecord::Migration.drop_table(:users)
{% endhighlight%}