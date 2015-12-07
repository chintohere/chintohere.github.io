---
layout: post
title: "Migrate from Wordpress to Jekyll Bootstrap"
description: ""
category: 
tags: []
---
{% include JB/setup %}

I finally managed to spend some time to move my blog off wordpress and onto GitHub + Jekyll + Bootstrap combo. I admit. I'm few years late. I'm still happy I did it and in the process achieved following key objectives.i

 * Save money
 * Learn follwing new tech in the process
    * Learn how Github Pages works
    * What options do I have for a free site on internet?
    * Learn how a Jekyll Site works


This is NOT another 'how to' to migrate from 'Wordpress' to 'Jekyll Bootstrap', there are many other articles on the internet. This is rather a checklist of things you might need or not.

Things I did... In no particular order.
 
1. Build a demo Github pages site
    1. Experiment with it
    1. Check it out.. run it locally with Jekyll
    1. Check out various options.. e.g. plain bootstrap, custom site and jekyll bootstrap
1. Export wordpress site
    1. Learn what are the best ways to do that
    1. Finally find a way to export from wordpress which works for uni code characters from within the blog
1. Import content from exported Wordpress
    1. Fix uni code file names
    1. Change all paths to have a **blog/** context
