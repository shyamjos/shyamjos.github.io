---
date: 2017-05-14
title: "A better email template for icinga2"
slug: icinga2-html-template
description: "I have created a very simple HTML email alert Template for Icinga 2 to replace the default boring text-based email alert"
images:
- /assets/img/icinga2/html-template-for-icinga.png
tags: [ "monitoring"]
keywords: ["icinga", "icinga2", "template", "theme", "email"]
---

I have created a very simple HTML email alert Template for Icinga 2 to replace the default boring text-based email alert. This template can be easily installed by replacing existing alert scripts inside /etc/icinga2/scripts.

**Update:** I have replaced mail command with mutt due to an incompatibility of options among different Linux distributions. Also, I have added new color highlight feature for different states (ok=green,warning=orange and critical=red).

## Screenshots 

![Icinga2 email alert screenshot](/assets/img/icinga2/html-template-for-icinga.png)
![Icinga2 email alert screenshot](/assets/img/icinga2/icinga-2-html-email-template.png)
![Icinga2 email alert screenshot](/assets/img/icinga2/icinga-html-email.png)

## Prerequisite 
Make Sure mutt package is installed on your server

## How to install

* Backup existing  script files (mail-service-notification.sh and mail-host-notification.sh) inside /etc/icinga2/scripts
* Download the scripts from this github repo and edit the “Variables for HTML Template” section in both scripts
* Now replace the existing scripts with the new ones and Send a custom notification to test new HTML email template.

If you have any issues, please [report it here](https://github.com/shyamjos/HTML-email-template-for-Icinga-2/issues)



