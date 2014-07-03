---
layout: post
title: "Official GSoC start"
date: 2011-05-24T22:37:00-07:00
categories:
 - sympy
 - GSoC
---

This week marks the official start of the Google Summer of Code. While I
started getting my feet wet last week after finishing the last of my finals and
grading, the bulk of the work has just started turning out. I'll quick cover
what I have from this last week and what I'm looking to get working this week.

Before the start, I worked out expanding the functionality of the currently
implemented x/y/z bases, which work I have
[here](https://github.com/flacjacket/sympy/tree/xyz_bases). The previous
implementation only allowed for evaluating inner products between states in the
same basis and representing the states in the Jz basis and then only with j=1/2
states. Using the Wigner D-function, implemented with the Rotation class, I
implemented represent to go between the x/y/z bases for any j values. Both
`_eval_innerproduct` and `_rewrite_as` were then created to take advantage of the
represent function to extend the functionality of the inner product and to
implement rewrite between any bases and any arbitrary j values.

This seems like this is some documentation and tests away from being pushed,
but there is something buggy with the Rotation.d function, implementing the
Wigner small d-matrix. I noticed when trying to do
``` python
>>> qapply(JzBra(1,1)*JzKet(1,1).rewrite('Jx')
```
and I wasn't getting the right answer. As it turns out, the Rotation.d
function, which uses Varshalovich 4.3.2 Eq 7, does not give the right answer
for `Rotation.d(1,1,0,-pi/2)` or `Rotation.d(1,0,1,pi/2)`. Namely, there is
something wrong with the equation that doesn't change the sign of the matrix
element when reversing the sign of the beta Euler angle. Running all four
differential representations given by Varshalovich for the small d matrix, Eq
7-10, give the wrong result, so the derivations of these will need to be
checked to fix this. I have a bug report up
[here](http://code.google.com/p/sympy/issues/detail?id=2423).

As for what I will be implementing this week, I already have the basics of the
Wigner3j and CG class implemented, the work for this going up
[here](https://github.com/flacjacket/sympy/tree/cg_coeff). This includes
creating the objects, _some_ of the printing functionality and numerical
evaluation of the elements using the wigner.py functions. The meat of the class
that I'm currently working on is the `cg_simp` function, which will simplify
expressions of Clebsch-Gordan coefficients. I currently have one case working,
that is `Sum(CG(a,alpha,0,0,a,alpha),(alpha,-a,a)) == 2a+1` which is
Varshalovich 8.7.1 Eq 1. There are still some things to smooth out with the
implementation, but I should have that worked out a bit better, in addition to
some more simplifications by the end of the week.

That's all I have for now, watch for updates within the week as to what I've
gotten done and what I have yet to do.
