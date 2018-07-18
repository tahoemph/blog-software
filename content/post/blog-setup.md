+++
topics = []
keywords = []
author = "Michael Hunter"
draft = false
date = "2018-07-09T14:30:46-07:00"
title = "Blog setup"
tags = ["blog","hugo"]
description = "How this blog is being built."
type = "post"
+++

I've used various blog or publishing platforms in the past. When I
started documenting my software journey again I decided
that instead of using a more traditional platform I wanted to try a static
site generator.

A static site generator is one that takes some form of input for your site
and generates matching html, css, and javascript.  Note that the static in
static site generator doesn't imply that your site doesn't use JavaScript
but instead that the content of the site isn't gathered and built into the
page in the viewers browser.  For a blog that consists of a mostly linear
stream of content this isn't a restriction.  If I was publishing a site
that suggested content dynamically or I wanted to decouple publishing
content with deploying the site a static site generator wouldn't work.

I looked at several generators starting with [Jekyll](https://jekyllrb.com/) but
ended up settling on [Hugo](https://gohugo.io/).  This wasn't due to
any real feature differences.  I am interested in the go programming
language which Hugo is implemented in and thought this might an
opportunity to work some in go.  That said so far I haven't had to
dip into the Hugo source code.

Hugo (and other generators I looked at) all provide a
[theme library](https://themes.gohugo.io/)
that makes initial styling of your site easier.  Hugo has some nice
[documentation](https://gohugo.io/documentation/) discussing this.
I was a bit distracted
by the quickstart aiming me at a single theme when in reality the
later [suggestion](https://gohugo.io/themes/installing-and-using-themes/)
to install all themes worked better.  It made it easier for me
to try several themes until I found a good one.
Since I am not very designy one that didn't force me to choose beautiful
art was a better place to start.  The Hyde templates are good blog
templates of this type.  [Hyde-y](https://github.com/enten/hyde-y/)
was the one that I choose.  Since you copy the theme into your own
directory and go from there it is a starting point.  I don't expect
I'll track any future Hyde-y development.

Configuration of the theme is done via the config.toml file that
you can copy from the theme home page almost directly and them modify
with your personal data.  Sticking to basics initially is working great.
Until you have a fair bit of content worrying about polishing the
chrome of the site seems like a waste of effort.

Once you have the theme selected you have to decide how to
deploy it.  Initially I looked at Google Cloud Platform Cloud Storage
but it didn't seem to support https.  While none of my
content mandates https I really can't imagine publishing a site in 2018
that doesn't use it.  Using Firebase to deploy your site was the suggested
alternative.  Initially I had a hard time getting around my personal
bias for thinking of Firebase as just a realtime database.  But after
clearing that hurdle it was an easy follow the instructions process
to set it up.

I have a lot to learn about this set of tools.  I've posted a few
things that have highlighting but they are all console sessions.  And
I haven't been entirely happy with them.  I need to zero in on the
best way to post code and diagrams.  I also haven't explored
the difference in topics, keywords, and tags in Hugo.  I don't have
enough content at the moment to care about but those feel like
they could be important organizational concepts.
