---
title: "Asus N56VZ Shutdown Problem with HDD Caddy"
date: 2015-09-01T15:02:00+01:00
draft: false
---
I;have had an;<a href=https://www.asus.com/Notebooks/N56VZ/>ASUS N56VZ</a>;laptop for about 18 months, and rate it as one of the best laptops I have ever had. I was dual-booting Windows 8 and Ubuntu off the 750GB hard drive since I got the laptop until one day I basically destroyed the Ubuntu install while playing with Docker.io
I could have recovered it, but I took this as an opportunity to do an upgrade I had been thinking about for a while - adding an SSD and relegating the hard drive to a caddy which would take the place of the optical drive. I can't remember a time where I had actually used the optical drive, so using the space for a second hard drive seemed a no-brainer.
I ordered a;<a href=http://www.samsung.com/global/business/semiconductor/minisite/SSD/global/html/ssd850evo/overview.html>250GB Samsung EVO 850 SSD</a>;and a;<a href=http://www.amazon.co.uk/dp/B00E7MH15Y/ref=pe_385721_37038051_TE_dp_2>drive caddy</a>;to take the existing HDD. The actual change-over was almost trivial in its simplicity, and since this laptop is EFI enabled, there was little to no messing about with boot-order and such to get WIndows to boot from the secondary drive.
I also took this an an opportunity to install Arch Linux on the SSD. I had kind gotten bored with Ubuntu and the lack of control I felt with certain configurations, so thought this might be an appropriate remedy.
Everything seemed to be working excellently until some time in the recent past, the laptop stopped cleanly shutting down in Windows. It would go through the shutdown process, and at the time when the screen would normally blank, and the drive and fans spin down, it basically sat there... unresponsive, but still spinning away.
Around this time, my place in the Windows 10 upgrade queue came about, so I thought that the upgrade might fix whatever had broken and went ahead with the upgrade - a remarkably painless experience, incidentally. The upgrade did not fix the issue though...
So, I started investigating... update drivers, check, update BIOS, check... all to no avail, though. Then, I came across;<a href=http://forum.notebookreview.com/threads/hp-elitebook-8560p-wont-shutdown.655065/>this thread on NotebookReview</a>. The situation it described matched my own, and as I read through the thread, came across a mention of the procedure being successful with the ASUS N56ZV.;
The procedure described the removal or otherwise ungrounding of pin3, which is the SATA Diagnostic pin.;
So, screwdriver out... I removed the caddy, and started disassembling it. It wasn't a huge job, slightly complicated by some hidden screws, but once they were all opened, it came apart easily and revealed the internals.

<img src=https://gerryk.sdf.org/site_images/2015-09-01%2011.37.17.jpg />

<strong>The Caddy with HDD fitted</strong>

<img src=https://gerryk.sdf.org/site_images/2015-09-01%2011.43.04.jpg />

<strong>HDD Removed</strong>

<img src=https://gerryk.sdf.org/site_images/2015-09-01%2011.48.39.jpg />

<strong>Caddy with the lid off</strong>

It was when I got the lid off and could see the internals that I saw the little switch (to the left of the internal SATA connector). From what I could see it was on the offending pin too, so it seems that I could disable the pin without reverting to surgery. So, I flipped it.
Once I reassembled the caddy, I noticed that the switch was perfectly accessible without all the disassembly... oh well... I'll know better next time.

<img src=https://gerryk.sdf.org/site_images/2015-09-01%2011.57.46.jpg />

<strong>Switch visible with the lid on</strong>

One reboot and shutdown later, I verified that the switch did indeed fix the issue.

