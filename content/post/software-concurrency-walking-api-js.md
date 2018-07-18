+++
title = "Walking an API using old JavaScript"
keywords = []
draft = false
type = "post"
date = "2018-07-18T15:12:21-07:00"
tags = ["Software Development", "Etudes", "Concurrency", "JavaScript", "Golang"]
topics = []
description = "Beginning of a series talking about concurrency through the lens of walking a paginated API."
author = "Michael Hunter"
+++

Since I started programming I've created software experiments.  A subset of
those are practice for using a feature of a language, library, or framework.  I have gathered
these at various points in my life but am going to become a bit more rigorous about that
and collect them in github in a single repository
[etudes](https://github.com/tahoemph/etudes).  That is somewhat at odds
with common git usage of maintaining more mono-use repos but these kinds of things tend to
burst into being quickly and then after being useful go away.  So the overhead of creating new
repos for them would probably mean they were ultimately lost.  I am going to try to save more
of them in git and talk about some of them here.

A while ago I
became interested in the various mechanisms languages and their libraries used for managing
asynchronous requests.  Some languages provide good support for concurrency out of the box
whereas in others it takes a bit of work.  This had been a tickle when I was working in python
but became much more interesting as I spent time with JavaScript and started looking at
newer JavaScript features like async/await and iterators/generators.

The basic problem I am going to use to play with the various languages and features is going to
be the task of walking a paginated API.  On the surface this is fairly basic but provides enough
richness to let us tease out differences.  The high level interface I am shooting for is the
ability for the iterator to return each element that is represented on the page to the caller
without the caller knowing the page structure.  From the callers standpoint this should
look like iteration in the context of the language being examined.  Being able to compose
iterators together into a stack that pulls and manipulates our data in a way that the high
level consumers doesn't have to worry about is a goal.

There are three reasons we want to see if we can get to this structure.

1. We want to be able to separate concerns of managing async interactions and business logic into sperate pieces of code.
2. We want to be able to apply optimizations (e.g. pre-fetching) without changing the structure of the higher level code.
3. We want to be able to compare languages on a level playing field.

We could use an API which is online.  But at some point in this etude I want to be able
to investigate performance.  Having an API over a network will allow us to see
normal networking effects but won't allow us to measure performance in a consistent way.
Instead I have provided a simple server written in [go](https://golang.org/).
At some point we might modify
it to emulate network latency so that we can better see the effect of overlapping I/O.
For the moment this is the simplest network server I can write in go.  It handles
each request serially and returns very simple fake data.  I present it on
[github](https://github.com/tahoemph/etudes/tree/master/concurrency/paginated_api/server)
without further comment.

The initial client code is pre-async/await JavaScript.  It does uses
[bluebird promises](http://bluebirdjs.com) to make organization of the code
somewhat better.  But in the end that could easily be done with callbacks.
It is hard to organize code in this era of JavaScript even with promises so that
the various concerns are separated.  By definition the code knows that something
async is happening even if it is a function call away.  The outer loop
looks
[like](https://github.com/tahoemph/etudes/blob/79bf61e9996e4c515c8d83f5365e78f60467c08e/concurrency/paginated_api/js/walk.js#L41)

```javascript
walker.next().then(function(data) {
    console.log(data.Data[0], data.Data[data.Data.length -1]);
    if (++numPages < 10) {
        getData()
    }
});
```

The "processing" of the data is contained in the console.log statement but the need to
know about pages is hard to pull out.  We could hide it under a closure with its own protocol
but it would be hard to express as a simple for loop.  I am not going to spend any more
time with this code as getting to my ideal would be hard and there are better ways to
write this in JavaScript these days.  This is here as a baseline for JavaScript.
