---
date: 2018-10-03
title: "Ripping DVDs in linux with FFmpeg"
description: "In this tutorial, I will show you a simple way to RIP DVD into a single file using FFmpeg command line tool in Linux."
images:
- /assets/img/dvd-ripping/dvd-linux.webp
tags: [ "linux"]
---
![dvd ripping in linux](/assets/img/dvd-ripping/dvd-linux.webp)
In this tutorial, I will show you a simple way to RIP DVD into a single file using FFmpeg command line tool in Linux.

## Install FFmpeg in Ubuntu/Debian/Linux Mint

```
sudo apt-get install ffmpeg
```

Now copy contents of your DVD to local folder and cd into that folder(eg: video_ts)

## 1\. RIP DVD into a single file

Now enter below command to start ripping process in optimum quality, If you want to control the size (eg: limit size to 700MB) of the ripped file, then use the third command

```
cat VTS_0*_*VOB | ffmpeg -i - -vcodec h264 -acodec mp2 rip.mp4
```

## 2\. RIP DVD with deinterlace option

If you want to enable deinterlace option run below command

```
cat VTS_0*_*VOB | ffmpeg -i - -vf yadif -vcodec h264 -acodec mp2 rip.mp4
```

## 3\. RIP DVD with quality option

Use below command to reduce size and quality of output file, Here the '-crf' option sets the quality of the ripped file. The range of the CRF scale is 0--51, where 0 is lossless , 23 is the default, and 51 is the worst quality possible.

```
cat VTS_0*_*VOB | ffmpeg -i - -c:v libx264 -crf 23 rip.mp4
```

Above command will read all video files in a folder and pipe the stream to FFmpeg command, after the successful completion of the command you can find the ripped file with name `rip.mp4`
