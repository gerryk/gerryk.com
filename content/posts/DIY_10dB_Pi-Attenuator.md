---
title: "DIY 10dB Pi-Attenuator"
date: 2017-02-09T09:26:00+01:00
draft: false
---
Attenuators are expensive, especially the fancy calibrated ones, and it seems that they are the only ones available. SMD resistors are cheap, though, and I have SMA connectors, so I thought I would try to make my own. I used the calculator;<a href=http://leleivre.com/rf_pipad.html>here</a>, to come up with a design that used resistors I had, gave an impedance of 50 ohms and an attenuation that was useful (10dB). The schematic for the attenuator is as follows.;
<img alt=pi attenuator data-align=center data-entity-type=file data-entity-uuid=2ef3598c-a29b-4113-b3fd-0bb34a5e578b src=/sites/default/files/inline-images/Pi-attenuator-pad.jpg />
The formulas to calcuate R1, R2 and R3 are:;

R1=R3= Z ( K-1/K+1);

R2= 2 Z ( K / K<sup>2</sup>;- 1);

And in my case, the values I got (while selecting for resistors I already had) are R1 = R3 = 100ohm, and R2 = 75ohm.

I built it up on a pair of SMA connectors with a bit of PCB soldered to the bottom to give a bit of rigidity. I will eventually replace this with some heavy copper or tin sheet, which I will be able to fully enclose the device with. This is how it currently looks.
<img alt=10dB Attenuator data-align=center data-entity-type=file data-entity-uuid=4a243508-de0e-4342-ba87-071657a6cd26 src=/sites/default/files/inline-images/2017-02-12%2016.28.39.jpg />
I did some measurements on my scope. I took readings at 2MHz and 20MHz and found an attenuation of very close to 10dB in both cases.

At 2MHz, I read a peak-to-peak voltage of 10.5V when fed direct from my signal generator. With the attentuator inline, I measured a peak-to-peak voltage of 3.28V, which is very nearly 10dB of attenuation.;

Direct reading...
<img alt=direct reading at 2MHz data-align=center data-entity-type=file data-entity-uuid=76f6133b-e18b-4c5f-af70-e6a5b4c60f11 src=/sites/default/files/inline-images/2017-02-12%2016.25.21.jpg />
Attenuated reading...
<img alt=attenuated reading at 2MHz data-align=center data-entity-type=file data-entity-uuid=4cd6d643-ce4f-4f02-ab17-174737011b25 src=/sites/default/files/inline-images/2017-02-12%2016.24.31.jpg />
At 20MHz, the figures were very similar... 9.92V p-p direct, and 3.2V attenuated. Slightly less attenuation, but close enough for my purposes.

Direct reading...
<img alt=direct reading at 20MHz data-align=center data-entity-type=file data-entity-uuid=b7ffa4bf-a9d7-4e7d-96da-cfc01a1828f9 src=/sites/default/files/inline-images/2017-02-12%2016.26.09.jpg />
Attenuated reading...
<img alt=attenuated reading at 20MHz data-align=center data-entity-type=file data-entity-uuid=5cb4eb36-f7b8-4298-b365-614f32ad1e66 src=/sites/default/files/inline-images/2017-02-12%2016.26.58.jpg />
This attenuator is not designed to handle power, but will be ideal for use with a reflection bridge and Red Pitaya for use as a Vector Network Analyser.
