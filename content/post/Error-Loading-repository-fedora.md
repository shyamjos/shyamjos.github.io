---
date: 2023-05-16
title: "Fix - Error: Loading repository 'fedora' has failed"
slug: Error-Loading-repository-fedora
description: "After some debugging I found out that this is due to a corrupted repo cache, we can easily fix this error by clearing all repo caches by running the below command"
images:
- /assets/img/featured.jpg
tags: [ "dnf","fedora"]
keywords: ["linux", "fedora"]
---
Recently when I tried to update my Fedora laptop I got the below error message

```
Error: Loading repository 'fedora' has failed
```

After some debugging I found out that this is due to a corrupted repo cache, we can easily fix this error by clearing all repo caches by running the below command 

```
sudo dnf clean all
```

If that doesn't work, you can run dnf command with debug options to see more details about the error.

```
dnf update --debuglevel 3
```
