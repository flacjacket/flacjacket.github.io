---
layout: post
title: "Finishing current coupled spin work"
date: 2011-07-30T01:45:00-07:00
categories:
 - sympy
 - GSoC
---

This last week I made some good headway towards finishing up the coupled spin
state work for the coupling of two spin spaces. The decision was made that
spin states should not contain any information as to their coupling, which
greatly simplifies not only the code, but also the allowable cases when it
comes doing things such as applying operators, rewriting, etc. As such, I am
very close to finalizing this stage in the coupled spin work. I will try to fix
up the implementation for some symbolic cases that should be doable under the
current implementation, but all the current code has tests implemented and
docstrings in place, so a pull request will be coming up shortly.

With this stage finishing, I will be moving on to generalizing the current
implementation to coupling between more than two spin spaces. I will first need
to expand cg.py to include Wigner-6j/9j/etc symbols to describe the coupling
between these additional spaces. The logic for spin states will need to be
reworked as well, not only to implement these new terms for coupling additional
spin spaces, but most of the logic will need to be reworked to allow for an
arbitrary number of coupled spin spaces.

While the change to get rid of what would be considered a coupled spin state
(that is a state where the state has defined the coupled spaces) does simplify
the current implementation, it does limit what can be done. For example, an
uncoupled operator could not be applied to a coupled state, as the coupled
states would need to be uncoupled, which is only possible if the j values of
the coupled states is known. However it was suggested by Brian that a new class
be created to deal with coupled states in this sense. Time permitting, I will
begin to look at the possibility of implementing such a feature into the
current spin framework.
