---
title: "Configuring DNSCrypt on OpenWRT"
date: 2017-08-10T14:16:00+01:00
draft: true
---
\n$ ssh root@192.168.1.1
\nroot@192.168.1.1's password: 
\n
\nBusyBox v1.23.2 (2016-01-02 18:01:44 CET) built-in shell (ash)
\n
\n  _______                     ________        __
\n |       |.-----.-----.-----.|  |  |  |.----.|  |_
\n |   -   ||  _  |  -__|     ||  |  |  ||   _||   _|
\n |_______||   __|_____|__|__||________||__|  |____|
\n          |__| W I R E L E S S   F R E E D O M
\n -----------------------------------------------------
\n CHAOS CALMER (15.05.1, r48532)
\n -----------------------------------------------------
\n  * 1 1/2 oz Gin            Shake with a glassful
\n  * 1/4 oz Triple Sec       of broken ice and pour
\n  * 3/4 oz Lime Juice       unstrained into a goblet.
\n  * 1 1/2 oz Orange Juice
\n  * 1 tsp. Grenadine Syrup
\n -----------------------------------------------------
\nroot@main-rt:~# vim /etc/config/dnscrypt-proxy 
\nroot@main-rt:~# /etc/init.d/dnscrypt-proxy enable
\nroot@main-rt:~# /etc/init.d/dnscrypt-proxy start
\nroot@main-rt:~# vim /etc/config/dhcp 
\nroot@main-rt:~# /etc/init.d/dnsmasq restart
\nroot@main-rt:~# logread | grep -n using nameserver
\n45:Tue Aug  8 11:11:45 2017 daemon.info dnsmasq[6006]: using nameserver 8.8.8.8#53
\n46:Tue Aug  8 11:11:45 2017 daemon.info dnsmasq[6006]: using nameserver 159.134.0.1#53
\n47:Tue Aug  8 11:11:45 2017 daemon.info dnsmasq[6006]: using nameserver 159.134.0.2#53
\n159:Tue Aug  8 12:04:32 2017 daemon.info dnsmasq[19353]: using nameserver 208.67.222.222#53 for domain pool.ntp.org
\n160:Tue Aug  8 12:04:32 2017 daemon.info dnsmasq[19353]: using nameserver 127.0.0.1#5353
\nroot@main-rt:~# logread | grep Proxying from
\nTue Aug  8 11:19:05 2017 daemon.notice dnscrypt-proxy[15984]: Proxying from 127.0.0.1:5353 to 208.67.220.220:443
\nroot@main-rt:~# 
\n</pre>
\n
