---
date: 2017-08-24
title: "How to reinstall grub2 efi bootloader on ubuntu"
slug: reinstall-grub2-efi-bootloader-ubuntu
description: "In this tutorial I will show you how to reinstall grub2 bootloader on a ubuntu system with efi partition."
images:
- /assets/img/featured.jpg
tags: [ "linux","ubuntu"]
keywords: ["grub2", "grub", "reinstall", "linux", "ubuntu", "efi partition"]
---
In this tutorial I will show you how to reinstall grub2 bootloader on a ubuntu system with efi partition.

## Boot from a live usb/cd

Boot from the ubuntu live usb/cd and select the option "try ubuntu without installing"

## Check if EFI is enabled in bios

Enter below command in terminal\
```
[ -d /sys/firmware/efi ] && echo "EFI boot on HDD" || echo "Legacy boot on HDD"
```

If you see "EFI boot on HDD" Message then you are already running on efi mode or if you see "Legacy boot on HDD" message then your system is not running on efi mode, you must change the boot options to efi before proceeding to next step.

Note: First you have to find the partition name where ubuntu is installed, You can use "sudo fdisk -l" to list all hard disks and partitions in your computer. In my case /dev/sda is the name of my harddisk, /dev/sda2 is the partition where ubuntu is installed (root partition) and /dev/sda1 was the efi partition.

## Mount and chroot into local filesystem

Note: You have to replace the sda with device name of your HDD, In most cases it is sda, assuming that you have only one hard disk installed.

Note: If you get any errors while trying to mount your efi partition (`/dev/sda1`), You may need to reformat your efi partition, In case if it got corrupted or if you  accidentally formatted it. [Follow this tutorial to restore or reformat your efi partition](https://linuxsuperuser.com/how-to-restore-or-create-efi-partition-in-ubuntu/).

Open terminal and enter below command\
```
sudo mount /dev/sda2 /mnt\
sudo mount /dev/sda1 /mnt/boot/efi\
for i in /dev /dev/pts /proc /sys /run; do sudo mount -B $i /mnt$i; done\
sudo chroot /mnt\
grub-install /dev/sda\
update-grub\
```
Important : ***use blkid command to check UUID of your efi partition, check if it matches  the value in your /etc/fstab entry , otherwise ubuntu will not boot , You may need to update the UUID especially if you have formatted EFI partition . (Eg: sudo blkid /dev/sda1)***

That's it!  Now reboot to test the bootloader
