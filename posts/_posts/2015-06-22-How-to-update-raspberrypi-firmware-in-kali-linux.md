---
layout: post
title: Update Raspberry pi firmware from Kali Linux
categories: rpi, firmware, linux
date: 2015-06-22 00:11
comments: true
published: true
---

We can easily update Raspberry pi firmware in raspbian by running the command rpi-update, But in kali linux we dont have rpi-update command by default.
<br><br>
To install the rpi-update  in kali, run the following command:


{% highlight sh %}
sudo curl -L --output /usr/bin/rpi-update https://raw.githubusercontent.com/Hexxeh/rpi-update/master/rpi-update && sudo chmod +x /usr/bin/rpi-update
{% endhighlight %}

Then, to update your rpi firmware, run the following command:

{% highlight sh %}
sudo rpi-update
{% endhighlight %}

Now restart your rpi to new frimware to take effect.
<br>
For more Expert options visit the [rpi-update project page](https://github.com/Hexxeh/rpi-update)

