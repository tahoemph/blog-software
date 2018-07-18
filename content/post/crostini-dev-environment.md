+++
tags = ["crostini"]
keywords = []
draft = false
topics = []
description = "How to use a Chromebook for Application development."
author = "Michael Hunter"
type = "post"
date = "2018-07-01T20:18:24-07:00"
title = "Crostini dev environment"
+++

I have become less then enthused with the macOS environment due to its odd set of choices
and constant friction with open source tools.  My first thought was to
get a Linux laptop thus removing the OSS friction.  I also tried an Ubuntu 18 install
on my MacBook but that had various issues and felt like a waste of the hardware.

I like the idea of Chromebooks.
Security, long battery life, and a fair bit of stability are important to me for application
development tasks.  So I took several shots at using a Chromebook and finally
have found a development environment that works.

First I tried this using termux following this
[article](https://blog.lessonslearned.org/building-a-more-secure-development-chromebook/)
using a Samsung Chromebook Plus.  This is an ARM based machine which a really nice IPS
screen.  Somewhere between the processor maybe not having enough oomph and setting
up the termux based environment this failed.  It felt clunky and not something that
would be easy to maintain and update.

About the time I gave up on termux Google
[announced](https://liliputing.com/2018/04/googles-crostini-lets-you-run-gnu-linux-apps-on-chromebooks-without-enabling-developer-mode.html)
a VM based dev solution on Chromebooks called Crostini.  Initially it was very limited but it has grown
some reasonable capabilities.  Currently I am using ~~"10798.0.0 (Official Build) dev-channel eve"~~"Version 69.0.3473.0 (Official Build) dev (64-bit)".  With this upgrade tmux now works.  Yea!

Configuration information is available
[here](https://chromium.googlesource.com/chromiumos/docs/+/master/containers_and_vms.md).

Future articles will go into issues I encounter and how to resolve them.
