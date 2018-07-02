+++
title = "Crostini upgrade pain"
keywords = []
description = "A problem I encountered upgrading my Chrombook."
draft = false
date = "2018-07-02T08:42:07-07:00"
tags = ["crostini"]
topics = []
author = "Michael Hunter"
type = "post"
+++

Not all goes well when you are on the bleeding edge.  When upgrading from
"10798.0.0 (Official Build) dev-channel eve" to "Version 69.0.3473.0 (Official Build) dev (64-bit)"
I ended up encounting a problem.  Before upgrading I backedup all of my user files in the VM.  This
ended up saving me.

After upgrade I was somewhat surprised that my VM seemed to be whole and viable.  But after less than
an hour the Chromebook froze and I needed to refresh-reboot it.  It came up but when I tried to start
the Terminal it spun and nothing happened.

I ended up in crosh and ultimately removed the vm with 'vmc destroy termina'.  This was after failure
attempting to start/stop the VM.  Then I could start a blank VM And restore my content losing only what
I had done in the interim.

I gathered little data about what the problem was.  This was my first time on crosh.  I'll have to
develop some muscle around manipulating VMs so that if I run into difficulties in the future I will
have a better chance of root causing and possibly saving the existing VM.
