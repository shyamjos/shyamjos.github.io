---
date: 2017-08-24
title: "How to create or restore efi partition in ubuntu"
slug: how-to-restore-or-create-efi-partition-in-ubuntu
description: "What Type of file system is used in EFI partition ? EFI partition in Ubuntu is basically a FAT partition with label `EFI`"
images:
- /assets/img/featured.jpg
tags: [ "linux","ubuntu"]
keywords: ["efi", "partition", "ubuntu"]
---

## What Type of file system is used in EFI partition ?

EFI partition in Ubuntu is basically a FAT partition with label "EFI"

## How to create / restore an efi partition ?

Just reformat or create a normal FAT file system partition with a size of 512MB (can be any size) and label it as "EFI", You can use fdisk command if you are comfortable with cli or you can use gparted tool from a live media of Ubuntu to create new efi partition.

## How can I reinstall Grub efi bootloader after creating or restoring efi partition ?

After restoring or formatting efi partition your system will not boot since bootloader needs to be reinstalled on the new efi partition, follow this [tutorial to reinstall grub efi bootloader in your Ubuntu](https://shyamjos.com/reinstall-grub2-efi-bootloader-ubuntu/) system.
