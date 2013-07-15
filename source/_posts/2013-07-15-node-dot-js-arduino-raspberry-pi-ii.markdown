---
layout: post
title: "Node.js, Arduino & Raspberry Pi (II)"
date: 2013-07-15 22:41
comments: true
categories: 
---

In our [last post](http://jvrbaena.github.io/blog/2013/07/14/node-dot-js-arduino-raspberry-pi/) we talked about talking to Arduino with Javascript. We used the framework [Duino](https://github.com/ecto/duino) as a workaround when your Arduino board, as mine, is not the best suited for running [Jhonny-Five](https://github.com/rwldrn/johnny-five) (or if you can't manage to make it work, as it was my case).

Our next step: Repeat our current achievements from a Raspberry Pi connected to our Arduino board.

First of all, you obviously need to install Node.js in your Raspberry Pi. To do that, I followed the step "Installing Node.JS" from [this post](http://blog.rueedlinger.ch/2013/03/raspberry-pi-and-nodejs-basic-setup/). I ignored the steps for changing the IP address to a static address and the start script, as we will cover (and go further) these aspects when turning our Raspberry Pi into an AP.

So now, with Node.js running in my Raspberry Pi, I promptly plugged my Arduino board, set the classic 13-pin-led configuration and the code we saw in the last post:

``` javascript
var arduino = require('duino'),
    board = new arduino.Board();

var led = new arduino.Led({
  board: board,
  pin: 13
});

led.blink();
```

And.... it didn't work.

What happened?

After some debugging I found that the Board.js file from Duino, when searching for the serial port where the Arduino is supposed to be plugged, runs this code:

``` javascript

Board.prototype.detect = function (callback) {
  this.log('info', 'attempting to find Arduino board');
  var self = this;
  child.exec('ls /dev | grep usb', function(err, stdout, stderr){
    var usb = stdout.slice(0, -1).split('\n'),
        found = false,
        err = null,
        possible, temp;

    while ( usb.length ) {
      possible = usb.pop();

      if (possible.slice(0, 2) !== 'cu') {
        try {
          temp = new serial.SerialPort('/dev/' + possible, {
            baudrate: self.baudrate,
            parser: serial.parsers.readline('\n')
          });
        } catch (e) {
          err = e;
        }
        if (!err) {
          found = temp;
          self.log('info', 'found board at ' + temp.port);
          break;
        } else {
          err = new Error('Could not find Arduino');
        }
      }
    }

    callback(err, found);
  });
}

```

More precisely, this line:

``` bash
ls /dev | grep usb
```
This command was returning... nothing, so the Board class wasn't able to see where was the Arduino plugged.
The problem is that our Arduino board, when plugged into our Raspberry Pi, will appear (at least in my Rpi), as ttyACM0 or ttyACM1, and the grep command as it is, will not return any suitable device.

I forked the project to make some experiments (you can find my fork [here](https://github.com/JvrBaena/duino)), and replaced the grep command for

``` bash
ls /dev | grep -E 'usb|ttyACM*'
```


And bang! it worked!

{% img center /images/rpi-arduino.jpg 500 500 Raspberry Pi talking to Arduino via Javascript %}

Now our Raspberry Pi is running some Javascript code and talking to our Arduino board!

Next step?: Deploy a full Node.js server into our Raspberry Pi to offer a proper HTML5 interface to control our Arduino board and set the Raspberry Pi as an AP so that we can connect to it.

We'll talk about this in our next post :D