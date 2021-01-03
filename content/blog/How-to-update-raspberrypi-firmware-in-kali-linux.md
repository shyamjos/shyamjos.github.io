---
date: 2014-04-02
linktitle: "Update Raspberry pi firmware from Kali Linux"
title: "Update Raspberry pi firmware from Kali Linux"
weight: 10
categories: [ "infosec","linux"]
---


We can easily update Raspberry pi firmware in raspbian by running the command rpi-update, But in kali linux we dont have rpi-update command by default.
<br><br>
To install the rpi-update  in kali, run the following command:


```
sudo curl -L --output /usr/bin/rpi-update https://raw.githubusercontent.com/Hexxeh/rpi-update/master/rpi-update && sudo chmod +x /usr/bin/rpi-update
```

Then, to update your rpi firmware, run the following command:

```
sudo rpi-update
```

Now restart your rpi to new frimware to take effect.
<br>
For more Expert options visit the [rpi-update project page](https://github.com/Hexxeh/rpi-update)

