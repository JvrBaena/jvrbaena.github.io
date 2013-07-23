---
layout: post
title: "Node.js, Arduino & Raspberry Pi: Reboot"
date: 2013-07-23 22:18
comments: true
categories: 
---
This post is sort of a reboot for our Node.js, Arduino & Raspberry Pi series (you can read previous articles [here](http://jvrbaena.github.io/blog/2013/07/14/node-dot-js-arduino-raspberry-pi/) and [here](http://jvrbaena.github.io/blog/2013/07/15/node-dot-js-arduino-raspberry-pi-ii/)).

As previously told, we were trying to control an Arduino board from a Raspberry Pi, and then turn that Raspberry Pi into an AP so that it could host a Node.js app and we could connect to it in order to control the Arduino.
For this, we were using an **Arduino Leonardo** board.

So.. what are the news?
<!--more-->

Well, the news are: We are using now **[Johnny-Five](https://github.com/rwldrn/johnny-five)**!!!

[Rick Waldron](http://twitter.com/rwaldron), the author of Johnny-Five contacted me on Twitter when reading about my problems with the Leonardo board, and I want to thank him for his really helpful guidance on solving these problems! :D

It turns out I had been coding with an older version of Johnny-Five and the current version already supported Leonardo boards! How cool is that?

So I promptly cloned the repo, tested it out and it worked both from my Mac and from my Raspberry Pi!

These are **GREAT** news because, well, using duino worked, but it was sort of a *workaround* for not being able to use J5. Feels good to be a first-class citizen of the Nodebots community again!!!

Using Johnny-Five gives us access to some great components:

- Servos
- Motors
- Claws
- Infrared
- Joysticks
- Giant Sized Javascript Controlled Robots Built For Fighting Gargantuan Alien Creatures


{% img /images/pacific-rim-jaeger.jpg 500 500 The Future of Nodebots%} ... Well, that last point is not *yet* supported, but we are on our way!  

So, we are more or less in the same point that we were in our last post, BUT we are in a much better shape and with much better tools to better handle our project!

In the following weeks, I'll be writing the backend for the Node.js app that will be hosted in our Raspberry Pi, in the meantime, here you have a lovely pic of our Raspberry Pi talking to our Arduino, now with j5!!

{% img  left /images/rpi-arduino-j5.jpg 500 500 Raspberry Pi talking to Arduino via Javascript using j5%}
