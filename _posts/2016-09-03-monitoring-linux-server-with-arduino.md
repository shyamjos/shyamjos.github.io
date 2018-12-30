---
layout: post
published: true
title: "Monitoring Linux Server with an Arduino"

categories: arduino,IoT,linux

comments: true

---

As usual I was so bored and wanted to build something cool on this weekend, So I ended up building an Arduino based Linux server monitoring solution for monitoring my Linux VPS.

The idea was Simple, use an Arduino Ethernet module to make a get request to the php script hosted on the server and parse the response data (free -m,df -h,uptime) and display it on the LCD screen every one minute.


And here is the demo of Arduino Linux monitor in action

## Demo 
![demo](https://i.imgur.com/CNQ7JSf.gif "demo")


If you are interested in this project you can download the Arduino sketch from my [github page](https://github.com/shyamjos/Arduino_ServerMon). 

Todo List 
---------

* Buzzer Notification upon increase in memory/cpu load..etc
* Ditch PHP and use a lighter json api