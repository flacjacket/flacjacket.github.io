---
layout: post
title: "Improving rewrite and represent for coupled/uncoupled states"
date: 2011-07-22T17:30:00-07:00
categories:
 - sympy
 - GSoC
---

This last week, most of the coding I have done has been working on getting
represent working properly for coupled and uncoupled states. After doing a
quick double check on what the basis vectors of a coupled or uncoupled state
would be, I was able to get this code in. Tests for the represent logic will
still need to be added, but so far it seems to be working properly.

In addition, I modified the rewrite logic to implement the represent method.
This way all of the coupling and uncoupling logic is taken care of by
represent, just as the represent method also takes care of all rotations of
coordinate bases. To simplify the rewrite logic, I also implemented a
vect_to_state, which returns a linear combination of states given any state
vector when provided with the appropriate parameters, to specify coupled or
uncoupled and what the j1 and j2 parameters are.


In addition to this work, I also wrote up the shell of the class that would
handle tensor products of operators. However, in its current state, it doesn't
function as one would expect, as the `_apply_operator_*` methods are not being
called by qapply. This, in addition to noting that there is very little logic
that is in the TensorProductState class has been making me think I can move
most of the logic for states and operators that are uncoupled out of the spin
class, implementing it instead in places like qapply and represent.  The only
trick would be the uncoupled$\rightarrow$coupled logic, which is just about the only
bit of logic that the TensorProductState class has that couldn't necessarily be
generalized, and the loss of the j1/j2/m1/m2 properties. I will be trying to do
this in the coming week, which will in turn fix the problems I am having with
getting tensor products of states to work.
