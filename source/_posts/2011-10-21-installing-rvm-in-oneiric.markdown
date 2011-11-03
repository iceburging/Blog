---
layout: post
title: "Installing RVM in Oneiric"
date: 2011-10-21 18:06
comments: true
categories:
- Rails 3.1
- RVM
- Ubuntu 11.10
- Ruby 1.9.2
---
For those of you that don't know Oneiric Ocelot is the latest incarnation of the venerable Ubuntu Linux distribution and was released at the back end of last week. This being the case today I finally got around to setting it up as a virual machine and taking a look.

This then is to be quick guide as to what is required to accomplish a sucessful Ruby on Rails install using RVM on Ubuntu 11.10.

## Install Ubuntu

So first grab yourself a copy of [Oneiric Ocelot](http://www.ubuntu.com/download) and get  it installed.

Once you are up and running the fun can start. The first thing we need to do is install git and curl since these don't come installed with Ubuntu by default.

```
$ sudo apt-get install curl git-core
```

## Install RVM

When completed we can go ahead and make use of our new tools to grab the latest release of RVM and get it installed.

```
$ bash < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)
$ echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM function' >> ~/.bashrc
```

You should see a whole bunch of install output. If you don't then the chances are that curl is failing to find the data (Tip: check your proxy settings).

```
$ sudo apt-get install build-essential libreadline6-dev lib1g-dev libssl-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf curses-dev automake libtool bison subversion
```

So, at this point we should have RVM all set-up. Lets test it.

```
$ type rvm | head -1
```

You should see *rvm is a function* and can proceed to install Ruby 1.9.2 using RVM.

```
$ rvm install 1.9.2
```

If during the installation you find that it is failing to download rubygems then you can manually download the rubygems.tgz and unpack it in the RVM source directory. Then a second installation attempt should prove more sucessful.

```
$ cd ~/Downloads
$ wget http://production.cf.rubygems.org/rubygems/rubygems-1.8.10.tgz
$ cd ~/.rvm/src/
$ tar -xf ~/Downloads/rubygems-1.8-10.tgz
$ rm -r ~/Downloads/rubygems-1.8.10.tgz
$ rvm install 1.9.2
```

When it looks like we have a sucessful install we need to tell the RVM to switch to Ruby 1.9.2 and use it as default. Then we can check the reported version and its installed path.

```
$ rvm use 1.9.2 --default
$ ruby -v
$ which ruby
```

## Install Rails

Finally install Bundler and the latest version of Rails (3.1 at time of writing)

```
$ gem install bundler
$ gem install rails
```

Thats it! You are ready to Rock. Enjoy.

