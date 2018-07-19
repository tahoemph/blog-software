+++
title = "Walking our API using Python 2 showing decomposition through generators"
topics = []
author = "Michael Hunter"
description = "In this part of the series we show how we can create a nice decomposition of a problem using Python 2."
draft = false
type = "post"
date = "2018-07-19T10:25:30-07:00"
tags = ["Software Development", "Etudes", "Concurrency", "Python 2"]
keywords = []
+++

In the previous [post](/post/software-concurrency-walking-api-js) in this series
we motivated our study, build a toy server to run against, and showed how we
might walk our paginated API in pre-ES6 JavaScript.  I didn't like the lack of
separation of concerns when building that code.  In this post I am going to
show what I like about sovling the same problem in Python 2.  We can do better then
this in ES6+ JavaScript and Python 3 but I will leave that for later
posts.

The code for this post is on
[github](https://github.com/tahoemph/etudes/tree/master/concurrency/paginated_api/python2).
It is intentionally over engineered to show how you can compose software with generators.
Python generators allow you to construct a function which acts like an iterator (can be used
in a loop).  In this case we [construct](https://github.com/tahoemph/etudes/blob/795bfc094cded0aa0c238118adc0884fb7fb5fdb/concurrency/paginated_api/python2/walk.py#L21)
a stack of iterators.  That is done alongside the code that would use
the resulting iterator but in a larger piece of code you could construct this stack
based on user input independent of your processing concerns.
This structure separates the concern of what data is being processed from
what is being done to it.  At the bottom level of our stack we have
`next_page` which is an generator which retrieves the next page of data.  On top of that
we stack a generator which returns the python array representing our application data.
And at the top of that stack we have a generator which returns each individual entry
on our page.  While this stack of things is contrived you can imaging other processing
happening in a stack of generators.

Our processing loop looks like

```python
for entry in takewhile(lambda value: value < 43, construct_iterator()):
    print entry 
```

The function `takewhile` comes from the package `itertools` which provides iterators
that you can use.  I didn't include it in the earlier stack of generators to show
how a piece of code could be handed an iterator and then do further composition
to manage the data it needs to process.

The `print` statement here represents what could be much more processing.  Iterators
are useful for retrieving and filtering data you want to process but might not
be the right tool for doing further work.  For example writing each entry to a database
would be an odd side effect for an iterator.
