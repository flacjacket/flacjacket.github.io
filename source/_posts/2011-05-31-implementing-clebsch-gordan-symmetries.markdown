---
layout: post
title: "Implementing Clebsch-Gordan symmetries and sum properties"
date: 2011-05-31T06:51:00-07:00
categories:
 - sympy
 - GSoC
---

In this first week of the GSoC project, I focused on implementing methods that
would simplify terms with Clebsch-Gordan coefficients. This still has a long
was to go, but I will outline what I have done so far.

The first step was implementing means of dealing with sums of single
coefficients. This would hopefully look something like:
``` python
>>> Sum(GC(a, alpha, 0, 0, a, alpha), (alpha, -a, a+1)
2*a+1
```
The first implementation of this used an indexing system that was able to index
single coefficients, which could then be processed. This allowed the
simplification function to act properly in simple numerical cases, so it could
do things like:
``` python
>>> cg_simp(CG(1,-1,0,0,1,-1)+CG(1,0,0,0,1,0)+CG(1,1,0,0,1,1)+a)
a+3
```
The problem with this implementation is doing something as simple as having one
of the terms have a constant coefficient would break it. In addition, there
would be no clear way to extend this to sums involving products of multiple
Clebsch-Gordan coefficients.

To deal with this, I started working a solution that could deal with having
constant coefficients and products of coefficients. Currently implemented is
method which creates list of tuples containing information about the
Clebsch-Gordan coefficients and the leading coefficients of the Clebsch-Gordan
coefficients. Currently, the only implemented logic is only able to deal with
the case in that could be dealt with in the previous implementation, however,
this should be able to expand to encompass more exotic cases.

Another thing that was touched on this last week was treating symmetries. These
are quite simple to implement, as they need only return new Clebsch-Gordan
coefficients in place of old ones, just with the parameters changed in
correspondence with the symmetry operation. The key will be using these
symmetries to help in simplifying terms. This will be based on the development
of better logic in the simplification method and the implementation of some
means of determining if these symmetries can be used to apply some property of
the Clebsch-Gordan coefficients that can simplify the expression.

I will be out of town this next week on a vacation, and will not be able to get
work in, but I will continue working on this when I return, with the intention
of getting it to a state that can be pushed within the next couple weeks.
