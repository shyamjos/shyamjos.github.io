---
date: 2021-09-25
title: "How to redirect PreStop hook output to pod logs"
description: "So how can we see the PreStop hook command output in pod logs? By default container engine only redirects the stdout/err of the main process"
images:
- /assets/img/featured.jpg
tags: [ "logging","kubernetes","container"]
keywords: ["PreStop hook", "kubernetes", "container", "logging"]
---
You might have noticed that command output of PreStop hook won't appear in pod logs and only thing you can see is whether the PreStop hook command failed or not is by checking kubernetes events log. 

So how can we see the PreStop hook command output in pod logs? 

By default container engine only redirects the stdout/err of the main process (running with `PID 1`) to the logging driver. Since the PreStop hook runs as a separate process the output from this command won't appear in container logs.

## How to redirect PreStop hook command output to container logs ?

In Linux you can easily redirect stdout/err of one process to another by writing to the other process's stdout/err file descriptor (/proc/PID/fd/1 or /proc/PID/fd/2). In our case we can redirect the stdout of PreStop hook command to our main process's stdout using the command `echo "Hello from the other side" > /proc/1/fd/1` and this message will be appear in the container logs. 


## Example PreStop hook command with output redirection 
```
 lifecycle:
          preStop :
             exec:
               command: ["bash", "uptime > /proc/1/fd/1"]           
```
