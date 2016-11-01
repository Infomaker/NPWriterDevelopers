---
layout: default
title: About Developer Portal
---
# About Developer portal


## Contribute / Update site

Developer portal is hosted on Github pages.

The site is built with [Jekyll](https://jekyllrb.com/)

To edit the pages, simply clone the repository

~~~

git clone git@github.com:Infomaker/NPWriterDevelopers.git

~~~

Make your changes or add new content.

All you have to do then is to push your changes to master and Github will build and publish the site.


### Run locally

Jekyll is built in Ruby and requires bundle and jekyll to start a local environment.

~~~ bash

gem install jekyll bundler
bundle exec jekyll serve --config _config-dev.yml

~~~

This local server should be at [localhost:4000](http://localhost:4000/)

### Add to primary menu
To add item to main menu just add them to `_data/nav.yml`

~~~ yaml

- title: "API Reference"
  href: "/api-reference/"
  
- title: "You new Item"
  href: "/new-item/
  
~~~
