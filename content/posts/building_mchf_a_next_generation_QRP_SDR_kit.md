---
title: "Building MCHF: A next-generation QRP SDR kit"
date: 2019-01-10T15:02:38+01:00
draft: false
---

A while ago, while browsing Ham Radio channels on Youtube, I came across an interesting project. Chris, M0NKA, an obviously talented hardware designer had designed a QRP Software Defined Radio (SDR) based on the STM32F407 from STMicroelectronics.


The STM32F407 is a System On a Chip (SoC) that includes a Cortex M4 CPU core running at 200MHz, and some high-speed DAC/ADCs, capable of up to 7Msamples/sec, so a good candidate for a single-stage superhet Software based radio. I continued looking at videos of various builds, and comparative tests between the mcHF (the name for this kit) and other radios, such as Yaesu's FT817. The comparative tests showed this radio in a very good light, with sensitivity across the HF band of better than -130 dBµV. Not bad at all for what is basically a non-commercial hobbyist radio.


There are a number of ways to get your own mcHF. You can download the Gerbers and fabricate or order boards from one of the many PCB fabrication services. You can purchase a set of boards and provide your own components, or you can order a 'full kit' which comprises a set of boards with all the SMD components already in place, almost all of the remaining components which must be installed by the builder. These include a voltage regulator, an LCD screen and the various UI components; buttons and rotary encoders. There is nothing stopping the builder from substituting components for others of the same specification... for instance, some replace the provided tuning encoder with a more substantial unit, since this will probably see a lot of usage.


Boards and kits may be ordered from Chris M0NKA at his website http://www.m0nka.co.uk/ which also has other resources such as a gallery of mcHF builds and a comprehensive Downloads section containing the design and build documents along with links to firmware builds that can be installed on the radio. On the topic of firmware, there is a very active community that has, in the Open Source way, taken the initial code developed by Chris and run with it, adding features such as FM modulation and demodulation, a waterfall display to supplement the existing panadapter display, USB audio and rig-control and many other tweaks and enhancements. The firmware is maintained at a github repository, where builds, documentation and a bug tracker can be found: https://github.com/df8oe/mchf-github/wiki


The boards are GBP8 each (1x UI, 1x RF) + postage


The Full Kit is GBP259 + postage. This includes everything you need except the finals (2x RD16HHF1), a speaker, case and knobs. There are a number of cases available through the community including files to 3D print your own, if you have access to a 3D printer. There is also a very nice complete case kit that includes knobs, a speaker, buttons and a nice aluminium case available from some Chinese suppliers.


Having researched and determined that this would be not just a fun build but would be a capable and performant addition to the shack, I decided to liquidate some unused gear to get myself an mcHF kit, and a few days after placing the order, the package arrived. All of the components are individually packaged and labelled, making the initial inventory very straightforward.

[IMG]

The two boards have all of the Surface Mount Devices already installed from the factory, so all that remains is to install some connectors, rotary encoders and pushbuttons, wind and fit a bunch of toroids for the LPF and SWR sensors and install the LCD, a couple of afternoon's work at most. The boards are well laid out, and have the various stages, such as receive pre-amp, transmit driver & PA and mixer stage silkscreened so that they are easily identified. This will doubtless be handy for any future diagnosis.

[IMG]

I started by winding the toroids and the task I hate most, scraping the enamel off the wire to expose the copper. I then measured each on my MFJ259b, and adjusted where necessary. I then soldered them to the RF board. I then did the same for the SWR measurment toroids and stripped a couple of pieces of RG174 to make the sensing elements. These were then soldered in place.


There were a few other items to wind, transformers for the PA and so forth. These were duly wound and soldered.

[IMG]

Once this was all completed, I soldered the buttons and encoders in place on the UI board, along with a couple of LEDs for TX & RX indication.

[IMG]

I then finally soldered the various connectors and jacks in place.

[IMG]

I ordered a case from a member of the community on Yahoo Groups (https://uk.groups.yahoo.com/neo/groups/M0NKA-mcHF/info) and a set of buttons from Farnell, who do free shipping in Ireland these days. I also ordered the finals (2x RD16HHF1) from Box73.de, who are a recommended supplier. Some of the commmunity had strange issues with what seem to be counterfeit parts and I didn't want to take that risk. These have yet to arrive, but when they do arrive, I will follow up with a post on the last stages of construction and the testing. Meanwhile, here is how it looks without its case...

[IMG]

Part 2 of this write-up can be found here.




