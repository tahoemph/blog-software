+++
date = "2018-07-04T11:24:54-07:00"
topics = [""]
keywords = [""]
author = "Michael Hunter"
title = "Crostini finding command"
tags = ["crostini"]
description = "Finding CLI commands in Crostini."
draft = false
type = "post"
+++

One of the features of the shell in the Linux distributions I've used
that I find very useful is suggestions as to what package a command
might exist in.  This need is increased in Crostini as the default
environment is very bare.  This came to a head the other day when I tried
to use cal and it didn't exist.

After some searching I discovered apt-file.

```console
tahoemph@penguin:~$ cal
-bash: cal: command not found
tahoemph@penguin:~$ sudo apt-get install apt-file
[...]
Setting up apt-file (3.1.4) ...
tahoemph@penguin:~$ apt-file search --regexp '/cal$'
9base: /usr/lib/plan9/bin/cal
bash-completion: /usr/share/bash-completion/completions/cal
bsdmainutils: /usr/bin/cal
tahoemph@penguin:~$ sudo apt-get install bsdmainutils
Reading package lists... Done
[...]
tahoemph@penguin:~$ cal
     July 2018
[...]
```

Yea.  But I still would like the automatic behavior that I expect
is implemented somewhere.  Additional searching and I discover
there is a script with the name command-not-found which is executed
when bash can't find a command.  Using apt-file I find what package
contains that script and install it and then I have a shell which helps
me flesh out my Crostini environment more easily.

```console
tahoemph@penguin:~$ apt-file search --regexp '/command-not-found$'
command-not-found: /usr/bin/command-not-found
command-not-found: /usr/lib/command-not-found
command-not-found: /usr/share/command-not-found/command-not-found
tahoemph@penguin:~$ sudo apt-get install command-not-found
[...]
Setting up command-not-found (0.2.38-4) ...
tahoemph@penguin:~$ cal
-bash: /usr/bin/cal: No such file or directory
```

This doesn't work until you reload bash.  If you open another shell
then you will see

```console
tahoemph@penguin:~$ cal
The program 'cal' is currently not installed.  To run 'cal' please ask your administrator to install the package 'bsdmainutils'
cal: command not found
```

Nice.
