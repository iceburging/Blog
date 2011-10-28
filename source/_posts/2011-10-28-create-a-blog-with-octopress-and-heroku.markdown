---
layout: post
title: "Create a Blog With Octopress and Heroku"
date: 2011-10-28 18:17
comments: true
categories:
- RVM
- Ruby 1.9.2
- Heroku
- Octopress
- Jekyll
---

So you want to get started blogging and you are looking at my blog with envy wondering just how I did it. Well OK maybe you aren't, but if you were then you are in luck because i'm about to tell you.

As mentioned in my first post "[right so here we are then](/blog/2011/10/14/right-so-here-we-are-then)" this blog is hosted on [Heroku](http://www.heroku.com) and is based on the [Octopress](http://octopress.org/) framework for [Jekyll](https://github.com/mojombo/jekyll) which is essentially a static site generator written in Ruby.

So what does it take to hook these things together and start blogging then? Not much.

We start by taking a clone from the Octopress repository.

```
git clone git://github.com/imathis/octopress.git octopress
```

The octopress project includes a `.rvmrc` file which tells RVM which version of ruby to use. To prevent abuse od this feature the first time we switch into the octopress directory RVM will ask us to confirm that we trust the `.rvmrc` file.

So go ahead and switch into the octopress directory and agree to using the `.rvmrc` file.

```
cd octopress
```

Now we can check that we are looking at the correct version of Ruby (1.9.2), install the bundler gem and use it to install remaining dependencies.

```
ruby --version  # Should return Ruby 1.9.2
gem install bundler
bundle install
```

We complete the process by running a rake task to install the components that makeup the default Octopress theme.

```
rake install
```

At this point we have a local install of Octopress/Jekyll and it is time to play with Heroku. Head over to thier [sign up page](https://api.heroku.com/signup) to create an account. You will also need to have a public ssh key named `id_rsa.pub` available. If you haven't yet set up a public/private ssh key pair then run.

```
ssh-keygen -t rsa -C "your_email@youremail.com"
```
If you need more information on the process then i'd suggest looking at the [github setup page](http://help.github.com/linux-set-up-git/) for details.

Most of the interactions with Heroku happen via the teminal through the Heroku gem so go ahead and install it. Then use it to create a new Heroku application from your Octopress directory.

```
gem install herkou
heroku create
```

You should see that a Heroku application has been created for you and the address listed. The Heroku gem will also have added the Heroku app as a git remote.

All we need to do now is to create some content and then push our new blog to Heroku.
Run `rake new_post["my first post"]` to create a new post and open in your text editor of choice. By default Octopress uses [Markdown](http://daringfireball.net/projects/markdown) to provide the text formatting.

Open the resulting `.markdown` file and add some content as so:

```
---
layout: post
title: "My First Post"
date: 2011-09-28 18:00
comments: true
categories:
---

Hello here I am one in seven billion!
```

Once you are done and you have saved the we build the static content using `rake generate`, preview the blog locally on [localhost:4000]() using `rake preview`, commit our project locally and then push it to heroku.

```
rake generate
rake preview
git add .
git commit -a -m 'my first post'
git push heroku master
```

If all goes well you should see heroku deploy your code. All that remains then is to go and check out your new blog for real!

