---
date: 2013-10-03
linktitle: "Decoding NASA's NOAA weather satellite signals with RTL-SDR"
title: "Decoding NASA's NOAA weather satellite signals with RTL-SDR"
weight: 10
categories: [ "rtlsdr"]
---

NOAA satellite is a series of weather satellites launched by NASA. It carries a suite of instruments that provides data for weather and climate predictions, everyday multiple NOAA weather satellites pass above us. Each NOAA weather satellite broadcasts an Automatic Picture Transmission (APT) signal (137MHZ), which contains a live weather image of our area. RTL-SDR dongle combined with a good antenna and programs like GQRX, sdrsharp and WXtoImg we can decode this signals.
![rtlsdr dvb dongle image](/assets/img/noaa/rtlsdr-dongle.jpg)
If you are not familiar with RTL-SDR, RTL-SDR is a very cheap software defined radio that uses a DVB-T TV tuner dongle based on the realtek RTL2832U chipset. Basically , this means that a cheap $20 TV tuner USB dongle with the RTL2832U chipset can be used as a computer controlled radio scanner.

After a long trial and error process with different antennas finally I am surprised with APT signal reception from my simple ground plane antenna which is made from coat hanger.I don't no more technical stuff about antennas, My GP antenna have 22 inch long radials ( slant down at an angle of 45 degrees) [close up photo of antenna](http://i.imgur.com/rq3t1W1.jpg).

![rtlsdr ground plane antenna](/assets/img/noaa/ground-plane-antenna-rtlsdr.jpg)

  The 4 radials are connected to metal base plate and the center radial is wrapped in an insulation tape (no contact with metal plate or other 4 radials ) I used a 75 ohm coax cable for the feed line and it is less than 5 meter long, center copper wire of coax is connected to the center radial and silver wires to the metal base plate.



## Software setup

Software used is sdrsharp (RF gain 100% ,40~42khz bandwidth,90% AF gain,Sample Rate: 1,024 MSPS,audio sample rate: 48000) and the audio is piped to WXtoImg via Virtual Audio Cable (48000 sample rate output).

![sdr#](/assets/img/noaa/rtlsdr-dongle-noaa.jpg)

## Decoded Images 

### NOAA 18
![NOAA 18 india image](/assets/img/noaa/noaa-18-image.jpg)

### NOAA 19
![NOAA 19 india image](/assets/img/noaa/noaa-19-rlsdr-image.jpg)

### NOAA 15
![NOAA 15 india image](/assets/img/noaa/noaa-15-image-rtlsdr.jpg)

### NOAA 15 - Sea surface temperature
![NOAA 15 india Sea surface temperature image](/assets/img/noaa/noaa-sea-level-rtlsdr.jpg)

discussion on [reddit ](https://www.reddit.com/r/RTLSDR/comments/1no5sh/received_noaa_images_using_my_coat_hanger_ground/).
