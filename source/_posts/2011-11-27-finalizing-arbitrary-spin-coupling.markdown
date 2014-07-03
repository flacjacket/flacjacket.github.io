---
layout: post
title: "Finalizing arbitrary spin coupling"
date: 2011-11-27T21:21:00-08:00
categories:
 - sympy
---

As expected, my work with Sympy slowed drastically once school started, but
nevertheless, I have found enough time to polish off the coupling of arbitrary
number of spin spaces that I started over the summer. I'll probably wait until
after school is done (and the initial Google Code-In traffic dies down) before
opening a pull request, but it has neared the state of conclusion, but I will
outline the work done on the branch [here](https://github.com/flacjacket/sympy/tree/multi_coupled).


A notable change from the summer is the coupling and uncoupling code is now
_much_ cleaner. The old methods used messy `while True` loops which would
increment some parameters and check if some end condition was reached, which I
found very unsatisfactory and open to some weird use case throwing it into
complete disarray. The new methods utilize the notion that any coupling or
uncoupling will occur such that there is a well defined change in either the j
(in the case of coupling) or m (in the case of uncoupling) values from their
maximal values, and this change can be applied over the (un)couplings in the
same way you can distribute n balls in m boxes, then it is just matching an
integer to a given state and check that the given state is physically feasible.

In addition, I have added all necessary documentation for the new functionality
and fixed a few other minor issues with other parts of the new code. I may yet
change some of the handling of the j_coupling parameter, but I will reevaluate
that when I have more time to look at the code after I finish the semester.

The passing of quantum numbers to define the couplings and un-couplings is
still quite verbose, but I see no better way of passing the parameters,
hopefully in review someone will see a better way of defining states and
couplings.
