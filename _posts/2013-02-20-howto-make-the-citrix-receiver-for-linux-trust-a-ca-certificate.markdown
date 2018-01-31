---
title: HowTo make the Citrix Receiver for Linux trust a CA certificate
date: 2013-02-20 20:17:00 -08:00
categories:
- fixes
tags:
- citrix
- receiver
- ssl
- linux
---

Recently I ran across the common error that my Citrix Receiver for Linux doesn't trust the CA certificate of my Citrix Access Gateway.

![xubuntuicaclientsslerror.png](/uploads/xubuntuicaclientsslerror.png)

To resolve this issue, please follow the instructions below:
1. Open your Access Gateway website with firefox
2. Click on the Lock left of https://... and choose "More Information"
3. Click on "View Certificate"
4. Change to the tab "Details"
5. Highlight your CA certificate in the Certificate Hierarchy field and click the "Export" button
6. Save the certificate (in X.509 Certificate (PEM) format) to your Desktop and give it the file extension .crt
7. sudo copy the file to /opt/Citrix/ICAClient/keystore/cacerts

Enjoy your working Receiver!
