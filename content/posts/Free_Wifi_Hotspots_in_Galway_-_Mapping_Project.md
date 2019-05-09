---
title: "Free Wifi Hotspots in Galway - Mapping Project"
date: 2009-01-06T09:00:00+01:00
draft: false
---

As a learning exercise I decided to use the Google Maps API to
create something that might be useful. A guide to free wifi hotspots in
Galway. I had a bit of a google around and found one effort that had
been started and died in the same month, about 2 years ago. So, I
figured that the niche still needed to be filled and got to it.

Google provides APIs to many of their apps, Search, Maps and more
recently the Google Ajax Feed. I'll do something with that in the
future, but for now, I wanted to play with Maps.

For those of you who know Javascript, it's pretty quick and easy to
get stuck in, for those who don't, well, if you know any OO language,
you'll have enough to be getting on with.

When you apply for access to the API, you are given a sample code
snippet, which, when pasted into a page gives you a map, centred on
Google HQ or thereaboutsâ€¦ no good for my purposes, so I opened up
GEarth and zoomed over to Galway, found Eyre Square and grabbed the
co-ordinates. I then edited the sample code to create a map object
centred on these coordinates and there was Galway.

Pins can be added to the map, much as you would a real map on a
corkboard, and it was these I was going to use to mark the hotspot
locations. To do this, I created a marker object with the co-ordinates
of the hotspot. I then added a listener (which listens for clicks) to
pop up an address and further details. Finally, I added an overlay to
the map to display the marker. Great!one hotspot. Now I just rinse and
repeat for all the hotspots I know about and we're done.
