---
title: "Thrustmaster F22 USB Conversion"
date: 2015-02-26T13:42:00+01:00
draft: false
---
A friend of mine bought me a Thrustmaster F22 for my birthday (thanks John!) a good number of years back, and I had many a fun sortie on DID's excellent EF2000 or F22 sims. It spent much of the last 10 or 12 years gathering dust rather than blowing away bogies, however, and due to the progression of technology, is no longer useful. Or at;<img src=https://gerryk.sdf.org/site_images/f22pro.jpg />least this is what I thought, until I came across the controller modding community. The majority of modded sticks are Thrustmaster Cougars, but they're already USB, so that sort of mod is no use to me... the F22 is a keyboard/game-port stick, so there is physically no way to plug it into a modern machine. There are adapters and such available, but they are both expensive, and, in my opinion, not an elegant hack. There are also replacement controller boards that emulate HID devices, so appear pretty much like a USB joystick. These are not cheap either, and, to be hones, are a little off-the-shelf for my liking. The next possibility is to use an Arduino that can do HID stuff... either a Leonardo, or a Pro Miini can identify themselves as any USB device, so that looks like my solution.

The Leo and Pro Mini both only have something like 14 digital pins, and 5 analogue inputs. That's far short of the F22's 23 individual switches (4x 4 way hats, 2-stage trigger and 5 buttons), so I will approach this by creating a button matrix.

The internals of the stick are pretty solid, albeit a bit dated looking, with through-hole components everywhere. There are only 5 wires coming from the stick, and opening it up revealed a bunch of micro-controllers doing whatever multiplexing stuff they have to. I would have to extend all of the wires to get to my button array and discard the microcontrollers in the handle as well as the main controller.

<img src=https://gerryk.sdf.org/site_images/2015-02-13%2012.55.07.jpg />

At some stage, I would also like to replavce the X and Y pots with hall-effect angle-sensors. These are far less noisy and spiky than pots, particularly 18 year old pots. The pots can be seen in this next image, along with the now-defunct controller board.

<img src=https://gerryk.sdf.org/site_images/2015-02-13%2012.10.44.jpg />

A pot swap would be almost trivial, but the sensors are expensive, so I will focus on making the joystick 21st century compatible first.

I used an Arduino Pro Mini for the brains of the conversion, as the Pro Mini has the capability to report itself as any USB device it likes. This allows it to behave as a USB HID Game Controller - Joystick in simple terms. However, the Arduino only has 12 digital inputs, but the F22 has 4 4-way hats and 5 buttons, one of which is the 2-stage trigger. There are a number of ways to solve this, but I went with the diode array, where the switches exist at the intersections of rows and columns, with each of the 6 rows and 6 columns going to a digital input. This uses the 12 inputs, but gives us 36 swiitches.

The schematic looks like this.

And the actual board looks like this.

<img src=https://gerryk.sdf.org/site_images/2015-02-27%2011.30.13.jpg />

Back side of the board

<img src=https://gerryk.sdf.org/site_images/2015-02-27%2011.30.20.jpg />

With the columns all connected

<img src=https://gerryk.com/node/Image%20URL%20Herehttps://gerryk.sdf.org/site_images/2015-02-27%2015.47.26.jpg /><img src=https://gerryk.sdf.org/site_images/2015-02-27%2015.47.26.jpg />

The next stage is to extend the wiring from each button in the handle to a connection in the array.
<a href=http://gerryk.com/node/45>Part 2 can be found here.</a>


