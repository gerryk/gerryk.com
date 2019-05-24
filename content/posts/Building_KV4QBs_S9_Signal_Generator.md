---
title: "Building KV4QB's S9 Signal Generator"
date: 2017-08-16T10:47:00+01:00
draft: false
---
65,I have previously talked about the highly informative blog run by <a href=http://kv4qb.blogspot.ie/>DuWayne Schmidlkofer KV4QB</a>. He often publishes board designs which he is happy for people do reproduce using their PCB house of choice. In the past I have built his <a href=https://gerryk.com/node/57>Scalar Network Analyser</a>, which has proved to be invaluable when tuning filters and building antennas. He has another project that I thought would be a very useful tool to have for any radio amateur interested in building their own rigs. This is his take on a receiver;test oscillator. The idea behind this is that it generates a signal at a known level, or often a number of levels, so that a receiver may be aligned. He has taken inspiration from both Elecraft and NorCal projects, and the result is his S9 Signal Generator.

As with most of KV4QB's projects, he doesn't provide a kit or boards, just design files, so my first task was to download the provided EagleCAD files and convert them to Gerber format. I use Gerbers because they are accepted by many of the Chinese PCB houses, who tend to be substantially cheaper than the US based houses like OshPark. I have used SeeedStudio and DFRobot in the past, but decided to try a newcomer, PCBGogo.;

The conversion process involved opening the EagleCAD file using EagleCAD, and then using the CAM (Computer Aided Manufacturing) tool to generate layer files which represent each stage of the manufacturing process. These layers define board dimension, copper tracks, solder-masking, pad-tinning, silk-screened legends, drills and plate-through &amp; vias. Once these have been generated - I used the;<em>gerb274x</em> CAM tool for the layers, and the <em>Excellon</em> tool for the drills - the files are combined into a single;<em>zip</em>;file and uplloaded to the PCB order. When ordering, it is posible to select a number of options: board thickness, solder-mask colour, substrate type, controlled-impedance. In my case, I selected a red solder mask and 1.6mm FR4, both of which were no-cost options. About a day after sending the order I got an email notifying me that the designs had passed their design-rule acceptance, basically a statement they the boards make sense at a mechanical level - there are no holes outside the board, and so forth. About two weeks later, I received my order.

<img alt=PCBs data-entity-type=file data-entity-uuid=0ad8a765-5704-4f73-9bc3-c71fa71b3587 src=/sites/default/files/inline-images/1-800px.jpg />

While waiting for the boards to arrive, I used DuWayne's schematic to create an order from Farnell for the parts I didn't have to hand. I often order SMDs in 10x rather than one-off quantities, since the unit cost is much lower like this, and you get a bunch of components to bulk out the parts-box. The parts arrived in due course, actually the following day, with Farnell's usual free shipping.

My first task was to find a suitable enclosure... the boards are designed to fit in an Altoids tin, so I rooted out one I had used for a previous project. It needed a little tidying up, but once that was done looked prefect. I marked out and drilled the various holes I would use for mounting and passing the SMA RF port through.

<img alt=test fit data-entity-type=file data-entity-uuid=6a20b355-9a9b-41b1-b937-86243f9c41ea src=/sites/default/files/inline-images/2-800px.jpg />

Soldering the components was a very quick and painless process. DuWayne generally specifies larger SMD components. In this case, 1206 size, which are about 3.5mm x 1.6mm, so by SMD standards, huge. Where through-hole components are used, rather than having holes, the PCB has larger pads, allowing me to bend the leads at a right-angle and solder them in an SMD manner also.

<img alt=fully built data-entity-type=file data-entity-uuid=6378be3d-8e72-4a0e-beb5-99e8223ab058 src=/sites/default/files/inline-images/8-800px.JPG />

The circuit is a relatively simple one... it has 4 crystals, or at least provision for 4... I only had one to hand, but an order with GQRP will soon rectify that. The crystals feed to a selector, which is basically a dual-row header which uses a jumper to select the crystal. This then feeds a simple oscillator based on a 2N3904 NPN, which in turn feeds to two switchable selectable pi-attenuators, with the attenuation levels being -14dB and -20dB respectively. These are also selected or de-selected through the use of jumpers. The design should generate signals at around S0 and S9 with -14dB and -20dB as intermediate levels in between.

When I initially finished the build, I plugged it into my Spectrum Analyser, and where I was expecting a spike saw nothing. I visually inspected the board, and being a simple circuit was able to verify it pretty quickly. The only other possibilities were the transistor and diode which when tested with a multimeter also proved OK. So these were not the;only possible cuplrits... maybe the crystal was faulty. I had another crystal I could use, a <a href=https://en.wikipedia.org/wiki/Colorburst#Crystals>colour-burst crystal I</a> had received from <a href=http://soldersmoke.blogspot.ie/>Bill M0HBR</a> a few years back. It was currently doing duty in a <a href=http://soldersmoke.blogspot.ie/2011/03/return-of-michigan-mighty-mite.html>Michigan Mighty-Mite 80m CW transmitter</a>, but a few seconds with a soldering iron soon liberated it. I soldered it in place and at last had my signal visible on the Spectrum Analyser. The 'S9' signal shows up at ~-65dBm, which is about what is expected. I then plugged it into the antenna port of my Icom IC7300 to see what it made of it. Sure enough a nice clean signal at about 3.59MHz at about S8. With both attenuators in place, it showed an S0 signal - perfect.

<img alt=SA data-entity-type=file data-entity-uuid=0b97b4ee-7c8c-44f4-8d8b-fafd82c1224d src=/sites/default/files/inline-images/7-800px.JPG />

<h5>Signal on Spectrum Analyser</h5>

<h5><img alt=S9 data-entity-type=file data-entity-uuid=81c3757a-6df8-42f2-bf47-cae2d2db1d9a src=/sites/default/files/inline-images/4-800px.JPG /></h5>

<h5>S8 signal on ICOM IC7300</h5>

<h5><img alt=S0 signal data-entity-type=file data-entity-uuid=74c8766c-94d7-4b6d-a259-b539ab5f3d0e src=/sites/default/files/inline-images/5-800px.JPG /></h5>

<h5>S8 signal on ICOM IC7300</h5>

Many thanks to DuWayne for yet another enjoyable and useful project.

;

<strong>Farnell Bill of Materials</strong>

<h4>;</h4>

<h4><strong>
<style type=text/css><!--td {border: 1px solid #ccc;}br {mso-data-placement:same-cell;}-->
</style>
</strong></h4>

<table border=1 cellpadding=0 cellspacing=0 dir=ltr xmlns=http://www.w3.org/1999/xhtml>
<colgroup>
<col width=100 />
<col width=100 />
<col width=100 />
<col width=100 />
</colgroup>
<tbody>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;R1&quot;}>R1</td>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;3K9&quot;}>3K9</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1100206}><a href=http://ie.farnell.com/welwyn/wcr1206-3k9fi/res-thick-film-3k9-1-0-25w-1206/dp/1100206 target=_blank>1100206</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;R2&quot;}>R2</td>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;10K&quot;}>10K</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:2073878}><a href=http://ie.farnell.com/multicomp/mcmr12x1002ftl/res-ceramic-10k-1-0-25w-1206/dp/2073878 target=_blank>2073878</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;R3&quot;}>R3</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:15}>15</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:2078989}><a href=http://ie.farnell.com/welwyn/asc1206-15rft5/res-thick-film-15r-1-0-25w-1206/dp/2078989 target=_blank>2078989</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;R4&quot;}>R4</td>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;20K&quot;}>20K</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:2057774}><a href=http://ie.farnell.com/panasonic-electronic-components/erj8enf2002v/res-thick-film-20k-1-0-25w-1206/dp/2057774 target=_blank>2057774</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;R5&quot;}>R5</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:470}>470</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:9240489}><a href=http://ie.farnell.com/yageo-phycomp/rc1206jr-07470rl/res-thick-film-470r-5-0-25w-1206/dp/9240489 target=_blank>9240489</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;R6&quot;}>R6</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:56}>56</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:2057808}><a href=http://ie.farnell.com/panasonic-electronic-components/erj8geyj560v/res-thick-film-56r-5-0-25w-1206/dp/2057808 target=_blank>2057808</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;R7, R9&quot;}>R7, R9</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:62}>62</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:2307801}><a href=http://ie.farnell.com/panasonic-electronic-components/erj8enf62r0v/res-thick-film-62r-1-0-25w-1206/dp/2307801 target=_blank>2307801</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;R8&quot;}>R8</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:240}>240</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1100174}><a href=http://ie.farnell.com/welwyn/wcr1206-240rfi/res-thick-film-240r-1-0-25w-1206/dp/1100174 target=_blank>1100174</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;R10&quot;}>R10</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:120}>120</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1576617}><a href=http://ie.farnell.com/multicomp/mchp06w2f1200t5e/res-thick-film-120r-1-0-5w-1206/dp/1576617 target=_blank>1576617</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;R11, R12&quot;}>R11, R12</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:75}>75</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:2057810}><a href=http://ie.farnell.com/panasonic-electronic-components/erj8geyj750v/res-thick-film-75r-5-0-25w-1206/dp/2057810 target=_blank>2057810</a></td>
</tr>
<tr>
<td>;</td>
<td>;</td>
<td>;</td>
<td>;</td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;C1&quot;}>C1</td>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;33pF&quot;}>33pF</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:2320894}><a href=http://ie.farnell.com/multicomp/mc1206n330j500ct/cap-mlcc-c0g-np0-33pf-50v-1206/dp/2320894 target=_blank>2320894</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;C6, C7, C8&quot;}>C6, C7, C8</td>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;0.01uF&quot;}>0.01uF</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1759350}><a href=http://ie.farnell.com/multicomp/mc1206b103k500ct/cap-mlcc-x7r-10nf-50v-1206/dp/1759350 target=_blank>1759350</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;C5, C9, C10&quot;}>C5, C9, C10</td>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;47pF&quot;}>47pF</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:2295749}><a href=http://ie.farnell.com/nte-electronics/2n3904/rf-transistor-npn-40v-250mhz/dp/2295749 target=_blank>2295749</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;C4 &quot;}>C4</td>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;10pF&quot;}>10pF</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1206}>1206</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:2320889}><a href=http://ie.farnell.com/multicomp/mc1206n100j500ct/cap-mlcc-c0g-np0-10pf-50v-1206/dp/2320889 target=_blank>2320889</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;D1&quot;}>D1</td>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;1N4148&quot;}>1N4148</td>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot; &quot;}>;</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:1621821}><a href=http://ie.farnell.com/multicomp/1n4148w/diode-small-signal-75v-sod-123f/dp/1621821 target=_blank>1621821</a></td>
</tr>
<tr>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;Q1&quot;}>Q1</td>
<td data-sheets-value={&quot;1&quot;:2,&quot;2&quot;:&quot;2N3904&quot;}>2N3904</td>
<td>;</td>
<td data-sheets-value={&quot;1&quot;:3,&quot;3&quot;:2295749}><a href=http://ie.farnell.com/nte-electronics/2n3904/rf-transistor-npn-40v-250mhz/dp/2295749 target=_blank>2295749</a></td>
</tr>
</tbody>
</table>

