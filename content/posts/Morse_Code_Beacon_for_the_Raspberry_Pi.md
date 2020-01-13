---
title: "Morse Code Beacon for the Raspberry Pi"
date: 2016-08-10T22:38:00+01:00
draft: false
---
Among other great features of the Raspberry Pi is the General Purpose Input Output array (GPIO). This is an array of pins that can be programmed to behave as pretty much any I/O type that can be represented digitally. The pins can be switched on or off to represent binary 1s and 0s and controlled so as to emulate any communication protocol that uses bits (I2C, SPI, RS232 etc. etc.). However, as a first attempt at working with GPIO, I took a recommendation from Steve EI5DD and wrote a program that will key a transceiver and generate morse code.

The program is written in Python, and runs from the command line. To install, first ensure that the RPi.GPIO Python module is installed on your Pi. This module enables programmatic access to the GPIO through Python, and makes it very simple. To install, enter the following at the command line:

<span style=font-family:Courier New,Courier,monospace;>$ sudo pip install RPi.GPIO</span>

Once this completes, the next stage is to download the cwbeacon code. To do this, enter the following at the commandline:

<span style=font-family:Courier New,Courier,monospace;>$ git clone;<a href=https://github.com/gerryk/cwbeacon.git title=https://github.com/gerryk/cwbeacon.git>https://github.com/gerryk/cwbeacon.git</a></span>

Assuming you were in your home directory, this will create a directory called 'cwbeacon' containing a Python file called 'beacon.py'. You can execute this by typing the following at the commandline:

<span style=font-family:Courier New,Courier,monospace;>$ python cwbeacon/beacon.py</span>

You will get a short message describing how to use the program, since you did not provide any parameters. The message is like this:

<span style=font-family:Courier New,Courier,monospace;><em>usage: CW Beacon Sender - uses GPIO pin [-h] [-c CPS] message [message ...]
CW Beacon Sender - uses GPIO pin: error: too few arguments</em></span>

Before you can key a rig with this program, you need to build a small keying circuit. Basically this uses a transistor as a switch. I used a BC548, but any general purpose NPN, such as 2N3904 may be used. I also added a small indicator LED, since when not plugged into a rig, the keying is silent.


This is the circuit...


<img src=https://www.dropbox.com/s/0eb8x5ddcsrasng/2016-08-09%2015.04.42.jpg?raw=1 />


Most rigs use a stereo jack as the key input with the tip and shield as key and ground. The pins on the Raspberry Pi are GPIO 11 and GND. The pinout for the Pi 2 is as follows (yours may differ depending on version):


<img src=https://www.dropbox.com/s/c6df49vxsv158ng/gpio-numbers-pi2.png?raw=1 />


Once the keying cirsuit is build and connected, the rig should be set to CW mode, but VOX (or however your rig actually transmits on keyng) disabled to test. The following command line will test the keyer:

<span style=font-family:Courier New,Courier,monospace;>$ python cwbeacon/beacon.py test</span>

You should see the LED flash and the side-tone generator in the transceiver should sound the morse for 'test'. The speed of transmission can be changed from the default 15 CPS by using the -c parameter as follows:

<span style=font-family:Courier New,Courier,monospace;>$ python cwbeacon/beacon.py -c 20 test</span>

Once this test has been successful - you may need to debug your keyer circuit! - you can activate CW transmit on the transceiver and test a transmission. It makes sense to transmit on a clear frequency, and using a power and frequency that is appropriate for a beacon.


Once this has been completed, you may wish to automate the beacon transmission. The Linux crontab feature may be used for this. To activate automated transmission, enter the following at the commandline:

<span style=font-family:Courier New,Courier,monospace;>$ crontab -e</span>

You will be presented with an editor screen where you can add the crontab configuration. An example configuration would be:

<span style=font-family:Courier New,Courier,monospace;>5,10,15,20,25,30,35,40,45,50,55,0 * * * * python /home/pi/cwbeacon/beacon.py -c 20 ei8drb io53mf</span>

This will beacon my callsign and grid square every 5 minutes of every day. You should customise this to your own environment and requirements.


Happy beaconing...

