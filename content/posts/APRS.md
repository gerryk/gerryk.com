---
title: "APRS"
date: 2009-09-04T10:50:00+01:00
draft: true
---

APRS is often misunderstood to mean Automatic Position Reporting System, when, according to creator Bob Bruninga, WB4APR, it actually stands for Automatic Packet Reporting System. Some might maintain that the primary purpose of APRS is vehicle tracking and service position reporting, and, while this is not entirely untrue, it does sell short the possibilities of this excellent technology.
\nThe more obvious purposes to which APRS could be put to include announcing services... obviously, being somewhat limited to the Amateur Radio community, services of interest to them would be the first choice. Voice repeaters, meetings and nets or news readings can be announced both as waypoints, showing location, and as bulletin messages to the APRS user's inbox.

Further uses would be in point to point communication experiments. Combining APRS data with weather information and topology detail, using a program like RadioMobile, could create a very comprehensive picture of the environment and be very useful in recording and recreating experiments.

AREN activites would also be enhanced using APRS. The Galway VHF Group provides communication for many voluntary and charitable events, and the use of APRS for monitoring participants could prove invaluable. Couple this with the visual impact to the non-technical watcher, of a moving map display with the walkers/cyclists progress through the event being graphically depicted, and it can be seen that APRS is definitely a technology which has many proctical purposes for the Amateur Radio community.

<h3>My Station</h3>
My home APRS station consists of a laptop running UI-View32 connected to a PacComm Tiny2 TNC, which connects to a Yaesu FT2800 VHF transceiver and finally through an antenna switch to the Diamond tri-band vertical on the roof. This setup is pretty typical for a home station, although alternatives exist, such as Xastir for Linux.
I have my beacon set up to transmit every 30 minutes, and have the path set to WIDE2-2. This gives me a Time To Live of 2 hops, which is optimal, as there is an IGate at EI7IG 2 hops from me.
I also got a nice big map of Ireland from John, EI7IG, which plugs nicely into UI-View32 and gives a great overview of the country, while being big enough to show loads of detail.

Mobile, I use a Tracker2 from Argent Data connected on one side to a Garmin Nuvi 350 and on the other to an Alinco DR110, which is operating at low power (10W) into a 1/4 wave whip on the roof of the car.
The Tracker2 has the facility to plot waypoints received via APRS on the Nuvi, it will also receive messages and bulletins and display then on the Nuvi, and the Nuvi has an onscreen keyboard which can be used to compose messages to other APRS stations.
The Tracker2 is set to beacon my position between every 15 minutes to 20 seconds, depending on delta-v... I'm not being purposely obscure here, because it really does use changes in velocity to determine beacon frequency... speeding up, slowing down and changing direction will all have an effect on the rate that beacons are sent out. This has the effect of keeping a pretty accurate record of position, while not clogging up the digis when stationary. I have set a path of WIDE1-1,WIDE2-2, which has the effect of giving me 2 - 3 hops, even where legacy digis, that don't understand the WIDEn-N paradigm, are in use. This should be sufficient to get me to an IGate from anywhere in Ireland.

<h3>Projects</h3>
One project I am working on currently is a system whereby local items of interest can be plotted on the fly from my mobile station.
I have a Psion 5MX, which plugs into a serial port on the Tracker2, and am writing some Perl or Python scripts to transmit custom APRS packets which will notify other users of transient events such as traffic congestion or flooding. I believe that this will be a useful feature as APRS gains more penetration in the community.
