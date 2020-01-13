---
title: "Flashing the Arduino Bootloader to a Bluepill STM Board"
date: 2019-06-10T10:15:00+01:00
draft: false
---

Recently I have been seeing the 'Bluepill' STMicro based development board popping up more and more in projects. The 

Download Arduino IDE

Download STM_32 Utils

Copy to ~/Arduinno/hardware or ~/Documents/Arduino/hardware (Win + OSX)

Add SAM boards via board mgr.

Download st-link urils

Download bootloader firmware (I used default, LED13)

Connect as follows:

<img>

Flash using this command...

 .\st-flash write ..\generic_boot20_pc13.bin 0x8000000
