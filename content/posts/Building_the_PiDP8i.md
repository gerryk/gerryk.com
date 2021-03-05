---
title: "Building the PiDP8i"
date: 2015-07-23T13:53:00+01:00
draft: false
---
The story leading up to this can be read;<a href=http://gerryk.com/node/48>here</a>. In short though, I have always had a thing for retro computers, and DEC boxes in particular, and now I have a remake of a PDP8/I in the form of a kit provided by Oscar Vermeulen another retro computing geek with an excellent site at;<a href=http://obsolescenceguaranteed.blogspot.ie/>Obsolescence Guaranteed</a>.

<img src=https://gerryk.sdf.org/site_images/2015-07-21%2007.08.35.jpg />

I finally received the kit, and once unboxed and inventoried, I referred to the build instructions on Oscar's site, and to the PiDP8 Google Group, where other builders documented their experiences and build tips. The kit includes a perspex front panel with beautifully garish 60s graphics in orange and brown, a PCB on which all the various LEDs and switches are mounted along with the Raspberry Pi, which runs the simh emulator - the brain of the machine. It also includes a nice wooden - bamboo, I think - case for everything to live in when assembled.
<img src=https://gerryk.sdf.org/site_images/2015-07-22%2019.24.02.jpg />There are 26 switches on the front-panel to provide data-entry and run-control. These need to be soldered to the panel. When building the original series of prototypes, Oscar had a few small difficulties keeping the switches nicely aligned. A member of one of the Swiss hackerspaces suggested popping out the switch pivot and threading the switches en-masse onto an appropriately sized bar.;

Oscar provided a small brass bar, about 2mm in diameter for this purpose, and described how to cut and remove the pivot and use a screwdriver to keep the switch together while threading onto the bar.

<img src=https://gerryk.sdf.org/site_images/2015-07-22%2020.15.29.jpg />Rinse and repeat 26 times, and it's done.;
Once this was completed, the next job was to insert the terminals into the board and tack-solder the two end switches, Then, moving along from switch to switch, I;aligned each, ensured a close-fit and soldered. I did this slowly, and checked multiple times to ensure good alignment, and spacing. While not perfect, I am pretty happy with the result. I will mask up and paint later, when I get the correct type pf paint.<img src=https://gerryk.sdf.org/site_images/2015-07-22%2021.47.08.jpg />
The next step was to solder in the rest of the components... first the diodes and resistors...

<img src=https://gerryk.sdf.org/site_images/2015-07-23%2019.33.34.jpg />

Then the LEDs... all 89 of them. There's a trick to doing these right. They are the star of the show, after all, so it's important to get them nicely aligned. My solution was to fit a row, supporting it from underneath with once of the blocks of wood that will eventually mount the PCB. I wasn't too concerned about getting the alignment right initially... I tacked in one leg in each LED, then when a row was complete, held the board in one hand and re-melted the solder while pushing from underneath to ensure a nice flush-fit with the PCB.;

<img src=https://gerryk.sdf.org/site_images/2015-07-23%2019.42.11.jpg />

<img src=https://gerryk.sdf.org/site_images/2015-07-23%2019.42.24.jpg />

It didn't take all that long, and the result looks nice...

<img src=https://gerryk.sdf.org/site_images/2015-07-23%2020.12.48.jpg />

The final few stages involved soldering in a driver IC for the LEDs and the 40way header that will accept the Pi's GPIO pins.;

<img src=https://gerryk.sdf.org/site_images/2015-07-23%2020.39.45.jpg />

I then attached the wooden blocks that will support the PCB, and drilled the necessary holes in the back of the case to accept the screws and USB cable to supply power.

<img src=https://gerryk.sdf.org/site_images/2015-07-23%2021.08.19.jpg />

Pi fitted...

<img src=https://gerryk.sdf.org/site_images/2015-07-23%2021.46.25.jpg />

I drilled holes through the PCB to allow screws to be screwed in...;

<img src=https://gerryk.sdf.org/site_images/2015-07-24%2008.57.48.jpg />

<img src=https://gerryk.sdf.org/site_images/2015-07-24%2008.57.45.jpg />

Then screwed in the screws... these will be used for the magnetic attachment of the front panel as suggested by;<a href=https://groups.google.com/d/msg/pidp-8/xAWE7pxFARg/rAz26ATe-RYJ>Chris Smith on the PiDP/8 Group</a>.

<img src=https://gerryk.sdf.org/site_images/2015-07-24%2008.59.11.jpg />

<img src=https://gerryk.sdf.org/site_images/2015-07-24%2008.59.18.jpg />

Then glued two small magnets to the back of the panel, at the appropriate places...

<img src=https://gerryk.sdf.org/site_images/2015-07-24%2011.54.35.jpg />

...and we're done! Well, almost... I still need to get paint and paint the switches, but it works.

<img src=https://gerryk.sdf.org/site_images/2015-07-24%2014.43.16.jpg />

