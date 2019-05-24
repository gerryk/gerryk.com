---
title: "Parental Control using OpenWRT"
date: 2017-02-07T22:47:00+01:00
draft: false
---

As a parent, I am somewhat torn regarding 'parental control' of Internet Access where my daughter is concerned. She is 8, so has limited access anyhow, but I would like for that access to be as unrestricted as possible while at the same time avoiding her stumbling any age-inappropriate content, which as we all know can often be only 2 or 3 clicks away.

I have decided on a multipronged approach, with the main home router, a TP Link N600 running OpenWRT Chaos Calmer being the crux of this.

<h3>Time Based Access</h3>

I am using a LuCI application called Access-Control which allows time-based rules block any accesses from any MAC address. It also has the facility to grant 'tickets' for usage within the usually restricted times. Basically, it is a LuCI UI to create;<em>iptables</em>;rules, which look like this:

<span style=font-family:Courier New,Courier,monospace;>zone_wan_dest_REJECT ;all ;-- ;anywhere ; ; ; ; ; ; anywhere ; ; ; ; ; ; MAC 00:04:4B:aa:bb:cc TIME from 00:01:00 to 08:30:00 /* Emily's Tablet Morning */
zone_wan_dest_REJECT ;all ;-- ;anywhere ; ; ; ; ; ; anywhere ; ; ; ; ; ; MAC 00:04:4B:aa:bb:cc TIME from 19:00:00 to 23:59:00 /* Emily's Tablet Evening */</span>

;

<h3>DNS Filtering</h3>

I use two types of DNS filtering... one is the LuCI App - Adblock. This leverages a number of blacklists which are used with dnsmasq to block requests for known ad and other unwanted content. This has the added benefits of blocking malware, ransomware, phishing sites and a bunch of other stuff you really don't want to be clicking on. I have this configured network-wide as I want to block this for everyone, not just the kids.

The second is OpenDNS <em>Family Shield</em>. This is basically a pair of DNS resolvers which are tailored to child-friendly content. Setting this up to only affect the kids while allowing the adults free access involves tweaking dnsmasq to add a 'tag' which will get the OpenDNS resolvers, while untagged clients will get the standard DNS resolvers. Once the tag has been set up, the clients you wish to tag need to be given a static DHCP lease, and then the configuration edited to add the tag.

The configuration on my router looks like this <em>(/etc/config/dhcp)</em>

<span style=font-family:Courier New,Courier,monospace;>config tag 'kids'
; ; ; ; list dhcp_option '6,208.67.222.123,208.67.220.123'</span>

<span style=font-family:Courier New,Courier,monospace;>config host
; ; ; ; option name 'emily-tablet'
; ; ; ; option mac '00:04:4b:aa:bb:cc'
; ; ; ; option ip '192.168.1.201'
; ; ; ; option 'tag' kids</span>
;

<h3>Links:</h3>

<a href=https://openwrt.org/>https://openwrt.org/</a>

<a href=https://github.com/k-szuster/luci-access-control-package>https://github.com/k-szuster/luci-access-control-package</a>

<a href=https://github.com/openwrt/packages/tree/master/net/adblock/files>https://github.com/openwrt/packages/tree/master/net/adblock/files</a>

<a href=https://www.opendns.com/home-internet-security/>https://www.opendns.com/home-internet-security/</a>
