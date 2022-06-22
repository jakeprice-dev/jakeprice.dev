---
title: Auto Connect a VPN on Windows 10 at Start Up
date: 2017-06-11T19:25:45+01:00
updated: 
type: post
tags: [vpn, network, security, privacy]
draft: false
---

Here's a handy little command for a .bat file for those of you that may use a VPN, and would like to forget about having to automatically enable it.


```cmd
rasdial myVPN
```

Open up Notepad and paste the above in, and make sure you replace myVPN with the name of your VPN connection, save the file as .bat into your Start-up folder. You should find the Start-up folder here on Windows 10, obviously just replace USERNAME with your Windows Username.

```text
C:\Users\USERNAME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
```

Then, next time you are starting up, you’ll see a command prompt window pop-up and you’ll see it logging into the VPN, and your good to go.
