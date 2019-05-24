---
title: "Bitcoin full-node on Raspberry Pi with NFS storage"
date: 2017-10-23T11:55:00+01:00
draft: false
---
I recently augmented my home-server with a bunch of additional storage. Since I have all this space, and a few Raspberry Pis lying around gathering dust, I though I might try running a Bitcoin Full Node at home. This has a couple of positive effects... it strengthens the overall bitcoin network, and it gives me a trusted verification for any inbound transactions.

I first created an NFS share on my home server... I allocated a 250GB LVM volume with an EXT4 filesystem to it, added it to /etc/exports and restarted nfs service. It was necessary to ensure that the user that owned the NFS share on the server had the same UID as the owner on the Pi. In this case, 101 for both.

I then installed the minimal Rasbian image onto a surplus 8GB MicroSD card and booted it up. I then followed these steps to install and build the bitcoin client...

<strong>1. Install prerequisites</strong>

<span style=font-family:Courier New,Courier,monospace;>sudo apt install build-essential autoconf libssl-dev libboost-dev libboost-chrono-dev libboost-filesystem-dev libboost-program-options-dev libboost-system-dev libboost-test-dev libboost-thread-dev libtool;libevent-dev</span>

<strong>2. Get bitcoin source (I got v0.15 which was the most recent 'stable', I would recommend getting whatever the most recent numbered release is)</strong>

<span style=font-family:Courier New,Courier,monospace;>git clone -b 0.15 https://github.com/bitcoin/bitcoin.git</span>

<strong>3. Build - the 'make' will take some time</strong>

<span style=font-family:Courier New,Courier,monospace;>cd bitcoin/
./autogen.sh;
./configure CPPFLAGS=-I/usr/local/BerkeleyDB.4.8/include -O2 LDFLAGS=-L/usr/local/BerkeleyDB.4.8/lib --disable-wallet
make
sudo make install</span>

<strong>4. Enable ssh (this is specific to newer Rasbian releases)</strong>

<span style=font-family:Courier New,Courier,monospace;>sudo touch /boot/ssh</span>

<strong>5. Add NFS share to fstab - in my case, my server is called 'erdos' and the share is located at /exports/blockchain... yours will;differ</strong>

<span style=font-family:Courier New,Courier,monospace;>$ sudo vi /etc/fstab</span>

Paste the following - yours may vary

<span style=font-family: &quot;Courier New&quot;, Courier, monospace;>erdos:/exports/blockchain  /home/pi/.bitcoin  nfs  defaults 0 0</span>

Mount the filesystem...

<span style=font-family:Courier New,Courier,monospace;>$ sudo mount -a</span>

<strong>6. Create systemd service file</strong>

<span style=font-family:Courier New,Courier,monospace;>$ sudo vi /etc/systemd/system/bitcoind.service</span>

Paste the following - again, yours may vary

<span style=font-family:Courier New,Courier,monospace;>[Unit]
Description=Bitcoin daemon serivce
After=network.target</span>

<span style=font-family:Courier New,Courier,monospace;>[Service]
Type=simple
User=pi
ExecStart=/usr/local/bin/bitcoind</span>

<span style=font-family:Courier New,Courier,monospace;>[Install]
WantedBy=multi-user.target</span>

<strong>7. Start and enable bitcoind service</strong>

<span style=font-family:Courier New,Courier,monospace;>pi@bitcoin:~/bitcoin $ sudo systemctl start bitcoind
pi@bitcoin:~/bitcoin $ sudo systemctl status bitcoind
● bitcoind.service - Bitcoin daemon serivce
  Loaded: loaded (/etc/systemd/system/bitcoind.service; disabled; vendor preset: enabled)
  Active: active (running) since Mon 2017-10-23 12:07:50 IST; 5s ago
  Main PID: 8717 (bitcoind)
       CGroup: /system.slice/bitcoind.service
         └─8717 /usr/local/bin/bitcoind</span>

<span style=font-family:Courier New,Courier,monospace;>Oct 23 12:07:50 bitcoin systemd[1]: Started Bitcoin daemon serivce.
pi@bitcoin:~/bitcoin $ sudo systemctl enable bitcoind
Created symlink /etc/systemd/system/multi-user.target.wants/bitcoind.service → /etc/systemd/system/bitcoind.service.</span>

<strong>8. Confirm listening status</strong>

<span style=font-family:Courier New,Courier,monospace;>pi@bitcoin:~ $ ss -ltp
State Recv-Q Send-Q Local Address:Port Peer Address:Port
LISTEN 0 128 127.0.0.1:8332 *:* users:((bitcoind,pid=8717,fd=10))
LISTEN 0 128 *:8333 *:* users:((bitcoind,pid=8717,fd=127))
LISTEN 0 64 *:33171 *:*
LISTEN 0 128 *:ssh *:*
LISTEN 0 64 :::39493 :::*
LISTEN 0 128 ::1:8332 :::* users:((bitcoind,pid=8717,fd=9))
LISTEN 0 128 :::8333 :::* users:((bitcoind,pid=8717,fd=126))
LISTEN 0 128 :::ssh :::*</span>


<strong>9. Forward port 8333 to your bitcoin node</strong>

This will be specific to your router. It is recommended that you either configure a static IP on your Pi, or configure static DHCP on your router, so the Pi will always have the same IP.


<strong><span style=font-family:Arial,Helvetica,sans-serif;>Notes on downloading the blockchain:</span></strong>

<font face=Arial, Helvetica, sans-serif>The limited RAM in the Raspberry Pi can cause issues when downloading the entire blockchain... it may hang or otherwise misbehave. To avoid this, I temporarily installed bitcoin core on my main server to do the download, but since discovered that it is available via Bittorrent from;https://getbitcoinblockchain.com/</font>

<font face=Arial, Helvetica, sans-serif>Once downloaded, move the downloaded files to wherever your NFS share is and it will appear in the .bitcoin home directory.</font>


