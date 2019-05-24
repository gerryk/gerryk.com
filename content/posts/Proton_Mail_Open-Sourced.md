---
title: "Proton Mail Open-Sourced"
date: 2015-08-25T15:00:00+01:00
draft: false
---

<a href=https://protonmail.ch/>Proton Mail</a>;is a free, web-based encrypted mail service founded by CERN in 2013. It uses client-side encryption, and could be termed a trust no-one mail service, since the data stored on the servers is encrypted, and the user never loses control of the encryption key.

Obviously, since the client-side is served rather than being resident on the client computer, this has raised some questions as to the overall trustworthiness of the service, but Proton Mail have addressed this by Open Sourcing the code - under the very permissive MIT license.

The code itself runs on Node.js, and leverages such modern web frameworks as Angular.js. It can be acquired from<a href=https://github.com/ProtonMail/WebClient>https://github.com/ProtonMail/WebClient</a>;as can the very scant install instructions. These instructions, however, don't address any set-up or install of dependencies, so here is a more complete instruction for Ubuntu 14.04 LTS, Trusty Tahr.

<span style=font-family:Courier New,Courier,monospace;>$ cd /var/www </span>

<span style=font-family:Courier New,Courier,monospace;>$ git clone <a href=https://github.com/ProtonMail/WebClient.git>https://github.com/ProtonMail/WebClient.git</a> protonmail </span>

<span style=font-family:Courier New,Courier,monospace;>$ cd protonmail </span>

<span style=font-family:Courier New,Courier,monospace;>$ sudo apt-get update </span>

<span style=font-family:Courier New,Courier,monospace;>$ sudo apt-get install nodejs </span>

<span style=font-family:Courier New,Courier,monospace;>$ sudo apt-get install npm </span>

<span style=font-family:Courier New,Courier,monospace;>$ sudo ln -s /usr/bin/nodejs /usr/bin/node </span>

<span style=font-family:Courier New,Courier,monospace;>$ sudo npm install -g grunt</span>

<span style=font-family:Courier New,Courier,monospace;>$ sudo npm install -g grunt-cli </span>

<span style=font-family:Courier New,Courier,monospace;>$ sudo npm install -g bower </span>

<span style=font-family:Courier New,Courier,monospace;>$ sudo npm install </span>

<span style=font-family:Courier New,Courier,monospace;>$ sudo bower install --allow-root </span>

<span style=font-family:Courier New,Courier,monospace;>$ sudo grunt --prod</span>

The service will be be available on port 8080.

All I have done so far is verify that the site loads. I need to look closer at the code to determine what persistence is used, how to register new users, how to actually hook into an SMTP back-end and so forth.

