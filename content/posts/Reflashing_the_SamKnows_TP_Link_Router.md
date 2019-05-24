---
title: "Reflashing the SamKnows TP Link Router"
date: 2017-01-20T22:44:00+01:00
draft: false
---
<a href=https://www.samknows.com/>SamKnows</a>;is a global Broadband Quality Monitoring service. They are funded by a number of national regulatory bodies, including the FCC and OfCom, and are to all intents unaffiliated. On sign-up, they will ship a heavily customised;<a href=http://www.tp-link.com/us/products/details/TL-WDR3600.html%3ETP%20Link%20N600%20router%3C/a%3E.%20The%20conditions%20of%20participation%20are%20that%20you%20leave%20this%20connected%20to%20your%20home%20broadband%20for%20two%20years,%20during%20which%20time%20it%20will%20gather%20metrics%20which%20are%20aggregated%20by%20SamKnows,%20who%20generate%20reports%20which%20can%20then%20presumably%20be%20used%20to%20encourage%20your%20carrier%20to%20improve%20their%20service.%20Once%20the%20two%20years%20have%20lapsed,%20the%20router%20is%20yours%20to%20keep.%3C/p%3E%3Cp%3EThis%20works%20fairly%20well...%20I%20have%20used%20these%20reports%20a%20number%20of%20times%20of%20the%20last%20two%20years,%20to%20often%20positive%20effect.%20However,%20now%20the%20two%20years%20are%20overr,%20I%20feel%20that%20I%20could%20put%20the%20router%20to%20better%20use.%20My%20choice%20of%20router%20firmware%20is%20%3Ca%20href=>OpenWRT</a>, mainly for its rich collection of addons and customisability. It might be a little harder to get to grips with than Tomato or dd-wrt, but I fell the additional functionality makes it worthwhile. A build of;<a href=https://downloads.openwrt.org/chaos_calmer/15.05.1/ar71xx/generic/openwrt-15.05.1-ar71xx-generic-tl-wdr3600-v1-squashfs-factory.bin>OpenWRT 15.05 (Chaos Calmer)</a>;exists for the provided router, a TP-Link TL-WDR3600 (N600), so downloading that is where I began.

Once downloaded, I renamed to 'tplink.bin' and left it in an accessible directory on my laptop. I then configured my laptop to a static address (192.168.1.2), and connected it directly to one of the LAN ports on the WDR3600. It is possible to set the SamKnows firmware into 'failsafe' mode, which sets the IP to 192.168.1.1 and exposes a telnet port with no password. This is achieved by powering the unit off, then powering back up... all of the LEDs will light up after a couple of seconds, and once they do, repeatedly pressing the Reset/WPS button on the back will eventually cause the little 'sun' LED, second from the left to start to flash rapidly... once this happens you are in failsafe and can log in.

The login and re-flash session was captured, and looks like this:

<span style=font-family:Courier New,Courier,monospace;>gerryk@feynman:~$ telnet 192.168.1.1
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^]'.</span>

<span style=font-family:Courier New,Courier,monospace;>=== IMPORTANT ============================
Use 'passwd' to set your login password
this will disable telnet and enable SSH
------------------------------------------</span>

<span style=font-family:Courier New,Courier,monospace;>BusyBox v1.19.4 (2015-02-03 17:28:09 GMT) built-in shell (ash)
Enter 'help' for a list of built-in commands.</span>

<span style=font-family:Courier New,Courier,monospace;>; ; ; ; ; ; ; ; ; ; ;_
;___ __ _ _ __ ___ ;| | ;; ;___ ;;__ ; ;_____ _____
/ __|/ _` | '_ ` _ \\| | / / '_ \\ / _ \\ \\ /\\ / / __|
\\__ \\ (_| | | | | | | ;&lt; ;| | | | (_) \\ V V /\\__ \\
|___/\\__,_|_| |_| |_|_| \\_\\_| |_|\\___/ \\_/\\_/ |___/
P E R F O R M A N C E M O N I T O R I N G</span>

<span style=font-family:Courier New,Courier,monospace;>OS: OpenWRT Attitude Adjustment, r35093
SW: WDR3600 Build
-------------------------------------------------
root@(none):/#
root@(none):/# mount_root
/sbin/mount_root: line 1: pi_include: not found
/sbin/mount_root: line 1: pi_include: not found
/sbin/mount_root: line 1: set_jffs_mp: not found
/sbin/mount_root: line 1: determine_root_device: not found
/sbin/mount_root: line 1: can't create /.extroot.md5sum: Read-only file system
switching to jffs2
root@(none):/# passwd
Changing password for root
New password:
Retype password:
Password for root changed by root
root@(none):/# cd /tmp
root@(none):/tmp# scp gerryk@192.168.1.2:~/tplink.bin /tmp</span>

<span style=font-family:Courier New,Courier,monospace;>Host '192.168.1.2' is not in the trusted hosts file.
(fingerprint md5 99:32:6a:72:db:26:03:a2:a5:42:ff:a6:9c:b8:6c:e8)
Do you want to continue connecting? (y/n) y</span>

<span style=font-family:Courier New,Courier,monospace;>Login for gerryk@192.168.1.2
Password:
You have logged in using cached account information. Some network services
will be unavailable.</span>

<span style=font-family:Courier New,Courier,monospace;>Press Enter to Continue.
tplink.bin 100% 7936KB 2.6MB/s 00:03
root@(none):/tmp# mtd -r write /tmp/tplink.bin firmware
Unlocking firmware ...</span>

<span style=font-family:Courier New,Courier,monospace;>Writing from /tmp/tplink.bin to firmware ... [w]</span>

<span style=font-family:Courier New,Courier,monospace;>Rebooting ...
Connection closed by foreign host.
gerryk@feynman:~$ telnet 192.168.1.1
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^]'.
=== IMPORTANT ============================
Use 'passwd' to set your login password
this will disable telnet and enable SSH
------------------------------------------</span>

<span style=font-family:Courier New,Courier,monospace;>BusyBox v1.23.2 (2016-01-02 18:01:44 CET) built-in shell (ash)</span>

<span style=font-family:Courier New,Courier,monospace;>_______ ________ __
| |.-----.-----.-----.| | | |.----.| |_
| - || _ | -__| || | | || _|| _|
|_______|| __|_____|__|__||________||__| |____|
|__| W I R E L E S S F R E E D O M
-----------------------------------------------------
CHAOS CALMER (15.05.1, r48532)
-----------------------------------------------------
* 1 1/2 oz Gin Shake with a glassful
* 1/4 oz Triple Sec of broken ice and pour
* 3/4 oz Lime Juice unstrained into a goblet.
* 1 1/2 oz Orange Juice
* 1 tsp. Grenadine Syrup
-----------------------------------------------------
root@OpenWrt:/#</span>

;

At this point, OpenWRT is installed. The web UI, LuCI, can be accessed by pointing a browser at;<a href=http://192.168.1.1/>http://192.168.1.1/</a>
The password will need to be set on first login, or the router will start-up in 'initialised' mode every time.

