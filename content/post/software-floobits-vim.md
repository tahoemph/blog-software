+++
date = "2018-07-18T11:40:06-07:00"
tags = ["Software Development Environment"]
topics = []
keywords = []
description = "Figuring out how to use Floobits with [n]vim."
draft = false
title = "Configuring Floobits with [n]vim"
author = "Michael Hunter"
type = "post"
+++

I wanted to pair program with an associate the other day.  The environment we used
was [Floobits](https://floobits.com).  Along the way I ended up changing from using
[Vim](https://www.vim.org) to [Neovim](https://neovim.io).  This article is a
recounting of some of the issues I resolved in this process.

Floobits is a nice envirionment for shared coding.  It uses a centralized server to
share modifications.  Out of this is it gets the ability to mediate changes from multiple
editors.  While it has a built in web editor you can also use a variety of editors including
Emacs, Sublime, Neovim, IntelliJ IDEA, and Atom.

I've used various editors over the years
including Black Beard, Emacs, and LSE (VMS).  I've done light editing tasks
in ed, Nano, and others I only hazily remember.  But for the last quarter of
a century or so I've used Vim a large portion of the time.  Muscle memory is
strong with this one.  My most recent try at switching editors was to
[Visual Studio Code](https://code.visualstudio.com) which is an awesome
product.  But I never got past the point where it was more friction then value.

You might note above that I said Floobits supports Neovim.  Neovim is a fork /
rewrite of Vim to better support asynchronous plugins as one of its priorities.
There is a plugin for Vim but after some initial trial and error I couldn't get it
to really work.  So I decided to take the pluge and switch to Neovim.  Last time
I tried it was too immature but it should be drop in and it had been a year
or more since my last attempt.

You can find guides for moving from Vim to Neovim in the Neovim documentation and
in various places online.  Mostly you want to take your .vimrc and copy it to
.config/nvim/init.config.  Some people try to build a link so they can switch
back and forth but I just took all of my Vim configuration and moved it aside
and built what I wanted for Neovim.

An immediate problem I ran into as I tried to edit basic things was the escape key
took a long time to register.  This turns out to be an interaction with tmux.  If
you change the delay time for escape to be detected in your .tmux.conf that goes away.
Specifically I added the following line to my ~/.tmux.conf

```console
set -g escape-time 10
```

From there you need to make certain your init.vim contains reasonable config.
I use Vundle and decided to stick with that instead of changing to one of the
newer package managers which work with Neovim.  Moving my existing Vim configuration
out of the way so that packages were updated seemed to help.  YMMV.  For Floobits
you will want to add

```console
Plugin 'floobits/floobits-Neovim'
```

to your init.vim.  Note that 'floobits-neovim'.  I had forgotten to change that from
'foobits-vim' and spent a few moments scratching my head.  The plugin complaining
about not having python support in Vim was the confusion and the clue.  Neovim doesn't
have to be compiled with extension language support to take advantage of it.

After that you can grab your configuration from Floobits and drop it in
~/.floorc.json.  As a complete json blob this is available from the Floobits
settings panel.  I was really happy not to have to put this together out of a template
and bits as is normal with many online services of this type.  Only a savings of a few
minutes but a really nice touch by Floobits.

At this point everything worked together nicely.  I only tested this between the online
editor and Neovim.  I havn't tried this between somebody using Neovim and Sublime (for example).
