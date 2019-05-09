---
title: "Flashing OpenWRT on TPlink 703n v1.7"
date: 2014-11-10T12:04:00+01:00
draft: true
---

I recently bought a TPLink WR703n as they are a nice, inexpensive, and very hackable little device. I have a few projects in mind for this, including playing with;<a href=http://hak5.org/?s=pineapple>Hak.5's Wifi Pineapple</a>. Pretty much all the hacks require flashing with OpenWRT.
\n
\nWhen I started my research, I discovered that some versions of the 703n can be bricked by OpenWRT. They are not actually fully bricked, as in completely unresponsive, but they boot with the LAN disabled, and therefore are uncontactable. It is possible to recover using the serial port, but this requires a bit of soldering, and is really not for the faint-of-heart.
\n
\nThe hardware that is susceptible is version 1.7. To add further complication, some devices that are labelled 1.6, are in fact really 1.7 devices under the hood. As a result, it is important to do a bit of probing to see what the actual version is. A couple of different scenarios may exist -;
\n
\n1. If the device is running the original Chinese firmware, the build version reading as follows - ;Build 120925 will correspond to a v1.7 firmware.
\n
\n2. If the device is shipped with dd-wrt pre-installed, it is possible to login over telnet The default login/password are root/admin. Once logged in, the following command will list the version -;
\n
\n<span style=font-family:Courier New,Courier,monospace;># grep -a U-Boot /dev/mtd0ro | cut -d'I' -f1;;;;;</span>
\n
\nA version 1.7 can be identified by a build date Sep 25 2012.
\n
\nIn my case, to further complicate the situation, the build version was -
\n
\n<span style=font-family:Courier New,Courier,monospace;>U-Boot 1.1.4 (Jun 19 2013 - 21:54:34)</span>
\n
\nThe usual 1.7 build id is;121204, there are some 1.6 builds reported as;130318 and;130321, whereas this is 130625. As a result, I I figured the prudent thing to do would be to flash a version of OpenWRT that would ensure compatibility with 1.7, while retaining compatibility with earlier hardware. The version that meets these criteria is the 12-09 build of OpenWRT - Attitude Adjustment branch. This can be downloaded from here:;<a href=http://downloads.openwrt.org/attitude_adjustment/12.09/ar71xx/generic/openwrt-ar71xx-generic-tl-wr703n-v1-squashfs-factory.bin>http://downloads.openwrt.org/attitude_adjustment/12.09/ar71xx/generic/op...</a>
\n
\nWhile doing my research, I came across the failsafe uboot project. The purpose of this is to provide a featureful recovery system to help with those failed flashes and other brick-generating events. I decided to go ahead and flash this image also. I came across a post on OpenWRT discussing an interesting uboot with a web-gui failsafe mode. The thread is here:;<a href=https://forum.openwrt.org/viewtopic.php?id=43237>https://forum.openwrt.org/viewtopic.php?id=43237</a>
\n
\nThe code repo for the uboot is here:;<a href=https://github.com/pepe2k/u-boot_mod>https://github.com/pepe2k/u-boot_mod</a>
\n
\nA precompiled binary for the 703n can be downloaded here:;<a href=https://app.box.com/s/z13rrr8v8vdu70la67jn>https://app.box.com/s/z13rrr8v8vdu70la67jn</a>
\n
\nOnce downloaded, the image needs to be modified. The MAC address of the router needs to be inserted. Thankfully, though, scripts exist to do this.
\nI will reproduce a script from;<a href=http://zhujunsan.net/index.php/2013/08/install-web-failsafe-u-boot-for-wr703n/>here</a>;for convenience:
\n
\n<span style=font-family:Courier New,Courier,monospace;>#! /bin/sh
\n#high chance need have a change ...
\nUBOOT_NAME=wr703n_tuboot_test_2012_06_06.bin
\nMD5SUM_SHOULD_BE=623dc0bba6fab68c22e5fb2f329d7d09
\n#need check the md5sum,any one byte in bootloader shoud right ...
\nCURRENT_MD5SUM_VAL=$( md5sum $UBOOT_NAME |awk '{print $1 }' )
\necho $UBOOT_NAME md5sum : $CURRENT_MD5SUM_VAL
\nif [ $MD5SUM_SHOULD_BE = $CURRENT_MD5SUM_VAL ]; then
\n; echo $UBOOT_NAME md5sum check pass
\nelse
\n; echo ###############$UBOOT_NAME md5sum check fail###############
\n; exit
\nfi
\nRAW_UBOOT_LEN=`wc -c $UBOOT_NAME | awk '{print $1 }'`
\nNEED_PAD_LEN=$((0x1fc00-$RAW_UBOOT_LEN))
\n#Generate a file used as pad ...
\ndd if=/dev/zero of=pad.bin bs=1 count=$NEED_PAD_LEN
\ncat $UBOOT_NAME pad.bin &gt;tuboot_0x1fc00.bin
\necho Backup some config first,just like MAC address ...
\ndd if=/dev/mtd0 of=./config.bin bs=1 skip=$((0x1fc00))
\ncat ./tuboot_0x1fc00.bin ./config.bin &gt;uboot_0x20000.bin</span>
\n
\nThis script needs to be run on the router, as it pulls data from the existing uboot. The script will create;<em>uboot_0x20000.bin</em>, which is the file we want to flash. Prior to running, UBOOT_NAME and MD5SUM_SHOULD_BE need to be updated to the values for your downloaded binary.
\n
\nThe commands I ran to update the image and flash it are as follows. My commands in bold.
\n
\n<span style=font-family:Courier New,Courier,monospace;>root@DD-WRT:~/flash#;<strong>sh update-image.s</strong>h
\n64512+0 records in
\n64512+0 records out
\nBackup some config first,just like MAC address ...
\n1024+0 records in
\n1024+0 records out
\n
\n
\nroot@DD-WRT:~/flash#;<strong>ls</strong>
\nconfig.bin ; ; ; ; ; ; ; pad.bin ; ; ; ; ; ; ; ; ;tuboot_0x1fc00.bin ; ; ;;
\nuboot_0x20000.bin ; ; ; ;uboot_for_tl-wr703n.bin ;update-image.sh
\n
\n
\nroot@DD-WRT:~/flash#;<strong>cat /proc/mtd</strong>
\ndev: ; ;size ; erasesize ;name
\nmtd0: 00020000 00010000 RedBoot
\nmtd1: 003c0000 00010000 linux
\nmtd2: 002e0000 00010000 rootfs
\nmtd3: 00020000 00010000 ddwrt
\nmtd4: 00010000 00010000 nvram
\nmtd5: 00010000 00010000 board_config
\nmtd6: 00400000 00010000 fullflash
\nmtd7: 00020000 00010000 fullboot
\n
\n
\nroot@DD-WRT:~/flash#;<strong>mtd write uboot_0x20000.bin mtd0</strong>
\nUnlocking mtd0 ...
\nWriting from uboot_0x20000.bin to mtd0 ... ;[w]
\n
\n
\nroot@DD-WRT:~/flash#;<strong>grep -a U-Boot /dev/mtd0ro | cut -d'I' -f1</strong>
\nU-Boot 1.1.4 (Jun 19 2013 - 21:54:34)
\n7▒AP121 (AR9331) U-Boot for TL-WR703N
\nroot@DD-WRT:~/flash#</span>
\n
\nOnce this is completed, we can continue in to flash the firmware. I downloaded it from here ;<a href=http://downloads.openwrt.org/attitude_adjustment/12.09/ar71xx/generic/openwrt-ar71xx-generic-tl-wr703n-v1-squashfs-factory.bin>http://downloads.openwrt.org/attitude_adjustment/12.09/ar71xx/generic/op...</a>;to a local webserver and downloaded to the router from there. I renamed it to something shorter while doing this.
\nSequence of commands below... my input in bold.
\n
\n<span style=font-family:Courier New,Courier,monospace;>root@DD-WRT:/tmp#;<strong>wget http://192.168.1.222/files/openwrt.bin</strong>
\nConnecting to 192.168.1.222 (192.168.1.222:80)
\nopenwrt.bin ; ; ; ; ;100% |
\n**************************************************************************
\n**************************************************************************
\n*******| ;3840k ;0:00:00 ETA
\n
\nroot@DD-WRT:/tmp#;<strong>mtd -r write openwrt.bin linux</strong>
\nUnlocking linux ...
\nWriting from openwrt.bin to linux ... ;[w]
\nConnection to 192.168.1.1 closed by remote host.
\nConnection to 192.168.1.1 closed.
\n
\n
\nroot@erdos:~ $;<strong>telnet 192.168.1.1</strong>
\nTrying 192.168.1.1...
\nConnected to 192.168.1.1.
\nEscape character is '^]'.
\n;=== IMPORTANT ============================
\n; Use 'passwd' to set your login password
\n; this will disable telnet and enable SSH
\n;------------------------------------------
\n
\n
\nBusyBox v1.19.4 (2013-03-14 11:28:31 UTC) built-in shell (ash)
\nEnter 'help' for a list of built-in commands.
\n
\n; _______ ; ; ; ; ; ; ; ; ; ; ________ ; ; ; ;__
\n;| ; ; ; |.-----.-----.-----.| ;| ;| ;|.----.| ;|_
\n;| ; - ; || ;_ ;| ;-__| ; ; || ;| ;| ;|| ; _|| ; _|
\n;|_______|| ; __|_____|__|__||________||__| ;|____|
\n; ; ; ; ; |__| W I R E L E S S ; F R E E D O M
\n;-----------------------------------------------------
\n;ATTITUDE ADJUSTMENT (12.09, r36088)
\n;-----------------------------------------------------
\n; * 1/4 oz Vodka ; ; ;Pour all ingredients into mixing
\n; * 1/4 oz Gin ; ; ; ;tin with ice, strain into glass.
\n; * 1/4 oz Amaretto
\n; * 1/4 oz Triple sec
\n; * 1/4 oz Peach schnapps
\n; * 1/4 oz Sour mix
\n; * 1 splash Cranberry juice
\n;-----------------------------------------------------
\nroot@OpenWrt:/#</span>
\n
\nSuccess!
\n