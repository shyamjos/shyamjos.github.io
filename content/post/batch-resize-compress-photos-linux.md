---
date: 2019-09-19
title: "How to batch resize and compress images in linux"
tags: [ "linux","bash","automation"]
---
![retro cmaer](/assets/img/ImageMagick/retro-camera-black.jpg)
In this tutorial I will show you how to batch resize and compress images in Ubuntu or in any other Linux distros(debian,arch and fedora).

'Convert' command is a very powerful image manipulation utility which comes preinstalled in almost all Linux distributions (ubuntu,debian,arch and fedora) and it is a part of ImageMagick software suite.

## Check if convert command is available on your Linux distro

```
 convert -version
```

output:

Version: ImageMagick 6.9.7-4 Q16 x86_64 20170114 http://www.imagemagick.org
Copyright: © 1999-2017 ImageMagick Studio LLC

If the above command is not found on your Linux distro you can install it by typing the below command.

## Install convert tool on Ubuntu / Debian

```
 sudo apt-get install imagemagick
```

## Install convert tool on fedora

```
 sudo dnf install imagemagick
```

## Install convert tool on arch

```
 sudo pacman -S imagemagick
```

Note: *It's always good idea take backup of your images before  running convert command.*

## Batch resize and compress images with convert command

Below command will resize and compress all images ending with .jpg extension in a 'for loop' and save the compressed/resized image as 'filename-Optimized.jpg'.

**--quality :**  this option is used to set the image compression level in percentage

**-resize :** this option is used to resize the image to a given resolution , You can use  -resize option with width ( -resize 1600x ) only or both width and height ( -resize 1600×900), In both cases convert command will automatically adjust the given resolution to get optimum aspect ratio  so you don't have to worry about stretched images.

Note: some jpeg image extensions may end with .JPG (in capital letters) ,Since Linux is case-sensitive you may need to adjust the bash script accordingly.

Open terminal and cd into the directory containing your photos and execute below command

```
 mkdir photos-Optimized;for photos in *.JPG;do convert -verbose "$photos" -quality 85% -resize 1600x900 ./photos-Optimized/"$photos-Optimized.jpg"; done
```

Voilà! Now you have successfully resized/compressed images, You can see the optimized images in the photos-Optimized directory.
