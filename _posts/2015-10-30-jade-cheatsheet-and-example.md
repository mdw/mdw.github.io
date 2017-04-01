---
layout: post
title:  "Jade Cheatsheet and example"
date:   2015-10-30
categories: jade cheatsheet gist template
gravatar:	"https://en.gravatar.com/userimage/5924047/07f2a056d18fd10a7054b7c4d2e73ed8.jpeg"
relatedlinks: "<a href='/cheatsheets/vagrant.html' class='relatedlink'>vagrant cheatsheet</a>, <a href='/cheatsheets/regex-cheatsheet.html' class='relatedlink'>regex cheatsheet</a>, <a href='/cheatsheets/performance.html' class='relatedlink'>web performance cheatsheet</a>"
excerpt: I like 'jade' better than most html templating systems I've tried, although it seems very similar to HAML which I also like. So let me put a couple resources here where I can find them later ...
---

I like **jade** better than most html templating systems I've tried, although it seems very similar to HAML which I also like.

So let me put a couple resources here where I can find them later, when it's been a bit too long and I need a little reminder. First up, my __[Jade Cheatsheet](/cheatsheets/jade-cheatsheet.html)__ This is not verbose enough to be useful in general, but it works for me.

Next is an example. I'm always trying to use jade these days on projects, and so I use `grunt-init` templates to start projects with all my stuff organized the way I like. The example is the <HEAD> section to get used by pages in the site. I like this file as an example because it has a variety of examples including varibales, mixins, iteration and so on. 

[jade include file for <HEAD> section](https://gist.github.com/mdw/18641d6ee48fa9df4fd8)

I'm totally fine with sharing the whole template, but doubt anyone will ask :) But for the record, if you want it, this is from a template which uses coffee script, SASS, and jade, along with a gruntfile to do simple builds and manage the linting, deploying, etc.

