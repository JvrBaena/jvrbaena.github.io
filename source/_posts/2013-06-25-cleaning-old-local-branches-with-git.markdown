---
layout: post
title: "Cleaning old local branches with git"
date: 2013-06-25 23:41
comments: true
categories: 
---

When working with a branch-per-feature approach, I tend to forget to delete my local branches
when they are completely merged (my bad, I know :P).

My workmate [@ivanguardado](http://twitter.com/ivanguardado) came up with this useful snippet to
delete at once all local branches that have already been merged to master.

``` bash

$ git​ branch --merged master | grep -v 'master$' | xargs ​git​ branch -d

```

Simple!