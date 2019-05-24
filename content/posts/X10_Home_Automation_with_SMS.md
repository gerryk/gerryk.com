---
title: "X10 Home Automation with SMS"
date: 2010-02-10T10:57:00+01:00
draft: true
---

I am currently building a house, and as such, have a great platform for implementing all the things I have dreamt of but could never manage to achieve in a rented house. Apart from finally having the spaghetti finally embedded in the walls and floors, and having almost enough power and network sockets (you can never actually have enough, right?) I can experiment with centralising control of the house and accessing home telemetry through my phone.

So... walk before you can run, right? I was discussing all of this with my builder who mentioned that he'd always wanted to be able to SMS his heating system to get it to turn on an hour before he gets home or whatever, and asked if I would be able to do it for him. Great! A testbed for the grand plan!

Being a Linux admin, I generally eschew embedded solutions for linux hosted ones, and in this case, hosted on suitably small hardware... the;<a href=http://us.acer.com/acer/product.do;jsessionid=E392CB47BB44B92F719E9797D0A980A7.public_a_us003?LanguageISOCtxParam=en&amp;rcond5e.c2att92=449&amp;inu49e.current.c2att92=449&amp;link=ln314e&amp;CountryISOCtxParam=US&amp;kcond47e.c2att92=449&amp;rcond159e.att21k=1&amp;kcond48e.c2att101=61912&amp;rcond190e.att21k=1&amp;acond23=US&amp;rcond4e.att21k=1&amp;sp=page17e&amp;rcond157e.c2att92=449&amp;var9e=793&amp;ctx1g.c2att92=449&amp;rcond42e.att21k=1&amp;kcond50e.c2att92=449&amp;rcond45e.att21k=1&amp;rcond158e.c2att1=25&amp;ctx2.c2att1=25&amp;inu53e.current.c2att92=449&amp;rcond38e.c2att1=25&amp;var13e=US&amp;rcond44e.c2att1=25&amp;rcond186e.c2att92=449&amp;rcond3e.c2att1=25&amp;rcond28e.attN2B2F2EEF=3264&amp;rcond189e.c2att1=25&amp;ctx1.att21k=1&amp;CRC=2678317110>Acer Veriton</a>. This little box is basically an Acer Aspire One with no keyboard or screen. Powered by an 1.6GHz Atom and containing 1GB of RAM and 160GB HDD, it's a decent little box for many purposes, including general computing, and drawing only 20W of power is perfect for an always-on system.

The system was planned as a couple of scripts polling the GSM dongle via the gnokii toolset and parsing out commands which would be passed to the heyu commandline tool which drives the;<a href=http://www.uk-automation.co.uk/x10-computer-interface-usb-serial-version-p-997.html>Marmitek CM11</a>;X10 controller.

Older styles of GSM dongle appear to Linux as a couple of USB ttys, which will accept AT commands and the like. The gnokii toolset simplifies this and allows SMS to be sent and received from the commandline. gnokii is available as a Debian package, so that made things as painless as it is possible for software installation to be; sudo apt-get gnokii-cli and 30 seconds later it's done. I then edited /etc/gnokiirc and saved it as .gnokiirc in my home directory.

The CM11 has a USB connector which also shows up as a USB tty. The heyu toolset needs to be downloaded and compiled, but it's a painless experience.

I built the;<a href=http://wiki.debian.org/DebianEeePC>eeePC version of Debian 5;</a>on the Veriton booting from the SD, which had the netinstall image dd'd onto it. I then installed the usual suspects; vi, sudo and build-essential, followed by gnokii and heyu (which had to be compiled).

The CM11 controls 4 X10 relays, which are ganged with the original relays to allow;

The scripts that run this whole thing were developed specifically for this site, but could easily be modified to handle different situations and functionalities. They are very much alpha version and there is absolutely no warranty, either explicit or implicit. That being said, I have made it available under the GPL, so it is open to copying, modification and everything else the GPL permits. It can be downloaded from;<a href=https://sourceforge.net/projects/x10-sms/>Sourceforge</a>.

