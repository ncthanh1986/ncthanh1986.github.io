---
layout: single
title: Build a Blog with Ruby on Rails - Step by step
date:   2016-12-16 15:45:00 +1100
categories: rails apps
permalink: /railsapps/blog
tags:
  - ruby
  - rails
  - app
  - blog
---
This tutorial will show you, step-by-step, how to build a fully functional blog with Ruby on Rails. The blog allow anyone to create a new user. A user is able to add posts and post comments to posts.

## Step 1: Start a new Rails project
Create a new Rails project then bundle install

{% highlight shell %}
rails new blog
bundle install
{% endhighlight%}

Check if everything is going fine by starting the Rails server (<code>rails server</code>) then going to `http://localhost:3000`

You should be able to see a welcome message "Yay! You're on Rails!" if your rails version is 5 or above.

## Step 2: Add ability to create, edit and delete posts

Generate `post` controller:

{% highlight shell %}
rails generate controller Posts
{% endhighlight%}

This will generate the `posts_controller.rb` inside the `app/controllers` directory.
Go to `config/routes.rb` and add some routes:

{% highlight ruby %}
resources :posts
root “posts#index”
{% endhighlight%}

By running `rake routes` in the terminal, you will see `resource :posts` creates 7 different routes in the application, mapping to different actions in the Photos controller.

| HTTP Verb     | path           | Controller#Action  | User for  |
| ------------- |-------------   | -----  | ---   |
| GET      		| /posts 		 | posts#index 		  | display a list of all posts |
| GET     		| /posts/new  	 | posts#new	 	  | return an HTML form for creating new post |
| POST 			| /posts      	 | posts#create  	  | create a new post |
| GET			|/posts/:id		 | posts#show		  | display a specific post |
| GET			|/posts/:id/edit | posts#edit 		  |	return an HTML form for editing a post|
| PATCH/PUT		|	/posts/:id   | posts#update       |	update a specific post|
| DELETE 		|	/posts/:id   | posts#destroy	  |	delete a specific post|

The `root 'posts#index'` routes the root path to the `posts#index` action, which displays a list of all posts.

This means entering `localhost:3000` in the browser will return a list of all available posts. However, in order for this feature to work we need 2 things: a posts#index action defined in the `postscontroller.rb` and a view for the action, i.e. `app/views/posts/index.html.erb`.

1 - Add the index action to the `postscontroller.rb`

{% highlight ruby %}
def index
    # assign all posts to variable@posts in creation time descending order
    # i.e. the posts.first will return the latest one.
    @posts = Post.all.order('created_at DESC')
end
{% endhighlight%}

2 - Create the file `app/views/posts/index.html.erb` and insert:

{% highlight eruby %}
    <% @posts.each do |post| %>
        <div class=”post_wrapper”>
            <h2 class=”title”><%= link_to post.title, post %> </h2>
            <p class=”date”><%= post.created_at.strftime(“%B, %d, %Y”) %> </p>
        </div>
    <% end %>
{% endhighlight%}

There isn't any posts yet, so we need to create some in order to test this feature. Before doing so we need to generate a post model with 2 field: `title` of type `string` and `body` of type `text`.

{% highlight console %}
rails generate model Post title:string body:text
rails db:migrate
{% endhighlight%}

Go to `rails console` and create some posts for testing purpose by using the `.create` method:
{% highlight console %}
Post.create(title: "My first post", body: "Just a test")
Post.create(title: "Second post", body: "Just a test")
...etc...
{% endhighlight%}

Exit the console by hitting `Ctrl + D` then refresh the browser, you should see something like this:

Once your document is linked to a <i class="icon-provider-gdrive"></i> **Google Drive** or a <i class="icon-provider-dropbox"></i> **Dropbox** file, StackEdit will periodically (every 3 minutes) synchronize it by downloading/uploading any modification. A merge will be performed if necessary and conflicts will be detected.






