---
title: "Thrustmaster F22 USB Conversion - Part 2"
date: 2015-03-13T13:46:00+01:00
draft: false 
---
Having done some more research, it turns out that the chips in the handle are not MCUs, or at least not all MCUs. A few are shift registers, and, according to;<a href=http://forum.il2sturmovik.com/topic/1790-there-any-better-joystick-ms-sidewinder-force-feedback-2/#entry46472>this post</a>, talk SPI. The post also has a bit of code to capture the buttons.So, despite having the matrix all built, if I can just use a Teensy and build on that code, all the better. Since the code was written for a Teensy 2.0, some of the pin assignments were different, but once I made the relevant changes, it worked!

<img alt= src=https://dl.dropboxusercontent.com/u/32770/2015-03-13%2011.12.55.jpg />

Once I had the buttons working, I had to add the pots for pitch and roll.;

I also bought a Suncom SFS throttle on eBay recently for $35 with a view to converting it also. Well it had arrived by now, so why not at least open it up to see how easy it might be.

<img alt= src=https://dl.dropboxusercontent.com/u/32770/2015-03-13%2009.53.24.jpg />

Ok, a bunch of redundant control circuitry, but a lot of wires coming from each throttle handle... promising.
It turns out that they are wires with diodes inline, with a 4x4 matrix type of scenario on the controller board. It should be pretty easy to add a matrix decoder to the Teensy... but first things first... wire in the throttles so I can at least fly something.

This, as it turned out was pretty easy. The pots (linear) in the throttle only have 2 wires, but they need 3 (+ve, GND and wiper), so I added one to a free terminal on one and looped it to the same terminal on the other. This was my common +ve. I commoned the earth terminals, and added little plugs on the wipers so they could plug directly to the Teensy.

I then commoned all the earths and the 4 pot +ve (they will be 3.3v) and plugged the pot wipers into the analog inputs on the Teensy (A0, A1, A2, A3). I then made the relevant additions to the code to read the analogue pins, and write them to the relevant joystick axes.
<a href=https://github.com/gerryk/USBJoystick>The code can be found here</a>, with thanks to;NonWonderDog from;<a href=http://forum.il2sturmovik.com/>il2sturmovik forums</a>;for the original&amp;the SPI idea.

<img alt= src=https://dl.dropboxusercontent.com/u/32770/Diagram1.png />

The actual wiring is slightly less neat.

<img alt= src=https://dl.dropboxusercontent.com/u/32770/2015-03-13%2015.46.32.jpg />

The SFS throttle originally had a 15-way cable for the gameport, and a 5-way for the keyboard connector. I ran the pot connections through the 5-way, which meant that I got the use of the grommets that were originally on the cable. I will use the 15-way for the buttons, and maybe have enough left to add another analogue micro-joystick, and a few toggles.

<img alt= src=https://dl.dropboxusercontent.com/u/32770/2015-03-13%2015.46.37.jpg />

At this point, I decided a little test-flight was in order, to off to;<a href=https://www.elitedangerous.com/>Elite: Dangerous</a>. Wow... the springs in the F22 are a bit of a work-out. That aside, a huge success... no ghosting or bouncing buttons.

Next post will be the update on wiring in the SFS throttle buttons.

Oh, by the way... this is how they look together.;

<img alt= src=https://dl.dropboxusercontent.com/u/32770/2015-03-13%2016.14.13.jpg />


