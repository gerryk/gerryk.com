---
title: "mcHF: a Next-Generation QRP SDR kit - Part II"
date: 2017-03-13T13:01:00+01:00
draft: false
---
59,Since the <a href=https://gerryk.com/node/52>last post</a>, I had gotten involved in a <a href=https://www.facebook.com/groups/1794230080790075/>Facebook group with a focus on the mcHF transceiver</a>. As well as being a great forum for sharing knowledge and experiences, it gave me the opportunity to get a very nice case in a group buy organised by one of the members. The case is 2-part design, which is easier to work with than the one I bought ;previously. It also comes with buttons, a speaker and very nice machined aluminium knobs.

<img alt=mcHF Case data-entity-type=file data-entity-uuid=943a8d78-a838-439a-ac10-4135b4b32553 src=/sites/default/files/inline-images/2016-11-16%2013.07.10-800.jpg />

<em>The case from the Group Buy</em>

;

The RD16HHF1s also arrived, so I started out by installing them and biasing. The biasing procedure is well documented on the <a href=https://github.com/df8oe/mchf-github/wiki/Adjustment-and-Configuration-Manual>github site</a>, and involves reading the quiescent current, and then transmitting;an unmodulated carrier, increasing;the bias setting until the current increases by 500mA over the previously noted quiescent current.

Once this is done, the settings for 5W transmit and full power, which can mean anything from 6 or 7W to 20W depending on band, driver FET and some transformer modifications that are documented on the Yahoo group, are configured in the software. At this point you are ready to transmit.

However, I still wanted to fit the case. Mainly for protection, but also because the heavy lumps of aluminium I was using for heak-sinking the regulators and final transistors were putting strain on the legs of the devices, and i really did not want to break them. Fitting the case was relatively straightforward. I first installed the speaker, with a small JST connector allowing it to be disconnected from the RF board if necessary. I then removed some of the panels to allow the boards to be fitted. They fitted easily. Once I had bolted the output transistors and regulators to the inside of the case, which provides heat-sinking, I bolted the small spacers and the RF shield to the UI board, and attached the UI board to the RF board which was in-situ in the case. I then fitted the side-pieces, which have the necessary holes for connectors already cut out. Finally I fitted the top cover, and stumbled on my first gremlin. The key-switches supplied in the kit are too long for the case I was using, which resulted in some of the buttons being activated by the case! I ordered replacements on Farnell's site, which does free next-day-delivery to Ireland. Once these were fitted, the shorter button stems, and the higher activation force (260g) meant that no unwanted activations were caused by the case.

<img alt=RF Shield data-entity-type=file data-entity-uuid=93fc87b3-3132-4d6a-985c-8acd9816a51a src=/sites/default/files/inline-images/2016-11-22%2015.50.12-800.jpg />

<em>Fitting the boards and RF shield</em>

;

<img alt=Side view data-entity-type=file data-entity-uuid=784bdabd-0cf6-4caa-9980-d2d30d98f448 src=/sites/default/files/inline-images/2016-11-16%2019.32.46-800.jpg />

<em>Side view, showing fitted spacers</em>

;

<img alt=Test fit data-entity-type=file data-entity-uuid=0da673a5-dee8-40cc-b90a-0768ffbfe580 src=/sites/default/files/inline-images/2016-11-16%2019.54.56-800.jpg />

<em>Test fit, showing incorrect button stem length problem</em>

;

I had read of an issue with the polyfuse specified in the kit, which being a non-resettable type, could blow leaving the radio inoperative until the fuse was replaced, so I ordered a fuse-holder and some 3A slow-blow fuses to replace the little SMD until. I also ordered a 1024Mbit serial EPROM which is used to store configuration. There is flash storage on the ST Micro CPU, but flash degrades, and I would sooner replace an SOIC-8 unit than a 100pin CPU when the flash dies. I added these and performed a small modification, involving running two bodge-wires from the CPU to SMD pads which enables the touchscreen functionality.

<img alt=touchscreen mod data-entity-type=file data-entity-uuid=80ffa73c-723c-4450-b76f-d3f919c03109 src=/sites/default/files/inline-images/2016-10-29%2014.50.00_0.jpg />

<em>Touchscreen mod and Serial EPROM (seen on top left)</em>

;

<img alt=touchscreen detected data-entity-type=file data-entity-uuid=a321bb9d-1f10-458e-b6e7-6f5c7f59d479 src=/sites/default/files/inline-images/2016-10-29%2015.42.07.jpg />

<em>Settings screen showing Touchscreen Detected</em>

;

Once this was completed, I updated the software. DF8OE runs a github which has the newest revision of both the software and documentation. The newer software includes a bootloader that allows flashing direct from USB flash drive rather than having to plug the radio into a computer. So much more convenient. The newer firmware also adds functionality such as FreeDV and a more useable spectrum view. The software is in heavy development so updates are frequent and sometimes quite substantial. This makes the USB update feature very useful indeed.

I needed a microphone to use with the radio, and having acquired a nice little unit at a recent radio rally, opened it up to rewire it to work with the mcHF. This was just a matter of swapping the leads around, as the radio can work with either dynamic or electret capsules. In this case, the capsules in the microphone is an electret type, which requires a 5V bias voltage to operate. This is enabled by soldering a 680ohm resistor to position R6 on the main board. I had one of these to hand, and fitting it was a matter of minutes... a testament to the design of both the case and the 2-part board layout. When I reassembled the radio, added power and plugged it into a dummy load to try a test transmission, I came across another issue. Distortion, and lots of it. After a bit of analysis, I determined that the compression and mic-gain settings were far too high. Reducing these brought the transmitted audio into spec, so I did some tests to determine what power I was getting on each band. On 80, 40, 30 and 20m, at full power, the mcHF is putting out just over 10W, on the remaining bands, the power decreases slightly to give about 8W on 10M.

<img alt=microphone bias enable data-entity-type=file data-entity-uuid=518fad89-255b-4883-8bca-f3a099dbee5f src=/sites/default/files/inline-images/2016-10-29%2014.49.55.jpg />

<i>Addition of 680ohm resistor to enable microphone bias voltage</i>

;

Using my Red Pitaya, I noted a little oscillation when using the 'tune' functionality. This is visible as harmonic content where there should be a single carrier. Winding down the power settings to about 4W while using the 'tune' feature reduces this distortion to almost nothing, but many people on the forums have demonstrated that the pin-diode switching allows RF feedback which causes distortion. I have purchased an Omron relay with which I will replace the diode switching to completely eliminate the feedback and distortion. For now, though, it is well within acceptable parameters, being 70dB down on the fundamental.

Some forum users have done various other modifications which I may try in the future. One has added lighting in the form of lit buttons. I think I may just add some LEDs under the case top, which will show through the transclucent rubber buttons that came with the case. Others have modified the output transformer and driver transistors to give higher power levels, up to 20W. I may also try this in the future, but would like to operate the radio as it stands for a while before I start 'enhancing' it.

All in all, the entire experience was both enjoyable and educational. The kit as provided by Chris M0NKA is of excellent quality and design, but the very active community around it ensures that there are continued developments and design improvements fed back into the project. In fact, the boards are now at Rev. 0.6, where the kit I started out at are Rev. 0.5. The newer version includes a new preamp. design which reduces possible distortion levels. This can be added to the 0.5 board quite easily also.

