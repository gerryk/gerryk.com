---
title: "One-Touch-Tune for FT897"
date: 2009-01-05T16:54:42+01:00
draft: false
---
My current HF setup is the Yaesu FT897D, MFJ 993B Auto ATU and 135' doublet in 'inverted V' configuration with the feedpoint at about 35' high. A good multiband setup which allows me to work locally on 80m and more DX on 40m and 20m.
The 993 handles antenna matching duty without a complaint, but the actual tuning procedure is a bit long-winded.
After selecting a frequency and having a listen, the first step is to change to AM (or any other carrier mode), then select menu 75 and reduce the power to about 30W so as not to fry the tuner or finals as we get a match. Then key the mic to give a carrier and wait for the ATU to do its thing. Then we change the mode back to whatever it was beforehand (USB/LSB depending on band) and set the power back to 100W. OK, so it probably happens a little more quickly than it may seem, but it's still a bit of a chore, particularly if you QSY a lot.
The solution... a single button press which will reduce the output power and key a carrier, returning back to the original settings on release. Nice, but not available as far as I'm aware. There does exist a circuit for the FT857 (basically the same radio in a different box), but it relies on a 'brown wire' in the DC connector which doesn't exist on the 897. Time for plan B.
While browsing the [FT897 Yahoo Group] (http://groups.yahoo.com/group/FT897/)I came across a file from DF1QQ containing a nice little circuit which purported to do what I require. The principle it is based on is that it uses the ACC port on the 897, which is basically a stereo jack. Grounding the tip keys a CW carrier... great... we're part of the way there, but we also need reduced power. The ring is an input for the AGC, normally used by linear amplifiers to prevent the radio overdriving, but in this case, DF1QQ cleverly feeds a negative voltage back to the AGC control, thus reducing the radio's output.
\nI built the circuit into a small aluminium case, along with a 100mA FSD meter, which serves as a remote S/PO/SWR meter. The controls are a momentary button and a pot. The pot controls the AGC feedback voltage, and set to about 12 o'clock gives us about 20W out.
\nNow when I change bands, re-matching is a simple matter of pressing a button... a vast improvement on the old method. Thanks DF1QQ.
