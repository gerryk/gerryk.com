---
title: "Using Ghidra to Reverse Engineer Wifi Pineapple Protection"
date: 2019-05-09T08:40:00+01:00
draft: false
---

I prefer to build my own hack-tools. Partly because I am a cheapskate and partly because it is more educational. One device I have often thought of replicating but until recently hadn't gotten round to it is the Wifi Pineapple from Hak5. This is basically a productified Wifi Attack Platform / Rogue Access Point. In past blog posts I had read that it is based on OpenWRT, and that the hardware is almost identical to the much cheaper GL-Inet AR-150 Wifi Router.

I had foound builds of v1.1.x and v.2.0.x on the Internet that installed fairly easily over uBoot. I wanted to keep up with the latest and greatest, however, so needed to find a way to build my own firmware image. A bit of searching turned up this very detailed blog post: https://oct8l.gitlab.io/posts/2019/54/making-a-knockoff-wifi-pineapple-from-a-gl-inet-ar150m/

The steps outlined are clear and easy to follow, and soon I had a firmware image based on OpenWRT and Wifi Pineapple 2.5.4 (the newest release). I installed it and had a browse around. It seemed much like what I had seen with earlier versions of the firmware, so I tried starting the PineAP module to try out some of the functionality only for it to fail. I had heard rumours that Hak5 were planning to implement some hardware verification to ensure that their code would not run on 'unofficial' hardware, so maybe this was why I was having issues... time for a bit of probing.

I ssh'd onto the router and first browsed through the PineAP module. First looking at the html to see what happens when the 'enable' switch is toggled on. This calls a PHP function enablePineAP().

{{< figure src="https://i.imgur.com/jORK9KB.png" title="PineAP PHP Code" >}}

This in turn contains calls to /etc/init.d/pineapd. This is a standard SysV init script that in turn calls /usr/sbin/pineapd, which when I tried running manually SegFaulted. So there is either some bug or the SegFault is a result of the hardware verification. Time to dig deeper...

{{< figure src="https://i.imgur.com/FbBfKoK.png" title="PineAP init.d script" >}}

In the not too distant past, the US National Security Agency released their Software Reverse Engineering suite, Ghidra, to the world. Ghidra has the capability of disassembling and decompiling binaries for CPU architectures other than Intel's x86 and x86_64, including the MIPS family, of which the CPU in thw AR-150 and Wifi Pineapple is a member. Worth a shot, right?

I loaded up Ghidra and created a new project. I then loaded the pineapd binary and opened the disassembler window, selected the binary and let Ghidra do its analysis. It correctly identified the binary as being an elf binary for the MIPS CPU Architecture, and sure enough displayed the assembly code in the main window. I scrolled down looking for an entry poiny and after a bit found what seemed to be a function definition for main(). After a few more seconds, the decompilation window was populated with C code generatd by the decompiler. I guess there must be some debug symbols included in the binary since some of the variables and function names were meaningful rather than __function__001() and so forth, as often seen in decompiled code.

Near the top of main() I noticed a call to strcmp() with the comparison string being 'WIFI_PINEAPPLE_NANO', A couple of lines back I saw a call to a function getBrd() which returns the string being searched for the comparison string. 

{{< figure src="https://i.imgur.com/xSk713J.png" title="getbrd() function" >}}

Looking at this function shows that it is looking at /proc/cmdline to determine part of the board id. /proc/cmdline is the kernel boot parameter list, and sure enough, one of the parameters is 'AR-150' where I guess the code would prefer to find 'WIFI_PINEAPPLE_NANO'

Looking back at main() there is another function call to getid() which when we examine it shows a shell-out to examine the first few lines of dmesg to look for an alphanumeric string. The significance of the string is unknown... perhaps a build id, but it seems that unless the expected strings are found in the expected places, the SegFault will be generated and the binary fail to execute.

{{< figure src="https://i.imgur.com/IyUbwbc.png" title="Output of /prod/cmdline & dmesg" >}}

The next step is to try at arrive at some sustainable workaround. Patching the binary in-place might work, but it would be easy to circumvent this and the test may exist in other code also so each would need to be analysed and patched individually. Another possible alterative might be to patch OpenWRT to ensure that the Kernel returns the expected values when interrogated. I think this is the approach worth pursueing. 
