---
title: "Building DVMega Digital Voice Modem"
date: 2017-06-02T11:40:00+01:00
draft: true
---
62,Recently, one of the club members, Steve EI5DD has been showing a lot of interest in digital voice modes. So much interest, in fact, that he did up an introductory document outlining the details of and differences between the main modes in use in the Amateur Radio Community. These are DStar (the oldest, and most commonly on ICOM radios), Yaesu C4FM/System Fusion, and DMR. The latter, DMR, was originally for use in the Commercial market, but more recently thanks to very inexpensive transceivers from the likes of Tytera, interest has grown very rapidly in the Amateur Community.
\n
\nOne of my main interests in Ham Radio is building stuff. Sure, you can buy off-the-shelf devices to do whatever you need, but to me, the challenge and education inherent in building is a big bonus. Also, it has been said that time spent melting solder is not deducted from out time allotted on earth. Among the off-the-shelf offerings are SharkRF Openspot, DVMini and DVMega. DVMega also do boards that sit on top of an Arduino, and can be connected to a Raspberry Pi to handle getting traffic onto and off of the Internet. There are a number of options available for connecting to the various DV networks, but I decided on MMDVMHost, since it is Linux based and doesn't require a GUI.
\n
\nThe main DV networks include Brandmeister and DMR-MARC for DMR, XLX , DPlus which are DStar networks and YSFReflector and Wires-X which are Yaesu Fusion networks. There is some interoperability between networks, with reflectors and talkgroups often connecting to one or more networks, and even across network types.
\nBrandmeister is popular in Europe, so I decided that I would use this for DMR, and YSFReflector for Fusion.
\n
\nI ordered the Dual-band DVMega board, which supports either 2m or 70cm, but not at the same time, or cross-band. This sits on top of an Arduino. I used a Mega 2560, since I had one to hand. The Arduino needs to be flashed 
