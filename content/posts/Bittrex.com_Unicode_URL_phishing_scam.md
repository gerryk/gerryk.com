---
title: "Bittrex.com Unicode URL phishing scam"
date: 2017-10-10T15:30:00+01:00
draft: false 
---
68,I occasionally use Bittrex to trade cryptos and were it not for my password manager, I would probably have fallen victim to a pretty subtle phishing scam.. The scam relies on the fact that in the huge unicode character set, there are many glyphs that look very like standard the roman characters we are used to as far as URLs are concerned. Many browsers do not make any visual distinction either, so if a letter looks like an 'A' for example, only some digging will reveal that it is in fact another character entirely.

Compare this, the legitimate URL...

<img alt=legit url data-entity-type=file data-entity-uuid=3590823d-32ac-4b62-900a-6333c0a6ef3c src=/sites/default/files/inline-images/2017-10-10%20%285%29.png />

With this, the fake...

<img alt=fake url data-entity-type=file data-entity-uuid=be3d7884-047b-4a81-81ed-3af215aabdad src=/sites/default/files/inline-images/2017-10-10%20%284%29.png />

All looks OK at a glance, right? Even has a green 'site secure' SSL notification. However, notice what looks like a;little comma under the 'r'? This is an entirely different character, which means that we are not at bittrex.com, we are at a phishing site. A pretty clever one too, as it turns out.

I didn't actually notice this at first. I use a password manager, Lastpass, which has a browser plugin that fills in credentials on recognised sites. In this instance, though, it failed to fill anything, which got me thinking.

I opened the 'site information' window and saw the following cookie...

<img alt=cookie data-entity-type=file data-entity-uuid=bb761768-e7a8-46cc-a05f-f7b7f6cbe488 src=/sites/default/files/inline-images/2017-10-10%20%287%29.png />

I then remembered <a href=https://www.theguardian.com/technology/2017/apr/19/phishing-url-trick-hackers>reading about Unicode URL hacks</a>, and looked closer at;the;URL only to notice the little comma. xn--bittex-eib.com is rendered as;bittŗex.com by the browser.

It seems that Google is returning an ad for this URL in its results for 'bittrex'.

<img alt=google results data-entity-type=file data-entity-uuid=d82bc09f-3a35-4031-a4ce-24876f2298fa src=/sites/default/files/inline-images/2017-10-10%20%2810%29.png />

Thankfully this is as far as the scam got with me, but others may be less lucky.

Password managers and 2FA are a good line of defense against this sort of attack.

A Unicode encoder can be seen here:;https://www.punycoder.com/

The registrar, namecheap.com and bittrex.com have both been notified since namecheap are identified in the whois record.


<pre>
Domain name: XN--BITTEX-EIB.COM
Registry Domain ID: 2172486546_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.namecheap.com
Registrar URL: http://www.namecheap.com
Updated Date: 2017-10-09T19:56:44.00Z
Creation Date: 2017-10-09T19:17:53.00Z
Registrar Registration Expiration Date: 2018-10-09T19:17:53.00Z
Registrar: NAMECHEAP INC
Registrar IANA ID: 1068
Registrar Abuse Contact Email: <a href=http://reversewhois.domaintools.com/?email=44c91f4f81df8526bd460ad6db4a95fe title=Search for this email address><img align=middle border=0 src=http://source.domaintools.com/email.pgif?md5=44c91f4f81df8526bd460ad6db4a95fe&amp;face=arial&amp;size=9&amp;color=000000&amp;bgcolor=FFFFFF&amp;face=arial&amp;size=9&amp;color=0000FF&amp;bgcolor=FFFFFF&amp;format[]=transparent&amp;format[]=transparent /></a>
Registrar Abuse Contact Phone: +1.6613102107
Reseller: NAMECHEAP INC
Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
Domain Status: addPeriod https://icann.org/epp#addPeriod
Registry Registrant ID: 
Registrant Name: WhoisGuard Protected
Registrant Organization: WhoisGuard, Inc.
Registrant Street: P.O. Box 0823-03411 
Registrant City: Panama
Registrant State/Province: Panama
Registrant Postal Code: 
Registrant Country: PA
Registrant Phone: +507.8365503
Registrant Phone Ext: 
Registrant Fax: +51.17057182
Registrant Fax Ext: 
Registrant Email: 3fd40fbd82894113a145535926a6c47f.protect@whoisguard.com
Registry Admin ID: 
Admin Name: WhoisGuard Protected
Admin Organization: WhoisGuard, Inc.
Admin Street: P.O. Box 0823-03411 
Admin City: Panama
Admin State/Province: Panama
Admin Postal Code: 
Admin Country: PA
Admin Phone: +507.8365503
Admin Phone Ext: 
Admin Fax: +51.17057182
Admin Fax Ext: 
Admin Email: 3fd40fbd82894113a145535926a6c47f.protect@whoisguard.com
Registry Tech ID: 
Tech Name: WhoisGuard Protected
Tech Organization: WhoisGuard, Inc.
Tech Street: P.O. Box 0823-03411 
Tech City: Panama
Tech State/Province: Panama
Tech Postal Code: 
Tech Country: PA
Tech Phone: +507.8365503
Tech Phone Ext: 
Tech Fax: +51.17057182
Tech Fax Ext: 
Tech Email: 3fd40fbd82894113a145535926a6c47f.protect@whoisguard.com
Name Server: rs60a.registrar-servers.com
Name Server: rs60b.registrar-servers.com
DNSSEC: unsigned
URL of the ICANN WHOIS Data Problem Reporting System: http://wdprs.internic.net/


As of October 13th, the domain has been cancelled and the account suspended. Thanks Namecheap!
