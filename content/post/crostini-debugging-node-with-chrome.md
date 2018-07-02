+++
title = "Crostini debugging node with Chrome"
keywords = []
description = "How to debug node applications in Crostini using Chrome."
author = "Michael Hunter"
date = "2018-07-02T08:51:14-07:00"
tags = []
topics = []
draft = false
type = "post"
+++

The integration of the Chrome Dev Tools with Node.js landed in Chrome 57 (it was exprimental before that).
You have to be using Node.js 6.4+.  This is a wonderful Node.js debugging environment.  On  single
machine it works with little effort.  But when working on a node app in Crostini it takes a bit of additional
effort.  This is because the "machine" you are running the node app on is different from where you want your
browser to be running.

Before I go into my solution it is worthwhile to mention that you can run chrome from within the Crostini
VM.  I found various issues with doing this.  The primary one is that the ChromeOS window manager doesn't
know about your Crostini Chrome windows.  This makes managing them on even a basic desktop less then great.
Also I found that sometimes I would start Chrome from Crostini and the keyboard was non-responsive.

There is a better solution!  Chrome supports remote debugging.  And by treating your Crostini instance as
a remote machine you can have the best of the Chromebook and Crostini worlds.  In order to do this you
will have to know something, configure something in Chrome in ChromeOS, and modify your invocation when
debugging.

The overview is that we will tell the ChromeOS Chrome that there is an external target.  That will require
that we know the Crostini IP address.  And when we invoke the node debugger we will tell it to bind to that
address instead of a local one.

In order to get your VMs IP address use ifconfig as below.

```console
tahoemph@penguin:~$ /sbin/ifconfig eth0
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 100.115.92.204  netmask 255.255.255.240  broadcast 100.115.92.207
        inet6 fe80::216:3eff:fe7f:30ad  prefixlen 64  scopeid 0x20<link>
        ether 00:16:3e:7f:30:ad  txqueuelen 1000  (Ethernet)
        RX packets 325869  bytes 2921520373 (2.7 GiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 248961  bytes 42623729 (40.6 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

You will need to take that and configure it into chrome.  Go to "about:inspect" (chrome://inspect/#devices).

![about:inspect](/images/chrome_inspect.png)

Choose "Configure" and enter 100.115.92.204:9229 (or whatever the IP address you discovered above was).  When done
and you return to the "about:inspect" tab you will discovered that now you have a "Remote Target" conigured.

When debugging you will need to tell inspect what address to bind to.  By default it will bind to localhost
which won't allow the remote debugger to attach.  You do work around this by supplying the --inspect-brk flag with
an IP address as below.

```console
tahoemph@penguin:~/src/personal/foreclosure_data$ node --inspect-brk=100.115.92.204:9229 main.js
Debugger listening on ws://100.115.92.204:9229/5435fdc1-0bc4-4656-bde1-f7748856d664
For help see https://nodejs.org/en/docs/inspector       
```

When you do this a target will appear under Remote Target in the "about:inspect" window and you can either
choose "Open dedicated Dev Tools for Node" or "inspect" under the target to begin debugging.
