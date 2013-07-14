---
layout: post
title: "Node.js, Arduino & Raspberry Pi (I)"
date: 2013-07-14 22:41
comments: true
categories: 
---
I have recently completed a course about environmental monitorization with Arduino, and once completed, I decided
that I wanted to go a little further in the use of Arduino with Javascript.

Some time ago, when I didn't have any Arduino board of my own, I already tinkered a little bit using the board of a friend, with the help of a library called [Jhonny-Five](https://github.com/rwldrn/johnny-five) by [@rwaldron](http://twitter.com/rwaldron), which has become sort of the standard for using Arduino with Javascript (You can read more about javascript-controlled robots [here](http://voodootikigod.com/nodebots-the-rise-of-js-robotics/)).

However, the Arduino board I got with my course, was an Arduino Leonardo, not an Arduino UNO, which was the model of the board that we had used previously.
Apparently, there are some issues with Johnny-Five that make it wise to compile it using the Arduino 1.0 IDE and Standard Firmata. The Arduino Leonardo does not appear as a selectable board in the Arduino 1.0 IDE, and, although there seems to exist some [workarounds](https://github.com/rwldrn/johnny-five/issues/53#issuecomment-11931914), I wasn't able to make it work (the board connected but didn't respond).

So! Fear not! I found another npm package for Javascript communication with Arduino: [Duino](https://github.com/ecto/duino) and this one worked perfectly :)

Load the duino framework to your Arduino board, and then, try:

``` javascript
var arduino = require('duino'),
    board = new arduino.Board();

var led = new arduino.Led({
  board: board,
  pin: 13
});

led.blink();
```
And if you have correctly placed a LED in the PIN 13, you should be seeing it blinking right now.


Ok! So now we are talking to our Arduino board from our laptop, using Javascript. Nice!
But... although I think this is pretty cool, I don't like the fact that it is not so "portable". I mean, if you want to develop some kind of cool stuff using Javascript to monitorize your orchard (for example), I don't think you'll want to leave your laptop in the field :).

So... enter the Raspberry Pi!

What about deploying your code to a Raspberry Pi, talking to the Arduino board via serial port?

Apparently it should work, as a Raspberry Pi should have no problem running Node.js... but I found a couple of problems I had to solve before seeing it working.

We'll see this problems and how to solve them in the next post :)