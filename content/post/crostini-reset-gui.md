+++
date = "2018-07-06T10:30:33-07:00"
keywords = []
type = "post"
title = "Crostini Resetting when access to :0 fails."
tags = ["crostini"]
topics = []
description = "Resetting the VM those times you can no longer start a GUI program."
author = "Michael Hunter"
draft = false
+++

Crostini seems to get itself into a spot where it can no longer open the display.
I havn't tried to root cause this.  But I do know how to reset it.  This is a
pretty big hammer that might be useful when your VM seems to get itself into
a bad spot.

The following is the clue I get that there is an issue running GUI programs from Crostini.

```console
tahoemph@penguin:~$ /usr/bin/google-chrome-stable

(google-chrome-stable:5098): Gtk-WARNING **: cannot open display: :0
```

The way to resolve this involves stopping the VM and restarting it.
First start crosh with [Ctrl][Alt][T].  Then issue the following
sequence of commands.

```console
crosh> vmc list
termina
Total Size (bytes): 12374966272
crosh> vmc stop termina
Unable to stop vm
crosh> vmc start termina
(termina) chronos@localhost ~ $ 
```

My experience has been mixed.  Sometimes you can stop the VM.  And sometimes it
seems to have already been stopped.  In this case I had rebooted the Chromebook
because I'd forgetten starting chrosh directly fails.  This is probably why the
termina VM wasn't running.
Also, in this case I ended up with a prompt that
isn't normal for crosh.  From what I remember that hasn't happened before.

This could be a dangerous set of steps so if you are worried about the data in Crostini
back it up first.  Definitely if you ever consider 'vmc destroy' backup any unique data.
