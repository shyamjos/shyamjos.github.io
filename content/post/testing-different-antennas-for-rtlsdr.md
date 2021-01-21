---
date: 2014-04-02
title: "Testing different DIY antennas for RTLSDR"
tags: [ "rtlsdr"]
---
![rtlsdr antennas](/assets/img/rtlsdr/rtlsdr-antenna.webp)
I have been experimenting with different DIY antennas for RTLSDR since 2013,Below is my review on different antennas I have tested so far.

## For decoding NOAA weather satellite Signals 
Quadrifilar Helix (QFH) Antenna is the most recommended antenna for APT signal reception, But I was too lazy to build one. So i decided to make a ground plane antenna with coat hanger. In my opinion GP antenna is the simplest and easy to make antenna for decoding APT signals.[Check out my NOAA images](http://shyamjos.com/decoding-noaa-weather-satellite-apt-signals-with-RTL-SDR) decoded with coat hanger GP antenna. 

## For decoding adb signals (tracking aircrafts)
Coaxial Collinear Antenna is the best antenna for long range adb signal reception,[On this page](https://www.balarad.net/) there is a good tutorial for making Coaxial Collinear Antenna.

## For decoding AIS signals (tracking ships)
Coaxial Collinear Antenna provides pretty good reception for AIS signals,[On this page](http://arundale.com/docs/ais/aerial.html) there is excellent instructions on constructing high gain coax collinear AIS antenna.

## For NFM/FM/WFM/AM Reception 
For me a [Ground plane antenna](http://shyamjos.com/decoding-noaa-weather-satellite-apt-signals-with-RTL-SDR/) worked pretty well for FM/FM/WFM/AM reception.You can use [GP antenna calculator](http://www.csgnetwork.com/antennagpcalc.html) to fine tune your GP antenna to a specific frequency for better reception.





