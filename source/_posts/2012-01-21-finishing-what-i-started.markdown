---
layout: post
title: "Finishing what I started"
date: 2012-01-21T22:57:00-08:00
categories:
 - sympy
---

As of today, I'm happy to report that my last pull request for angular momentum
coupling was merged into master. The master branch now has the capability to do
arbitrary angular momentum coupling and uncoupling. I ended up writing a
summary of the algorithm I used to write this, which I briefly described (or
more accurately, brushed over) in the previous blog post, the write up for
which is currently hosted on github
[here](https://github.com/flacjacket/coupling_algorithm). This should be all of
the big changes for the angular momentum algebra I can foresee in the near
future.

At this point, school is starting back up again and especially since I have
joined a research group I won't be doing anything big in the near future. That
said, I do have a couple things I've started in on that I will try to finish up
if I can get some time. First, I started working on some changes to the quantum
printing framework. I have a pull request open for some new tests to the
quantum printing framework, so if that can get finished up I'll try to work
on getting those changes in. This was an issue that had been brought up
before (around the time I started the GSoC project) and even the work I've done
so far, I've dug up a couple issues with the printing framework. The current
pull for the tests are [here](https://github.com/sympy/sympy/pull/908) and the
changes to the printing framework which are to follow are
[here](https://github.com/flacjacket/sympy/tree/quantum_printing).

In addition, over winter break, I dug into some related issues with Piecewise,
particularly with the treatment of the otherwise parameter. Just today I opened
a pull request for collecting feedback on the changes I made
[here](https://github.com/sympy/sympy/pull/1009).

Now that the spin stuff is finished, I've been thinking about going back and
looking at the stuff I did at the beginning of the GSoC project, particularly
some of the stuff with CG coefficients and simplification of these terms. From
what I remember, there should be some quick changes to make some stuff run much
better, so if I get time, I'll take a look back at that.

Last, while I am quite happy with how the current angular momentum coupling and
uncoupling methods treat numerical cases, there's nothing really there for
treating symbolic cases and any symbolic arguments cause the methods to return
a very general summation. I put some thought into modifying the current
algorithm to allow for some forms of symbolic coupling and uncoupling, but I
wasn't able to come up with any. If I can sit down and find something that
could do symbolic coupling and uncoupling, that would be the icing on the cake
of the current algorithm.

With the merging of this pull request, everything that I set out to do for my
GSoC project last summer has been completed in some form.  There may be some
things to refine or work on, but for the most part, I have accomplished
everything I set out to do. Unless I make some big changes to the coupling
algorithm, like working out something with symbolic cases, or make some other
big change to the angular momentum algebra, this will likely be my last post
here, at least until something else comes up that I'd like to document.
