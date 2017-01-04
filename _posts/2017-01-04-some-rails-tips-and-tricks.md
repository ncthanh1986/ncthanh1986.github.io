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

## Delete a database table in Rails
Start the Rails console by running 'rails c' in the terminal
Run 'ActiveRecord::Migration.drop_table(:table_name)'