---
title: "Arch Linux Upgrade Breaks EFI Dual-Boot"
date: 2014-12-18T13:35:00+01:00
draft: false 
---
I recently started using Arch as my primary distribution on my laptop. I made this change for a number of reasons... mainly that I did not like the direction that Ubuntu was going in, and I kind of missed the hands-on approach I had experienced with Slackware and Debian. ;I wanted to recapture the control that first drew me to Linux nearly 20 years ago.
Part of the transition was getting used to a rolling-upgrade methodology. I work in telecoms, where the idea of an upgrade that doesn't get put through multiple phases of end-to-end verification is completely unheard of, and all of my experiences with Linx have been release-based rather than rolling distros. It's a big mind-shift, and apparently can be fraught, if the various Arch forums are to be believed. So, it was with some trepidation that I finally did my first;sudo pacman -Syu

Not before first snapping the volumes. though. When I installed Arch, I decided to go with something other than;<em>EXT4</em>. The 'next-generation' filesystem/volume manager that most caught my attention was;<em>btrfs</em>, so I ran with that. When installing, I created subvolumes for<em>;/, /var, /home, /usr;</em>and;<em>/opt</em>. Snapping these was very straightforward, and unlike other volume managers I am used to, allow concurrent access to the snapped filesystem and the live filesystem without any additional mounting or anything. Nice.

So, I kicked off the upgrade, which took maybe 40 minutes including downloads. The system rebooted, and initally, all seemed well... I got my;<em>lightdm;</em>greeter, and once I entered my credentials, got my;<em>i3;</em>desktop. All fine... until I tried to move the mouse. Nothing. So, after some investigation, it seems that Elantech touchpads are quirky, and some functionality that had worked in kernel 3.15, was broken in 3.17, and would be fixed in 3.18. So, between the options of (a) building 3.18 from;<em>AUR</em>, porting the patch that had worked in 3.15 or pushing forward with learning to live with keyboard only, I decided to go with the latter. I will detail the whats, whys and hows of that in another blog-post.

That seemed to be the only issue, however. I thought I would boot into Windows 8.1 to update that too, as I do this so rarely that when I do, it takes forever, and involves huge downloads and multiple reboots. It was then that I noticed that my grub menu did not include Windows... or the Ubuntu that was on another partition... in fact nothing except Arch.

So, I did some digging, and found that the 'new' grub did things a little differently from what I was used to. No more was<em>menu.lst</em>;configured by hand, but instead sections in;<em>/etc/grub.d</em>;created the boot menu. Different, but definitely better. So, based on memory (and a little bit of Googling), I recreated the line that would point at the Windows EFI bootloader... rebooted and selected Windows, and got the following error:

symbol grub_term_highlight_color not found

So I did a bit more Googling, found one or two posts involving Ubuntu upgrading to 14.04, read a bit and thought maybe the grub upgrade had failed to write some file properly. So I had a look in the pacman logs, to find that grub had not been upgraded at all as part of that run. I next mounted the Windows EFI partition, and noticed a bunch of different EFI files, including one for;<em>memtest</em>, so I created a boot option for that, booted and sure enough, got;<em>Memtest</em>. So, back to the EFI partition, where I noticed that the Windows bootloader was much smaller than the other various;<em>.efi</em>;files, and had a modification date of the day I did the upgrade. So, for some unknown reason, the bootloader was modified, and possibly broken. There was also what seemed to be a backup bootloader (prefixed with bk) which was much bigger, so I renamed the broken one and copied the backup in its place...;

One reboot later, I never thought I would be so glad to see a Windows boot screen.
Now to download Elite: Dangerous, and relive some of my childhood in HD.

