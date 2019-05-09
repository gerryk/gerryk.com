---
title: "Mobile APRS with Icom IC7100 and mobilinkd"
date: 2014-11-21T13:20:00+01:00
draft: true
---


28,I;used to have a bunch of radios in my car; an IC7000 for HF, a Kenwood TM D710 for APRS/VHF/UHF and a Cleartone CM7 ex-PMR for 4m AM/FM. They were installed relatively stealthily, but when I came across the successor to the IC7000, the IC7100, I saw how I could aggregate all of this into a single radio.
\nSo... long story short, I sold all the radios that were in the car and bought the;<a href=http://www.eham.net/reviews/detail/11080>IC7100</a>.;
\n
\nAll the basic functionality, HF, VHF/UHF etc was pretty much trivial, but my previous APRS setup included a Garmin Nuvi 350 for GPS, and had the APRS TNC built into the radio head. The IC7100 has no TNC, and the data port is in the radio body rather than the head, which meant another cable to run.
\n
\nSo... I did a bit of research, and came across;<a href=http://www.mobilinkd.com/>Moblinkd</a>, a fully featured TNC (based on an Atmel MPU) with Bluetooth! Cable problem sorted. I have an Android phone, so after more research, came across;<a href=http://aprsdroid.org/>APRSDroid</a>. So the GPS and mapping duties were also taken care of.
\n
\nOnce I received the TNC, I charged it (it has a built in battery... so handy for /P operation), and made up a cable to connect it to the ICOM rig. The cable looks like this:
\n
\n<img alt= src=https://dl.dropboxusercontent.com/u/32770/IC7100-Mobilinkd.png />
\n
\n
\nThe behaviour of the IC7100 means that when some device is connected to the DATA2 port, it will only respect the PTT line if the radio is set to DigitalFM (FM-D) mode, so there will be no rude data-bursts over your voice QSO. I haven't tested to see how quickly the IC7100 stops scanning, so I don't know if an incoming packet will be truncated or not. For the moment, I leave it on 144.800 (the Irish APRS frequency) when driving unless I want to talk to someone.
\n
\nOnce connected, I paired the;<a href=http://www.mobilinkd.com/>Mobilinkd;</a>with my phone over bluetooth, installed APRSDroid, and set up the connection to use bluetooth.;<a href=http://aprsdroid.org/>APRSDroid;</a>has a number of beaconing settings, but the standard Smartbeacon settings seem to do as required. The main views are the packet log and map. The log displays the raw packets, so maybe not the easiest to decode on the fly, especially if you receive packets from a weather station. The maps display uses Google Maps for its data, so looks good and functions well.
\n
\nIt is also possible to send and receive messages, so pinging one of your friends to have a voice QSO via APRS messaging is possible.
\n
\nI look forward to making up a lead to talk to my Baofeng B5 or Yaesu VX7 to do a bit of portable APRS.
\n