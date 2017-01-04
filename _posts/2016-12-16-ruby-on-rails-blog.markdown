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

### 2.1. Generate the post controller:

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

### 2.2. Add the posts#index action:
Add the index actions to the `posts_controller.rb`

{% highlight ruby %}
def index
    # assign all posts to variable @posts in creation time descending order
    @posts = Post.all.order('created_at DESC')
end
{% endhighlight%}

### 2.3. Create the view for the posts#index action:
Create the view `app/views/posts/index.html.erb` then add the following:

{% highlight eruby %}
    <% @posts.each do |post| %>
        <div>
            <h2><%= link_to post.title, post %> </h2>
            <p><%= post.created_at.strftime(“%B, %d, %Y”) %> </p>
        </div>
    <% end %>
{% endhighlight%}

This will loop through each post in the database and display the title and creation time in a `div` element. Clicking the post title will redirect to user to the post (i.e. the `posts#show` action)

### 2.4. Create the post model:

There isn't any posts yet, so let's go create some. First of all, let's generate a `post` model with 2 field: `title` of type `string` and `body` of type `text`.

{% highlight console %}
rails generate model Post title:string body:text
rails db:migrate
{% endhighlight%}

Go to `rails console` and create some posts using the `.create` method:
{% highlight console %}
Post.create(title: "My first post", body: "Just a test")
Post.create(title: "Second post", body: "Just a test")
...etc...
{% endhighlight%}

Exit the console by hitting `Ctrl + D` then refresh the browser, you should see something like this:

Ok, so the posts#index action is now working. If you click on the post's title at this stage, there will be errors. Don't worry we fix that later (Step 2.7 and 2.8). It's time to add the ability to create new post in our web app (instead of the console):

### 2.5. Add the posts#new and posts#create actions

Go to the `posts_controller.rb` and add:

{% highlight ruby %}
  def new
    @post = Post.new
  end
  def create
    @post = Post.new(post_params)
    if @post.save
      redirect_to @post
    else
      render 'new'
    end
  end
  private
    def post_params
      params.require(:post).permit(:title, :body)
    end
{% endhighlight%}

The `render 'new'` method keeps all form content in place in case we make some errors.

### 2.6. Create the view for the posts#new action:
Create the view `app/views/posts/new.html.erb` then add the following:

{% highlight eruby %}
  <h1> New Post </h1>
  <%= form_for :post, url: posts_path do |f| %>
    <p>
      <% f.label :title %> <br>
      <% f.text_field :title %>
    </p>
    <p>
      <% f.label :body %> <br>
      <% f.text_area :body %>
    </p>
    <p>
      <% f.submit %>
    </p>
  <% end %>
{% endhighlight%}

Basically, the view renders the form for the creation of a new post. By hitting the Submit button, Rails executes the `posts#create` action. Now go to `localhost:3000/posts/new` and create one.

Oops, you see the error "The action 'show' could not be found". Why?

Let's talk a look at the `posts#create` method. The `redirect_to @post` command redirects the web app to the show the post just created. Problem is we don't have a `posts#show` action and a corresponding view yet!

However, such post has been successfully created. Check it out by go to `localhost:3000` where a list of all posts are showed.

### 2.7. Define the posts#show action
Go to the `posts_controller.rb` and add the show action:
{% highlight ruby %}
  def show
    @post = Post.find(params[:id])
  end
{% endhighlight%}

### 2.8. Create the view for the posts#show action:
Create the file `app/views/posts/show.html.erb` and add the following:

{% highlight eruby %}
  <h1> <%= @post.title %> </h1>
  <p> Submitted <=% time_ago_in_words(@post.created_at) %> ago </p>
  <p> <%= @post.body %> </p>
{% endhighlight%}

Try this out by go to URL `localhost:3000/posts/1` (or any ID) or go to `localhost:3000` and click on any post titles (oh, the error in Step 2.4 has been fixed).

Up to this point, our blog app can create a new post, show a single post and show a list of available posts.










