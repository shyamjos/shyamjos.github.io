---
layout: post
published: true
title: "The curious case of MGMNT ssid and Airtel wifi routers "

categories: hacking,router,wifi,IoT

comments: true

---

 Some of the wifi routers (especially beetel models) provided by airtel broadband is paired with two SSIDs(Access point), One is actual SSID for internet access and another one is MGMNT which used by airtel for maintenance / automatic configuration. 
 The default key for MGMNT is `0987654321` which is hard-coded into the router's firmware and the stupidest part is there is no option to disable it.

![router hacking](/assets/img/hardcoded-password-meme.jpg){: .align-right}

Now lets start hacking!, Connect to MGMNT SSID with the key `0987654321`.
Then Navigate to `192.168.1.1` in your browser and login with the default credentials username: admin and password: password
If you are lucky now you can see a network status page (view only) 


In recent models airtel patched a vulnerability that allows an attacker to view/change the password of the main SSID by connecting to MGMNT and browsing to the URL : `http://192.168.1.1/basic/home_wlan.htm`.Since the router i am testing was running on a patched firmware so it didn't worked.

So the next option was Telnet, I was able to telnet into the router with the credentials admin/password.

```
Telnet 192.168.1.1
```
![hacking router](/assets/img/wifi-router-hacking.png  "Airtel router telnet ")

Bingo! after playing with telnet for sometime I found the password for main SSID by typing the command:

```
show wlan config
```
![alt text](/assets/img/airtel-wifi-password.png  "hacking airtel wifi password ")

I was also able to hack another airtel router in a coffee shop with my andriod phone using [terminal emulator app](https://play.google.com/store/apps/details?id=jackpal.androidterm&hl=en).

![router hacking](/assets/img/airtel-wifi-android-hacking.png){:height="300pxdth="150"}

airtel patched vulnerability in web interface but forgot to patch telnet service which is accessible through the MGMNT ssid , An attacker can use the default user account which has full privilege to view and modify router configuration via telnet.


### How to disable MGMNT ssid ?
Currently there is a workaround for this problem, by modifying the router configuration backup file and restoring it back.Please see this [stackoverflow answer](http://superuser.com/questions/449289/how-to-prevent-wifi-router-from-broadcasting-multiple-ssids/925810#925810).Also change your router's default password as soon as possible.








