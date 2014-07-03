---
layout: post
title: "Getting coupled_spin merged"
date: 2011-08-12T18:50:00-07:00
categories:
 - sympy
 - GSoC
---

The biggest development this week was working out what is needed to get the
coupled_spin which implements spin coupling merged back into master. There were
some things to clean up with non-spin modules and a few minor things to
address, but in cleaning this up, there will be some big changes to the way
spin coupling works. First, with respect to things that have been implemented,
rewrite and represent will no longer handle the coupling and uncoupling of
states. To do coupling and uncoupling, instead, a couple and uncouple method
will be created to handle the coupling and uncoupling of states. In addition,
coupled states will now be represented by new classes, J?KetCoupled for the
Cartesian directions. These will be returned by rewrite when a TensorProduct is
coupled and will return the proper vector for the coupled space when it is
represented and can be uncoupled when an uncoupled operator acts on it.

Most of these new changes have been implemented to varying degrees. There is
some functionality lacking, but much of what remains for this is to implement
tests for the new functions and make sure everything is working properly.

The coupling of arbitrary number of spin spaces had made slow progress due to
some ambiguity when coupled states were created using normal states, but with
the new Coupled classes, specifying the coupling should be possible, thus
making the computations easier.
