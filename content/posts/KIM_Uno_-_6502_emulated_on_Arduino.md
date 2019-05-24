---
title: "KIM Uno - 6502 emulated on Arduino"
date: 2014-12-04T13:25:00+01:00
draft: false 
---

When I was young, about 11, I was lucky enough to be bought a;<a href=http://en.wikipedia.org/wiki/Commodore_64>Commodore 64</a>, the computer that introduced a generation to computers, and likely launched thousands of careers in computing, mine included. It wasn't long before I started to feel constrained by the very;<a href=http://en.wikipedia.org/wiki/Commodore_BASIC>basic version of BASIC</a>;that it ran... 2 character variable names, no labels, no loops apart from FOR, no allowances to structured programming whatsoever. However, help was at hand, in the form of the<a href=http://www.commodore.ca/manuals/c64_programmers_reference/c64-programmers_reference.htm>Commodore 64 Programmer's Reference Guide</a>, and;<a href=http://www.commodore.ca/commodore-history/jim-butterfield-meet-jim-butterfield/>Jim Butterfield</a>'s;<a href=http://www.atarimagazines.com/compute/issue32/082_1_SUPERMON_64.php>Supermon 64</a>;machine language monitor. I remember keying in Supermon 64 from the pages of;<a href=https://archive.org/details/compute-magazine>Compute!</a>;magazine... my mentor and educator for many years, and remember clearly the vast speed increases to be had from running machine language code versus BASIC.
Since then, things have changed so much... I do much of my coding in Python and Java running on multi-cored monsters that live in air conditioned data centres, and capable of speeds that are beyond ridiculous, and yet I still feel a great deal of nostalgia for simple CPUs that can be coded directly with no scheduler or process management to be concerned with. Arduinos deliver some of the fix I miss, as does the Raspberry Pi, but I really miss the;<a href=http://6502.org/>6502</a>.

One day, while browsing, I came across a site,;<a href=http://obsolescence.wix.com/obsolescence>Obsolescence Guaranteed</a>, wherein the site owner described his adventures in;<a href=http://obsolescence.wix.com/obsolescence#!kim-uno-summary/c1uuh>creating an emulation of the Computer That Started It All</a>, as far as I am concerned. The;<a href=http://en.wikipedia.org/wiki/KIM-1>KIM-1</a>;was released by Commodore in 1976, when I was 5, and had little more than a CPU, a bit of memory, a hexadecimal keypad and display, and a serial port. Not exactly a monster or performance by today's standards, but back then, when you could easily blow a couple of hundred thousand on a PDP-11, or a few million on a 'big iron' System 360, this little thing was a revelation, and cheap at about $250.

Oscar, of Obsolescence Guaranteed seems to have as much fondness for old quirky computers as do I, but the KIM-UNO, basically an emulated 6502 and RAM running on an Arduino Mini Pro, with a simple circuit board for the keypad and display, was what really caught my eye. On getting in touch, I found out that a new run had been ordered and should be ready for shipping within a few days. Providence! It was clearly meant to be, so I paypal'd €25 for the kit, and a box and USB-TTL cable, and 6 or so days later had my prize.

I strongly recommend the documentation be read before beginning, or a critical step may be missed. Aside from that, it's a simple build, albeit with loads of solder joins to be made for the keypad. An hour or so of soldering and it's done, ready to be started up... (yes, I know some of the leads could be trimmed better, but I need to get a new side-cutter).

<img alt=KIN UNo data-entity-type=file data-entity-uuid=9a77e645-b217-48e3-9fb0-ef41a1a379ff src=/sites/default/files/inline-images/2014-11-28%2012.44.40.jpg />

So back to my roots, I go.

