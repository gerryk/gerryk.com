---
title: "Authentication Bypass on Zyxel D1000 (Eircom) Router"
date: 2014-12-16T13:32:00+01:00
draft: false 
---
<img alt= src=https://dl.dropboxusercontent.com/u/32770/eircom-zyxel.JPG />

<strong>The Eircom D1000 Zyxel Router</strong>

Eircom, an ISP in Ireland, supplies a branded version of the Zyxel D1000 router with their DSL broadband offerings. The web interface is protected, as one might expect, by a login&amp;password challenge. All good, one might think. However, if you look at the source of the login page, located at;<em>/cgi-bin/login.html</em>;you might find an interesting surprise.


;function DefaultPasswdNote_check()
{
; ; ; ; var random_passwd = 01282e7c08b4;
; ; ; ; var current_passwd = xxxxxxxxx;
// ; ; ;alert(current_passwd +  +random_passwd);
; ; ; ; if(current_passwd != random_passwd ){
; ; ; ; ; ; ; ; ; ; $(#defaultPassNote).hide();
; ; ; ; ;}
}

The admin password can be seen in this function, as;current_passwd. I have obviously replaced mine with x's (it was hunter2). I have verified this vulnerability on a number of D1000 routers.
If the web GUI is exposed to the outside world... well, bad things will happen.

The only mitigations are -;
;;;;1. Ensure the web GUI is not exposed to the outside world (WAN), LAN and WIFI only.

;;;;2. Ensure you have a strong WPA2 key.

