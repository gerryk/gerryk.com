---
title: "SSTV on Raspberry Pi"
date: 2016-06-16T16:19:00+01:00
draft: false
---
Following a suggestion by Galway VHF Group mamber Steve, EI5DD, I thought I would give SSTV a shot. It's not a mode I have any experience with, apart from hearing the transmissions at 14.230MHz when I tune around. Steve mentioned a cross-platform SSTV program QSSTV, which seems to run well on a Pi 2, so that's what I decided to use.
I have a Pi 2 that I use for playing with SDR and radio software already set up with the current Rasbian (wheezy). Initially, I installed the version of QSSTV in the Rasbian repositories, however, I got errors when it tried to open the audio device on the Pi. I uninstalled it and decided to build from source instead. The code and build instructions are available on;<a href=http://users.telenet.be/on4qz/>the author's site</a>.
I started by installing the dependencies.
sudo apt-get install g++ libfftw3-dev qt5-default libpulse-dev
sudo apt-get install hamlib-dev libasound-dev libv4l-dev
sudo apt-get install libopenjp2-7 libopenjp2-7-dev
I then downloaded and exploded the source tarball and compiled and installed the binary. Compilation on the Pi takes a while, so be patient.
$ cd ~/Development
$ tar -xvzf qsstv_9.1.1.tar.gz
$ cd qsstv_9.1.1
$ qmake
$ make
$ sudo make install
Running the application is just a matter of entering 'qsstv' at the command prompt.
$ qsstv
Once started, it needs to be configured.
