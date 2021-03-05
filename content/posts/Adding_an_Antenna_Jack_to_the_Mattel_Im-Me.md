---
title: "Adding an Antenna Jack to the Mattel Im-Me"
date: 2016-02-10T15:10:00+01:00
draft: false
---

The hugely <a href=https://hackaday.com/tag/im-me/>hackable</a> <a href=http://service.mattel.com/us/technicalproductdetail.aspx?catid=519&amp;prodno=L7281&amp;siteid=27>Girltech Im-Me</a> has been used for many <a href=http://ossmann.blogspot.ie/2010/03/16-pocket-spectrum-analyzer.html>interesting</a> <a href=http://travisgoodspeed.blogspot.ie/2010/03/im-me-goodfet-wiring-tutorial.html>hacks</a>. However the internal antenna leaves a lot to be desired, being basically a little piece of wire. Having the ability to connect antennas for the specific frequency range you are interested in does a lot to improve receive sensitivity and transmit range.

Once opened, I removed the little wire antenna which was soldered to the point;<strong>highlighted in red</strong>;below. I then scraped back some solder mask from the groundplane nearby to which I was going to solder the coax shield,;<strong>highlighted in blue</strong>.

<img alt= src=https://gerryk.sdf.org/site_images/2016-02-09%2013.49.29.jpg />

I then drilled out a spot on the front of the lower housing that I thought might have enough clearance from the components in the top housing and passed the SMA connector through. I then secured it with a nut&amp;lock washer, stripped back the external insluator, a bit of shield and some inner insulator and tinned the various parts I was going to solder. I then soldered the inner conductor to the point the original antenna had been connected to, and the shield to the place I had exposed some groundplane.

<img alt= src=https://gerryk.sdf.org/site_images/2016-02-09%2013.49.41.jpg />

<img alt= src=https://gerryk.sdf.org/site_images/2016-02-09%2013.58.03.jpg />

Finally I routed the little wires internally to prevent any damage and reassembled. The wires poking out at the bottom of the device are soldered to the debug port to allow flashing using a <a href=http://goodfet.sourceforge.net/hardware/goodfet31/>GoodFET</a> or some such device.

<img alt= src=https://gerryk.sdf.org/site_images/2016-02-09%2014.09.54.jpg />

