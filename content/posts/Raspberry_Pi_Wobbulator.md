---
title: "Raspberry Pi Wobbulator"
date: 2014-12-02T13:23:00+01:00
draft: false
---
I came across am interesting project at the;<a href=http://ei7mre.org/>Mayo Radio Experimenter's Club</a>;<a href=http://ei7mre.org/?page_id=67>Rally;</a>earlier this year.;<a href=http://en.wikipedia.org/wiki/Wobbulator>A Wobbulator</a>. A small board that would piggy-back on a Raspberry Pi and utilise an Analog Devices AD9850 Direct Digital Synthesiser as an RF source. ;The purpose of a Wobbulator is to generate an RF sweep which can be routed through a device undet test, and captured, in this case, using an RF-voltmeter, but traditionally using an oscilloscope, to determine the characteristics of the device to be tested. It can be used to determine the response of filters and crystals and other RF circuits.
A Wobbulator would, in the past, have cost hundreds of euros, so to see;<a href=http://asliceofraspberrypi.blogspot.co.uk/2013/12/building-raspberry-pi-wobbulator-kit.html>the full kit</a>;available for a Rally special price of €40 was all the excuse I needed to get one. I already have a few Raspberry Pis and had a DDS on the way from eBay, so no further expenditure would be needed. The kit included a well manufactured board and all the various parts, including some header strips to connect to the GPIO array on the Pi and some high quality SMA ports for the RF in and outputs.;

The assembly started out with soldering some SMD devices... a few capacitors, diodes and resistors and two 1mm pitch DIL chips. I used a .5mm tip on my iron and .3mm silver bearing solder to mount these. I tinned the pads on the board first, then using a fine tweezers, held each device while I flowed to one side, and then other. The chips were a little more tricky, keeping all of the legs aligned while tacking one corner and then the other. The rest of the components are through-holeand a relatively trivial install. A set of headers are installed to take the DDS, and a double header on the other side to connect to the Pi.
<img alt= src=https://dl.dropboxusercontent.com/u/32770/2014-12-04%2021.10.21.jpg />

Once assembled, I started with a basic install of Rasbian on an SD card. A few tweaks need to be done to enable the functionality of the Wobbulator, and install the Wobbulator control software.

The default configuration for Rasbian is that i2c is disabled. We need to re-enable this first.Edit;<em>/etc/modprobe/raspi-blacklist.conf</em>;and comment out the line that blacklists i2c.

<span style=font-family: 'Courier New';>blacklist spi-bcm2708
<strong>#blacklist i2c-bcm2708</strong>
blacklist snd-soc-pcm512x
blacklist snd-soc-wm8804</span>

Then edit;<em>/etc/modules</em>;and add a line to load;<em>i2c-dev.</em>

<span style=font-family: 'Courier New';>snd-bcm2835
<strong>i2c-dev</strong></span>
;

Install i2c-tools, add the 'pi' user to the 'i2c' group and power-down the Pi.

<span style=font-family: 'Courier New';>$ sudo apt-get install i2c-tools
$ sudo adduser pi i2c
$ halt</span>

While the Pi is powered-off, attach the Wobbulator board to the GPIO array and power up the Pi.

When it restarts, check that the Wobbulator has been detected.

<span style=font-family: 'Courier New';>$ i2cdetect -y 0
; ; ;0 ;1 ;2 ;3 ;4 ;5 ;6 ;7 ;8 ;9 ;a ;b ;c ;d ;e ;f
00: ; ; ; ; ;-- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- 68 -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- --</span>

The '68' indicates that the Wobbulator has been successfully detected. Next,;install the required Python libraries.

<span style=font-family: 'Courier New';>$ sudo su;

# curl;<a href=https://bootstrap.pypa.io/ez_setup.py>https://bootstrap.pypa.io/ez_setup.py</a>;-o - | python3
# exit
$ git clone https://github.com/quick2wire/quick2wire-python-api.git
$;cd quick2wire-python-api/
$ sudo python3 setup.py install;
$ cd ~</span>

Finally, install the Wobbulator software.
<span style=font-family:Courier New,Courier,monospace;>$ git clone https://github.com/mi0iuo/RPi_Voltmeter.git
$ git clone https://github.com/mi0iuo/RPi_Wobbulator.git</span>

Once this is done, we need to test and calibrate the Wobbulator, as follows:

<span style=font-family: 'Courier New';>$ startx</span>

Once LXDE has started, open a Terminal window and enter the following:

<span style=font-family: 'Courier New';>$ cd RPi_Voltmeter-master
$ python3 rpi_voltmeter.py</span>

A small window will display.
<img alt= src=https://dl.dropboxusercontent.com/u/32770/RPiVM.png />

Leave Channel on channel 1, and click the Measure button. This will likely display a voltage up around 2v. This is around the maximum voltage the RF voltmeter can sample, so we need to reduce this greatly, since there is currently no input. On the board, there are two variable resistors (little blue boxes) with a little brass adjustment screw on each. Start to turn the one in the channel 1 section on the board anti-clockwise, clicking Measure periodically, until you get a voltage around 0.1v.

Do the same for Channel 2, except the target voltage is around 0.6v.

At this point, the Wobbulator is calibrated. You may exit the voltmeter and run the Wobbulator control software by entering the following in the Terminal:

<span style=font-family: 'Courier New';>$ cd ../RPi_Wobbulator-master
$ python3 rpi_wobbulator.py</span>

Once this was done, I ran a quick test of a filter I had built a year or so ago. The results, while not what I wanted, were excellent. The trace showed the filter to be out by about 1MHz, so there are a couple of toroids to be rewound. I will use the<a href=http://www.eham.net/reviews/detail/13>MFJ 259b</a>;with a 'custom' connector as an L/C meter to verify the toroids. I will document this process in another post.

<img alt= src=https://dl.dropboxusercontent.com/u/32770/wobbulator-1.png />

