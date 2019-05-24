---
title: "SBC6120 - RetroBrew Computers Edition"
date: 2017-06-08T13:49:00+01:00
draft: false
---
63,Following on from <a href=https://gerryk.com/node/58>here</a>. Farnell were typically swift with their turnaround wit most of the components arriving within a couple of days. I was not so timely, in either building out the board or writing it up, but better late than never... I had also ordered a CF to IDE interface. There is an IDE interface on the SBC board, but these days, it's hard to find an IDE drive, and who wants a spinning platter with all of its attendant power consumption issues when a little bit of flash memory would do just as;well. This took its time arriving, so I did as much soldering as I could in the meantime. I had ordered sockets for all of the ICs, so I started out by soldering these in place. I then followed with the various capacitors, resistors, jumpers, fuses and the two crystal oscillators. Compared to many of the projects I have worked on, which have been primarily SMD, the size and spacing of the through-hole components was positively roomy. This made for a quick and problem-free build. The final steps were to install the status LEDs, power connector and reset button, and we are ready to go, from a hardware perspective at least.

<img alt=SBC6120 board built up data-entity-type=file data-entity-uuid=eb4ddbbc-0b93-4092-aec4-c32bf8ba2b7b src=/sites/default/files/inline-images/2017-03-28%2011.18.32-1.jpg />

I have a 1GB Compact Flash card which will be my storage device. This can be partitioned into multiple disks using the SBC6120 Monitor Program. The Monitor Program is executed on boot, and once fully booted, the system drops you to a console prompt where monitor commands may be executed. Full documentation on teh Monitor Program can be read in Bob Armstrong's original SBC6120 documentation.

Partitioning the CF card is done using the;<em>df</em>;command in the Monitor.;<em>df </em>stands for Disk Format, and takes 1 parameter... the disk partition to format.

From the SBC6120 manual, we can see the following command definition:

<em><strong>5.8.3 RF (Format RAM Disk) and DF (Format IDE Disk)</strong>
.
.
.
Format
&gt;RF u ⇒ format RAM disk unit u
&gt;DF pppp ⇒ format IDE disk partition pppp</em>

Each disk partition is 2,097,152 bytes in size, which means that on my 1GB CF Card, I could have a maximum of around 50;partitions. This is probably far more that would be necessary to store every bit of PDP8 software and data out there... we shall see. There is a whole lot of PDP8 software <a href=http://www.pdp8.net/images/index.shtml>here</a>, mostly as either tape or disk image format. However, for my purposes at the moment, the OS/8 and Games images <a href=https://www.grc.com/pdp-8/os8utils-sbc.htm>provided by Steve Gibson</a> are enough to get started.

;

;

