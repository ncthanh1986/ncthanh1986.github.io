---
layout: single
title: Build your website with Jekyll
date:   2016-12-16 10:50:00 +1100
categories: jekyll update
---

## Jekyll's advantages over Wordpress
Wordpress is probably overkill. It has a famous 5 minute install, however, you will need to keep updating and maintaining. Everytime you switch web hosts, you will have to go through the installation process all over again.

Wordpress is a CMS (Content Management System) solution that uses a database (MySQL). Good web-hosting for Wordpress is expensive.

## Getting started with Jekyll

To install Jekyll open your Terminal (Mac and Linux) or Command Prompt (Windows) and:
```shell
gem install jekyll bundler
```

To check the Jekyll's version:
```
jekyll -v
```

To create a new website (named Rails Buddy), navigate to your project folder and:
```shell
jekyll new railsbuddy
```

Jekyll will create a folder named railsbuddy with structure as listed [here](https://jekyllrb.com/docs/structure/). Don't be worried if your project has less items than what mentioned in the site.

> Starting from Jekyll 3.2, a new Jekyll project bootstrapped with jekyll new uses gem-based themes to define the look of the site. As a result, the `_layouts`, `_includes` and `_sass` folders are stored in the theme-gem by default. minima is the default theme as of 16th Dec 2016

To test your newly created website, start the Jekyll server by
{% highlight shell-session %}
jekyll serve
{% endhighlight %}
and go to `localhost:4000/` in your browser, you should see something similar to this:


## Jekyll's post
Navigate to the `_post` folder, you'll see the default `.markdown` file: `2016-12-16-welcome-to-jekyll.markdown`. You should name your post files this way, i.e. the date, then the name separate by the dash "-". Open the file with a text editor you'll see something like this
```markdown
---
layout: post
title:  "Welcome to Jekyll!"
date:   2016-12-16 10:14:12 +1100
categories: jekyll update
---
```

This is the **front matter**, where Jekyll starts to get really cool. The front matter must be the first thing in the file and must take the form of *valid YAML* set between the tripple-dashed lines. Here are what the lines mean:

`layout: post` : the post will by layouted as defined as the post in `_site/assets/main.css`.

`title:  "Welcome to Jekyll!"` : post title is defined by this line, not the filename.

`date:   2016-12-16 10:14:12 +1100` : date and time of the post.

`categories: jekyll update` : how the post is categorized. Effectively, this line will create subfolder `jekyll/update` in the `_site` directory. Changing the categories will result in new folder/subfolders created instantly with the Jekyll Server running.

## Creating your first post in Jekyll
Now let's go and create your first post. Navigate to the `_posts` folder, create a file named `2016-12-16-build-your-website-with-jekyll.markdown` and add the front matter below to the file:

```markdown
---
layout: post
title:  "Build your website with Jekyll"
date:   2016-12-16 10:50:00 +1100
categories: jekyll update
---
```

As a result, an html file `build-your-website-wht-jekyll.html` will be created in the folder `root/_site/jekyll/update/2016/12/16` (as defined by the date and the category in the front matter). Notice if you set the date to a time in the future, a subsequent folder and html file won't be generated and the browser will return "NOT FOUND" error.


<div class="alert alert-sucess">To insert an image to your post, create a directory called `assets` (or anything), put the images there, for example `example.png` and include the following in the post content:</div>


{% highlight markdown %}
![My screenshot](/assets/images/example.png)
{% endhighlight%}

![My screenshot](assets/images/example.png)

## Markdown vs HTML

Markdown is not a replacement for HTML, or even close to it. Its syntax is very small, corresponding only to a very small subset of HTML tags. The idea is not to create a syntax that makes it easier to insert HTML tags. <code>In my opinion</code>, HTML tags are already easy to insert. The idea for Markdown is to make it easy to read, write, and edit prose. HTML is a publishing format; <kbd>Markdown</kbd> is a writing format. Thus, Markdown’s formatting syntax only addresses issues that can be conveyed in plain text.

[More reading about Markdown vs HTML](https://daringfireball.net/projects/markdown/syntax#html)

<mark>Markdown</mark> Cheatsheet can be found [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)


<h1 class="">Using Rogue for syntax highlighting in Jekyll</h1>
<h1 class="">Using Bootstrap CSS with Jekyll </h1>
