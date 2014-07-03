---
layout: post
title: "Moving beyond first coupling iteration"
date: 2011-08-05T17:00:00-07:00
categories:
 - sympy
 - GSoC
---

In the last week, one of the main things I did was to submit a pull request for
the coupled spin machinery that I have been working on. This pull request can
be seen [here](https://github.com/sympy/sympy/pull/524). This
implements the coupling and uncoupling operations for states and operators and
how these states and operators interact for coupling of two spin states. This
pull still has some kinks to work out and some details to iron out, but should
be finished up soon.

Moving beyond this pull, the rest of this week has been in working on modifying
the coupling methods developed in this pull and making them work for an
arbitrary number of spin spaces. The current idea will be to pass a tuple of j
values which are to be coupled instead of passing j1 and j2 parameters. While
this would work, it would be nice to be able to define how the terms are
coupled, noting that the order of how the spaces are coupled matter in
determining the coefficients and what will be diagonal in the basis of the
coupled states. The current way I am working the coupling is to couple j1 and
j2, then couple this to j3, etc. I have currently changed the all the methods
to accept the tuple of j values, however, the coupling and uncoupling methods
have not been changed to accept arbitrary numbers of spaces. Most of this week
has been thinking and trying to determine a good way to implement this
machinery that scales to arbitrary numbers of spaces. While it is not directly
necessary for dealing with spin states, I will likely also implement
Wigner-6j/9j/12j coefficients in cg.py, which will be very similar to the
Wigner-3j symbols that were implemented with the Clebsch-Gordan coefficients.

While I am starting to work on this final component of my project, it will be a
close call as to whether or not it can get pushed in time to make it in before
the end of the project, which will be in just 2 weeks. The initial coupling
stuff should get in, but this will be a much closer call. That said, I will
definitely see this last part of the project into master.
