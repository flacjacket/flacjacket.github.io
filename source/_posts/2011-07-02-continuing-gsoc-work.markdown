---
layout: post
title: "Continuing GSoC work"
date: 2011-07-02T10:27:00-07:00
categories:
 - sympy
 - GSoC
---

This last week, I have made progress on my project working on laying the base
work for the spin states and in reimplementing logic in the `cg_simp` method
for Clebsch-Gordan coefficients.

First, I have started the work on the implementation of coupled/uncoupled spin
states. Currently, this is implemented by adding a `coupled` property to the
spin states. This can be set to True for coupled, False for uncoupled or left
as None for other states. As this evolves, I will move to having uncoupled
product states be represented by a TensorProduct of two spin states. The next
key will be establishing represent and rewrite logic for these spin states.
Part of this will be figuring out how exactly these methods will work and what
they will return. Namely, the represent method, noting that when representing
an uncoupled state as a coupled state, it returns states with multiple j
values, which under the current logic, would return matrices of different
dimension. Also, we will have to determine what represent will do to uncoupled
tensor product spin states. This next week, I will likely rebase this branch
against the CG branch so I can start using the Clebsch-Gordan coefficients to
implement these functions as the CG pull is finalized.

With the Clebsch-Gordan coefficients, this last week I was able to get the
simplification of symbolic Sum objects working. I did this using the pattern
matching built into sympy with Wild and .match. The final step with this should
be to rework the logic of `_cg_simp_add` to make it easier to add in additional
symmetries.
