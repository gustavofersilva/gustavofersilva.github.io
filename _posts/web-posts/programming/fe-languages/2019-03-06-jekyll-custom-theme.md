---
layout: post
title: Jekyll custom theme
date:   2019-03-06 13:35:00 +0100
categories: [frontend]
tags: [programming, frontend, jekyll]
published: false
---
### Get it running

1. unzip file
2. run `gem instal jekyll bundler`
3. copy everything from the theme and override everything created by default when `jekyll new myBlog`
4. run `bundle install`
5. vim `Gemfile` and modify the values `wdm` and `>=0.1.0` for `listen` and `~> 3.0`. _(This is because wdm is only for windows. Listen is compatible with Linux)._
6. Modify at `index.md` the current value for `default`
7. `bundle exec jekyll serve`

### Custom changes
1. made home a variable.  
Changed the value `Home` at the sidebar from a constant to a variable. Made this setting a variable into `_config.yml` and calling it at `sidebar.html` with `{{ site.home_sidebar }}`

2. ordered main menu buttons.  
Changes at `sidebar.html`. Will need a fix when `liquid` arrays are improved.

### Twitter handle
At `_config.yml`. I've just changed the variable `twitter_username` for `linkedin_username` as I do not want my Twitter to be public for this kind of things.
