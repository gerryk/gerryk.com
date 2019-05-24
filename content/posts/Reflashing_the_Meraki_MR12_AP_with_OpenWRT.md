---
title: "Reflashing the Meraki MR12 AP with OpenWRT"
date: 2017-01-30T22:45:00+01:00
draft: false
---
Meraki (now part of Cisco) are well known for their high-quality enterprise grade networking hardware. Over the last number of years, they have been promoting their kit by way of providing 'evaluation' units for the cost of simply attending a webinar. They specify that the attendee should be a 'networking professional', but it is possible that not every attendee is.
I recently acquired a number of these, where the evaluation period had expired, and the cloud-management interface was no longer accessible without a license key. This in effect makes the unit useless. Unless...
There is a build of;<a href=https://github.com/riptidewave93/Openwrt-MR12>OpenWRT CC available for the MR12 and MR16</a>;Access Points, and it turns out it is not too hard to flash. All you need is the build images, a serial to USB convertor with flying leads, and a TFTP server.
A serial consle is exposed over a debug port on the main board, and connecting a serial lead and configuring a terminal as 15200,8,n,1 is enough to get access. Pressing a key during boot will halt the boot process and drop the user to an 'emergency' prompt.
At this prompt, it is possible to do a 'test' boot without flashing... this is good practise, since once you flash, if there is a problem, it is difficult to recover.
In the 1.3 release of riptide_wave's build, there are images for boot and to flash.

To boot from TFTP: <em>openwrt-ar71xx-generic-mr12-initramfs-uImage.bin</em>
To flash to the device: <em>openwrt-ar71xx-generic-mr12-kernel.bin &amp; openwrt-ar71xx-generic-mr12-rootfs-squashfs.bin</em>

The command to enter at the recovery prompt to boot is:

<span style=font-family:Courier New,Courier,monospace;>tftpboot 0x81000000 openwrt-ar71xx-generic-mr12-initramfs-uImage.bin; bootm</span>

Once the unit boots, log in and verify the behaviour before flashing, which can be done using these commands:

<span style=font-family:Courier New,Courier,monospace;>tftpboot 0x80010000 openwrt-ar71xx-generic-mr12-kernel.bin;erase 0x9fda0000 +0x240000;cp.b 0x80010000 0x9fda0000 0x240000
tftpboot 0x80010000 openwrt-ar71xx-generic-mr12-rootfs-squashfs.bin;erase 0x9f080000 +0xD20000;cp.b 0x80010000 0x9f080000 0xD20000
setenv bootcmd bootm 0x9fda0000; saveenv; boot</span>

When the system boots at the end, you have a full OpeWRT/LuCI build available. The default IP is 192.168.1.1

<h3>Session Transcript</h3>


<span style=font-family:Courier New,Courier,monospace;>[ 58.980000] random: nonblocking pool is initialized</span>

<span style=font-family:Courier New,Courier,monospace;>U-Boot 1.1.4-g0c3911dd (Mar 3 2011 - 17:08:51)</span>

<span style=font-family:Courier New,Courier,monospace;>PB93 (ar7241 - Virian) U-boot
DRAM:
sri
ar7240_ddr_initial_config(133): virian ddr1 init
#### TAP VALUE 1 = 0x2, 2 = 0x2 [0x1440010: 0x10000000]
64 MB
Top of RAM usable for U-Boot at: 84000000
Reserving 272k for U-Boot at: 83fb8000
Reserving 192k for malloc() at: 83f88000
Reserving 44 Bytes for Board Info at: 83f87fd4
Reserving 36 Bytes for Global Data at: 83f87fb0
Reserving 128k for boot params() at: 83f67fb0
Stack Pointer at: 83f67f98
Now running in RAM - U-Boot at: 83fb8000
id read 0x100000ff
flash size 16MB, sector count = 256
Flash: 16 MB
*** Warning - bad CRC, using default environment</span>

<span style=font-family:Courier New,Courier,monospace;>In: serial
Out: serial
Err: serial
Net: ag7240_enet_initialize...
Fetching MAC Address from 0x83fe7ea0
Virian External MII mode MDC CFG Value ==&gt; 6
: cfg1 0xf cfg2 0x7014
eth0 link down
eth0: 00:03:7f:e0:00:2a
ATHRSF1_PHY: PHY unit 0x0, address 0x4, ID 0xd04e,
ATHRSF1_PHY: Port 0, Neg Success
ATHRSF1_PHY: unit 0 port 0 phy addr 4
eth0 up
eth0
RESET is un-pushed
Hit any key to stop autoboot: 0
ar7240&gt;
ar7240&gt; tftpboot 0x81000000 openwrt-ar71xx-generic-mr12-initramfs-uImage.bin; bootm
Trying eth0
Using eth0 device
TFTP from server 192.168.1.101; our IP address is 192.168.1.1
Filename 'openwrt-ar71xx-generic-mr12-initramfs-uImage.bin'.
Load address: 0x81000000
Loading: len bad 52 &lt; 60
#################################################################
#################################################################
#################################################################
#################################################################
#################################################################
#################################################################
#################################################################
#################################################################
#################################################################
#################################################################
###
done
Bytes transferred = 3339055 (32f32f hex)
## Booting image at 81000000 ...
Image Name: MIPS OpenWrt Linux-3.18.11
Created: 2015-05-09 15:35:10 UTC
Image Type: MIPS Linux Kernel Image (lzma compressed)
Data Size: 3338991 Bytes = 3.2 MB
Load Address: 80060000
Entry Point: 80060000
Verifying Checksum ... OK
Uncompressing Kernel Image ... OK
No initrd
## Transferring control to Linux (at address 80060000) ...
## Giving linux memsize in bytes, 67108864</span>

<span style=font-family:Courier New,Courier,monospace;>Starting kernel ...</span>

<span style=font-family:Courier New,Courier,monospace;>[ 0.000000] Linux version 3.18.11 (riptide_wave@BuildBox1) (gcc version 4.8.3 (OpenWrt/Linaro GCC 4.8-2014.04 r45651) ) #2 S5
[ 0.000000] bootconsole [early0] enabled
[ 0.000000] CPU0 revision is: 00019374 (MIPS 24Kc)
[ 0.000000] SoC: Atheros AR7242 rev 1
[ 0.000000] Determined physical RAM map:
[ 0.000000] memory: 04000000 @ 00000000 (usable)
[ 0.000000] Initrd not found or empty - disabling initrd
[ 0.000000] Zone ranges:
[ 0.000000] Normal [mem 0x00000000-0x03ffffff]
[ 0.000000] Movable zone start for each node
[ 0.000000] Early memory node ranges
[ 0.000000] node 0: [mem 0x00000000-0x03ffffff]
.
.
.
[ 23.280000] eth0: link up (1000Mbps/Full duplex)
[ 23.280000] br-lan: port 1(eth0) entered forwarding state
[ 23.290000] br-lan: port 1(eth0) entered forwarding state
[ 23.310000] IPv6: ADDRCONF(NETDEV_CHANGE): br-lan: link becomes ready
[ 25.290000] br-lan: port 1(eth0) entered forwarding state</span>

<span style=font-family:Courier New,Courier,monospace;>BusyBox v1.23.2 (2015-05-09 10:22:11 CDT) built-in shell (ash)</span>

<span style=font-family:Courier New,Courier,monospace;>_______ ________ __
| |.-----.-----.-----.| | | |.----.| |_
| - || _ | -__| || | | || _|| _|
|_______|| __|_____|__|__||________||__| |____|
|__| W I R E L E S S F R E E D O M
-----------------------------------------------------
CHAOS CALMER (Bleeding Edge, r45651)
-----------------------------------------------------
* 1 1/2 oz Gin Shake with a glassful
* 1/4 oz Triple Sec of broken ice and pour
* 3/4 oz Lime Juice unstrained into a goblet.
* 1 1/2 oz Orange Juice
* 1 tsp. Grenadine Syrup
-----------------------------------------------------
root@OpenWrt:/#
[ 58.980000] random: nonblocking pool is initialized</span>

<span style=font-family:Courier New,Courier,monospace;>U-Boot 1.1.4-g0c3911dd (Mar 3 2011 - 17:08:51)</span>

<span style=font-family:Courier New,Courier,monospace;>PB93 (ar7241 - Virian) U-boot
DRAM:
sri
ar7240_ddr_initial_config(133): virian ddr1 init
#### TAP VALUE 1 = 0x2, 2 = 0x2 [0x1440010: 0x10000000]
64 MB
Top of RAM usable for U-Boot at: 84000000
Reserving 272k for U-Boot at: 83fb8000
Reserving 192k for malloc() at: 83f88000
Reserving 44 Bytes for Board Info at: 83f87fd4
Reserving 36 Bytes for Global Data at: 83f87fb0
Reserving 128k for boot params() at: 83f67fb0
Stack Pointer at: 83f67f98
Now running in RAM - U-Boot at: 83fb8000
id read 0x100000ff
flash size 16MB, sector count = 256
Flash: 16 MB
*** Warning - bad CRC, using default environment</span>

<span style=font-family:Courier New,Courier,monospace;>In: serial
Out: serial
Err: serial
Net: ag7240_enet_initialize...
Fetching MAC Address from 0x83fe7ea0
Virian External MII mode MDC CFG Value ==&gt; 6
: cfg1 0xf cfg2 0x7014
eth0 link down
eth0: 00:03:7f:e0:00:2a
ATHRSF1_PHY: PHY unit 0x0, address 0x4, ID 0xd04e,
ATHRSF1_PHY: Port 0, Neg Success
ATHRSF1_PHY: unit 0 port 0 phy addr 4
eth0 up
eth0
RESET is un-pushed
Hit any key to stop autoboot: 0
ar7240&gt; tftpboot 0x80010000 openwrt-ar71xx-generic-mr12-kernel.bin;erase 0x9fda0000 +0x240000;cp.b 0x80010000 0x9fda0000 0x24000
Trying eth0
dup 1 speed 1000
Using eth0 device
TFTP from server 192.168.1.101; our IP address is 192.168.1.1
Filename 'openwrt-ar71xx-generic-mr12-kernel.bin'.
Load address: 0x80010000
Loading: #################################################################
#################################################################
#################################################################
####################################
done
Bytes transferred = 1179648 (120000 hex)
Erase Flash from 0x9fda0000 to 0x9ffdffff in Bank # 1
First 0xda last 0xfd sector size 0x10000
253
Erased 36 sectors
Copy to Flash... write addr: 9fda0000
done
ar7240&gt; tftpboot 0x80010000 openwrt-ar71xx-generic-mr12-rootfs-squashfs.bin;erase 0x9f080000 +0xD20000;cp.b 0x80010000 0x9f08000
Trying eth0
Using eth0 device
TFTP from server 192.168.1.101; our IP address is 192.168.1.1
Filename 'openwrt-ar71xx-generic-mr12-rootfs-squashfs.bin'.
Load address: 0x80010000
Loading: #################################################################
#################################################################
#################################################################
#################################################################
#################################################################
#################################################################
#################################################################
######
done
Bytes transferred = 2359296 (240000 hex)
Erase Flash from 0x9f080000 to 0x9fd9ffff in Bank # 1
First 0x8 last 0xd9 sector size 0x10000
217
Erased 210 sectors
Copy to Flash... write addr: 9f080000
done
ar7240&gt; setenv bootcmd bootm 0x9fda0000; saveenv; boot
Saving Environment to Flash...
Protect off 9F040000 ... 9F04FFFF
Un-Protecting sectors 4..4 in bank 1
Un-Protected 1 sectors
Erasing Flash...Erase Flash from 0x9f040000 to 0x9f04ffff in Bank # 1
First 0x4 last 0x4 sector size 0x10000
4
Erased 1 sectors
Writing to Flash... write addr: 9f040000
done
Protecting sectors 4..4 in bank 1
Protected 1 sectors
## Booting image at 9fda0000 ...
Image Name: MIPS OpenWrt Linux-3.18.11
Created: 2015-05-09 15:26:58 UTC
Image Type: MIPS Linux Kernel Image (lzma compressed)
Data Size: 1132559 Bytes = 1.1 MB
Load Address: 80060000
Entry Point: 80060000
Verifying Checksum ... OK
Uncompressing Kernel Image ... OK
No initrd
## Transferring control to Linux (at address 80060000) ...
## Giving linux memsize in bytes, 67108864</span>

<span style=font-family:Courier New,Courier,monospace;>Starting kernel ...</span>

<span style=font-family:Courier New,Courier,monospace;>[ 0.000000] Linux version 3.18.11 (riptide_wave@BuildBox1) (gcc version 4.8.3 (OpenWrt/Linaro GCC 4.8-2014.04 r45651) ) #1 S5
[ 0.000000] bootconsole [early0] enabled
[ 0.000000] CPU0 revision is: 00019374 (MIPS 24Kc)
[ 0.000000] SoC: Atheros AR7242 rev 1
.
.
.
[ 26.920000] eth0: link up (1000Mbps/Full duplex)
[ 26.920000] br-lan: port 1(eth0) entered forwarding state
[ 26.930000] br-lan: port 1(eth0) entered forwarding state
[ 26.950000] IPv6: ADDRCONF(NETDEV_CHANGE): br-lan: link becomes ready
[ 28.930000] br-lan: port 1(eth0) entered forwarding state</span>

<span style=font-family:Courier New,Courier,monospace;>BusyBox v1.23.2 (2015-05-09 10:22:11 CDT) built-in shell (ash)</span>

<span style=font-family:Courier New,Courier,monospace;>_______ ________ __
| |.-----.-----.-----.| | | |.----.| |_
| - || _ | -__| || | | || _|| _|
|_______|| __|_____|__|__||________||__| |____|
|__| W I R E L E S S F R E E D O M
-----------------------------------------------------
CHAOS CALMER (Bleeding Edge, r45651)
-----------------------------------------------------
* 1 1/2 oz Gin Shake with a glassful
* 1/4 oz Triple Sec of broken ice and pour
* 3/4 oz Lime Juice unstrained into a goblet.
* 1 1/2 oz Orange Juice
* 1 tsp. Grenadine Syrup
-----------------------------------------------------
root@OpenWrt:/#
root@OpenWrt:/# passwd
Changing password for root
New password:
Retype password:
Password for root changed by root
root@OpenWrt:/#</span>

