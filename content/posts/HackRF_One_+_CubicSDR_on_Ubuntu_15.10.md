---
title: "HackRF One + CubicSDR on Ubuntu 15.10"
date: 2016-03-30T15:17:00+01:00
draft: false
---
I have been playing with Software Defined Radio for a number of years, but recently advances in high-speed sampling has put relatively high quality, extremely high frequency SDR within reach of everyone. A few years ago Eric Fry reverse-engineered the communications from a Digital TV USB Dongle to see that it transmitted raw samples. A;<a href=http://comments.gmane.org/gmane.linux.drivers.video-input-infrastructure/30346>number of</a>;<a href=http://comments.gmane.org/gmane.linux.drivers.video-input-infrastructure/40927>email threads</a>;followed up this research, and eventually;<a href=http://sdr.osmocom.org/trac/wiki/rtl-sdr>Osmocom</a>;developed the first RealTek-SDR (rtlsdr) driver that began the low-cost SDR revolution.
Last year, I heard of a very interesting Kickstarter by renowned hardware hacker;<a href=http://www.ossmann.com/mike/>Michael Ossman</a>;(Im-Me hacking fame). For a remarkably low price ($300) he was developing an SDR capable of both receive and transmit (albeit about 15dBm) from 10MHz to 6GHz. Once the Kickstarter completed, Michael Ossman productified it as the<a href=https://greatscottgadgets.com/hackrf/>;HackRF One</a>. I had to have one.

Before getting into the hacking aspect, I wanted to get the basic receive-only SDR functionality working. My current favourite Linux SDR demodulator is;<a href=http://cubicsdr.com/>CubicSDR</a>. It demodulates FM, AM, SSB and CW and can also output an IQ stream of selectable bandwidth. I currently have Ubuntu 15.10 as my radio experimentation OS.

1. Install dependencies...

<span style=font-family:Courier New,Courier,monospace;>sudo apt-get install hackrf gnuradio gnuradio-dev gr-iqbalsudo apt-get install git build-essential librtlsdr-dev automake libfftw3-dev cmake libgl1-mesa-dev libwxgtk3.0-dev libpulse-dev

sudo apt-get install libfftw3-dev libpulse-dev libgtk-3-dev

sudo apt-get install freeglut3 freeglut3-dev</span>

2. Clone and install liquid-dsp

<span style=font-family:Courier New,Courier,monospace;>git clone https://github.com/jgaeddert/liquid-dsp
cd liquid-dsp/

./bootstrap.sh;

./configure;
make
sudo make install
sudo ldconfig
cd ..</span>

3. Clone and install SoapySDR

<span style=font-family:Courier New,Courier,monospace;>git clone https://github.com/pothosware/SoapySDR.git
cd SoapySDR/</span>

<span style=font-family:Courier New,Courier,monospace;>mkdir build
cd build/
cmake ../ -DCMAKE_BUILD_TYPE=Release
make
sudo make install
sudo ldconfig
cd ..</span>

4. Clone and install SoapyHackRF;

<span style=font-family:Courier New,Courier,monospace;>git clone;<a href=https://github.com/pothosware/SoapyHackRF.git>https://github.com/pothosware/SoapyHackRF.git</a>

cd SoapyHackRF/
mkdir build;

cd build/
cmake ../
make
sudo make install

sudo ldconfig</span>

<span style=font-family:Courier New,Courier,monospace;>cd ..</span>

5. Download and build wxWidgets

<span style=font-family:Courier New,Courier,monospace;>wget;<a href=https://github.com/wxWidgets/wxWidgets/releases/download/v3.1.0/wxWidgets-3.1.0.tar.bz2>https://github.com/wxWidgets/wxWidgets/releases/download/v3.1.0/wxWidget...</a></span>

<span style=font-family:Courier New,Courier,monospace;>tar -xjvf wxWidgets-3.1.0.tar.bz2;
cd wxWidgets-3.1.0/
mkdir ~/Development/wxwidgets-staticlib
./autogen.sh;
./configure --with-opengl --disable-shared --enable-monolithic --with-libjpeg --with-libtiff --with-libpng --with-zlib --disable-sdltest --enable-unicode --enable-display --enable-propgrid --disable-webkit --disable-webview --disable-webviewwebkit --prefix=`echo ~/Development/wxwidgets-staticlib` CXXFLAGS=-std=c++0x --with-libiconv=/usr

make &amp;&amp; make install
cd ..</span>

5. Finally clone and install CubicSDR

<span style=font-family:Courier New,Courier,monospace;>git clone;<a href=https://github.com/cjcliffe/CubicSDR.git>https://github.com/cjcliffe/CubicSDR.git</a></span>

<span style=font-family:Courier New,Courier,monospace;>cd;CubicSDR
mkdir build

cd build/
cmake ../ -DCMAKE_BUILD_TYPE=Release -DwxWidgets_CONFIG_EXECUTABLE=~/Development/wxwidgets-staticlib/bin/wx-config

make
sudo make install</span>

