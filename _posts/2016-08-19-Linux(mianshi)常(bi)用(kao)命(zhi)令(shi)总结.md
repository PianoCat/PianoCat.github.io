---
layout: post
title: Linux(面试)常(必)用(考)命令总结(实时更新)
category: Linux
tags: [Linux, shell]
---

1. `top`命令

> display Linux processes: The  top program provides a dynamic real-time view of a running system.  It can display system summary information as well as a list of processes or threads currently being managed by the Linux kernel.  The types of  system summary information shown and the types, order and size of information displayed for processes are all user configurable and that configuration can be made persistent across restarts.

2. `uptime`命令

> Tell how long the system has been running: uptime  gives  a one line display of the following information.  The current time, how long the system has been running, how many users are currently logged on, and the system load averages for the past 1, 5,  and  15  minutes.

3. `w`命令

> Show who is logged on and what they are doing: w  displays  information  about  the users currently on the machine, and their processes.  The header shows, in this order, the current time, how long the system has been running, how many users are currently logged on, and the system load averages for the past 1, 5, and 15 minutes.

4. `scp`命令

> secure copy (remote file copy program): scp copies files between hosts on a network.  It uses ssh(1) for data transfer, and uses the same authentication and provides the same security as ssh(1).  Unlike rcp(1), scp will ask for passwords or passphrases if they are needed for authentication.
