---
title: "Building KV4QB's SNA Jr II"
date: 2017-02-17T08:49:00+01:00
draft: false
---
57,I came across the highly informative and interesting website of <a href=http://kv4qb.blogspot.ie/2016/05/sna-jr-version-ii-part-1.html>DuWayne KV4QB</a> through Bill Meara M0HBR who has the excellent Ham Radio podcast <a href=http://soldersmoke.blogspot.ie/>Soldersmoke</a>. DuWayne has documented many projects on his site, but one that caught my attention is the SNA Jr II. An SNA is a Scalar Network Analyser, which is a device that has the capability to measure RF amplitude. The SNA Jr II is the second iteration of this project by DuWayne, and is based on a number of enexpensive modular components. The brain of the device is an Arduino Nano, display is courtesy of a small 1.8 TFT, control through a push-button rotary encoder, and signal generation is provided by the Analogue Devices AD9850, and the RF power measurement is done by another Analogue Devices component, the AD8307. The AD8307 can take as input an RF signal up to 13dBm, and as low as -70dBm so has quite a wide range. It first became widely known in the Amateur Radio community when Wes Hayward W7ZOI <a href=http://www.qsl.net/df7tv/pm8307.html>published his design for a power meter</a> using this component. These devices are all available through eBay.

DuWayne has published PCB designs and a Bill of Materials for his SNA Jr II. He also uploaded the Eagle PCB files to OshPark, so ordering a batch is a very simple matter. In my case, though, I thought I could get a cheaper deal by shopping around. I have used Chinese supplier DFRobot for other components in the past, and found them very reliable, and they also do PCB fabrication, so I though I might try them. There was a little stumbling block however... they require Gerber files for PCB manufacture rather than the files created by EagleCAD. EagleCAD has, however, the capability to generate Gerber files using its CAM (Computer Aided Manufacturing) module. Gerber files are basically vector files describing each layer of the manufacturing process... copper tracks, solder masking, silk-screening and drills.;

It took about 3 weeks for my PCBs to arrive, and on inspection, they look perfect. For less than half the cost of OshPark, including;postage. In the meantime, I had ordered the rest of the passive components from Farnell, who do free shipping to Ireland. I had the main modules already to hand, so was ready to start construction.


<img alt=pcbs data-entity-type=file data-entity-uuid=3c720ce4-456d-405d-85df-dd2875e04ef3 src=/sites/default/files/inline-images/fig1-800px.jpg />

<em>PCBs arrived from DFRobot</em>

The build was relatively quick, since the SMD components are on the larger size (1206), and there is not a huge amount to solder. All in all it took about an hour. I had a aluminium case in the junkbox which I Dremelled to permit access to the screen and drilled to allow the encoder shaft to peek through. Once this was done assembly was straightforward. I had a 7.2V LiPo from an old RC helicopter lying around, so that was co-opted for power.

<img alt=board built up data-entity-type=file data-entity-uuid=c7b4f2fa-5a51-4966-9261-f2274e4f8388 src=/sites/default/files/inline-images/fig2-800px.jpg />

<em>PCB built</em>

<img alt=board fully assembled data-entity-type=file data-entity-uuid=2e2fa145-7fa5-43c5-bb08-4c398890ee7f src=/sites/default/files/inline-images/fig3-800px.jpg />

<em>SNA Jr II Assembled</em>

Once the software was uploaded to the Arduino, I quickly ran through the functionality. The SNA Jr. II can do the following:

<ol>
<li>
Measure filter response - a start and end frequency can be set and swept, with the output of the filter measured and a graph of response generated. It is capable of frequencies as high as 40MHz, so is well capable in HF frequencies.
</li>
<li>
Measure RF power - using a 40dB tap, the power output of a rig can be measured.
</li>
<li>
Measure antenna response and SWR - using a Return Loss Bridge, the response curve and SWR of an antenna can be plotted, assisting with tuning.
</li>
<li>
Measure resonance - using an additional coil the SNA Jr. II can behave as a DIP meter, measuring the resonance of a circuit.
</li>
</ol>

<img alt=menu display data-entity-type=file data-entity-uuid=258185f2-7971-4424-bec5-c66cd94bc866 src=/sites/default/files/inline-images/fig4-400px.jpg /><img alt=sweep display data-entity-type=file data-entity-uuid=a03082ff-5bb0-4130-b2ee-cb5cde0d792a src=/sites/default/files/inline-images/fig5-400px.jpg />

<em>Display functions</em>

I had the parts to build the Return Loss Bridge to hand, so assembled that also and look forward to better weather so I can use it in erecting the 80m loop I have planned.

<img alt=rlb data-entity-type=file data-entity-uuid=799cc1c9-aacc-49db-baec-9c22c014a002 src=/sites/default/files/inline-images/fig6-800px.jpg />
<em>Return Loss Bridge</em>

<img alt=rlb in  case data-entity-type=file data-entity-uuid=eff9a86c-3db9-4e2d-be31-18dec82f4391 src=/sites/default/files/inline-images/fig7-800px.jpg />

<em>Return Loss Bridge</em>

;

