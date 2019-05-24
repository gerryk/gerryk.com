---
title: "a small matching unit to use the watson w2000 triband antenna on 70mhz"
date: 2016-05-17T15:34:00+01:00
draft: false
---
I recently upgraded my shack to an;<a href=http://www.eham.net/reviews/detail/12742>ICOM IC7300</a>, which in the EU specification includes the 4 meter / 70MHz band. I do not have a vertical for 4m, or space for one right now, but had read about others using a small matching unit to provide the necessary match using the;<a href=http://www.diamondantenna.net/v2000a.html>Diamond V2000</a>, or Watson W2000, as my version is badged. Two blogs I got my inspriation from are;<a href=http://ea4eoz.blogspot.ie/2012/09/using-v2000-triband-antenna-on-70-mhz.html>Miguel EA4EOZ's blog</a>;and that of;<a href=http://ei4dib.blogspot.ie/2015/09/70-mhz-antenna-tuning-unit-for-4-meter.html>Tony EI4DIB</a>, so having done some reading, and some rummaging in the junk box to see if I had the requisite parts, I got to work.
I first wound an inductor... estimating by eye from the work of Tony and Miguel. I used a pen with a diameter around 8mm, and wound 4 turns, spaced around 3mm. I then stripped down a rubbish old antenna switch, which provided a case and some SO239s.
<img src=https://dl.dropboxusercontent.com/u/32770/2016-05-17%2012.19.43.jpg />
I then drilled some holes to hold the variable capacitors. I had a few dual-gang units I bought from GQRP with 60pF on one gang and 140pF on the other. I ended up using the 60pF gang from one cap on the antenna side and the 140pF from the other cap on the TX side.
<img src=https://dl.dropboxusercontent.com/u/32770/2016-05-17%2012.40.29.jpg />
Once these were mounted, as I was using a C-L-C Pi circuit I connected the two centres of each socket to the appropriate gang of the caps.
<img src=https://dl.dropboxusercontent.com/u/32770/2016-05-17%2013.35.09.jpg />
I then added the inductor, again, soldered between the two centre pins of the co-ax connectors.
<img src=https://dl.dropboxusercontent.com/u/32770/2016-05-17%2013.40.12.jpg />
Finally, I wired the earths of the capacitors to the earth tags of the coax connectors
<img src=https://dl.dropboxusercontent.com/u/32770/2016-05-17%2013.45.41.jpg />
A few tweaks of the capacitors, and both the rig and the inline meter are happy with the match.
<img src=https://dl.dropboxusercontent.com/u/32770/2016-05-17%2013.50.22.jpg />
<img src=https://dl.dropboxusercontent.com/u/32770/2016-05-17%2013.50.31.jpg />
This was with 10W of FM at 70.25MHz. The W2000 has some small capacitors in the matching section in the base, and I do not want to risk toasting them.
