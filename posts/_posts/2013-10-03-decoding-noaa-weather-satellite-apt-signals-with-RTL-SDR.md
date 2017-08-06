---

layout: post
title: "Decoding NASA's NOAA weather satellite signals with RTL-SDR"
categories: rtlsdr, sdr, noaa
date: 2013-10-03 00:11
comments: true
published: true
---

After a long trial and error with different antennas finally I am surprised with APT signal reception from my simple ground plane antenna which is made from coat hanger.I don't no more technical stuff about antennas, My GP antenna have 22 inch long radials ( slant down at an angle of 45 degrees) [close up photo of antenna](http://i.imgur.com/rq3t1W1.jpg).

<img src="/assets/img/noaa/ground-plane-antenna-rtlsdr.jpg">

  The 4 radials are connected to metal base plate and the center radial is wrapped in an insulation tape (no contact with metal plate or other 4 radials ) I used a 75 ohm coax cable for the feed line and it is less than 5 meter long, center copper wire of coax is connected to the center radial and silver wires to the metal base plate.



## Software setup

Software used is sdrsharp (RF gain 100% ,40~42khz bandwidth,90% AF gain,Sample Rate: 1,024 MSPS,audio sample rate: 48000) and the audio is piped to WXtoImg via Virtual Audio Cable (48000 sample rate output).

<img src="/assets/img/noaa/rtlsdr-dongle-noaa.jpg">

## Decoded Images 

### NOAA 18
<img src="/assets/img/noaa/noaa-18-image.jpg">

### NOAA 19
<img src="/assets/img/noaa/noaa-19-rlsdr-image.jpg">

### NOAA 15
<img src="/assets/img/noaa/noaa-15-image-rtlsdr.jpg">

#### NOAA 15 - Sea surface temperature
<img src="/assets/img/noaa/noaa-sea-level-rtlsdr.jpg">

Also checkout my [reddit post](https://www.reddit.com/r/RTLSDR/comments/1no5sh/received_noaa_images_using_my_coat_hanger_ground/) on the same.
