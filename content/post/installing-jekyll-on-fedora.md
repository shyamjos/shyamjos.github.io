---
date: 2015-01-16
title: "Installing Jekyll on fedora"
slug: installing-jekyll-on-fedora
description: "Follow below steps to install jekyll on fedora"
images:
- /assets/img/misc/jekyll-logo-linux.png
tags: [ "fedora","linux"]
keywords: ["fedora", "linux", "Jekyll"]
---
![jekyll logo linux](/assets/img/misc/jekyll-logo-linux.png)
Follow below steps to install jekyll on fedora

## Install jekyll
```
sudo dnf install ruby-devel redhat-rpm-config jekyll
```
## Optional packages
```
sudo dnf group install "C Development Tools and Libraries"
sudo dnf install rubygems-devel nodejs bundler
```

