---
layout: post
title: "Developing coupled/uncoupled states and operators"
date: 2011-07-16T00:31:00-07:00
categories:
 - sympy
 - GSoC
---

Most of this last week was spent developing coupled and uncoupled states,
beginning to develop how operators will act on these states and writing tests
to ensure the code returns the desired result. This week I finished up writing
the code for expressing states, and the logic for rewriting from one to the
other and back. In addition to this, I implemented the tests which are used for
these rewrites. This mostly finishes up the logic for the coupled/uncoupled
states, there is still the represent logic which may need to be implemented,
tho this will take some looking into to determine what is appropriate and
necessary to implement.

For the operators, using the qapply logic already in place, I have begun to
implement how operators act on coupled and uncoupled states. I have thus far
only implemented logic for coupled operators, that is, for example $J\_z =
J\_{z\_1} + J\_{z_2}$ ($=J\_{z_1} \otimes 1 + 1 \otimes J\_{z_2}$ in an
uncoupled representation). In addition to defining how uncoupled product states
are acted upon by spin operators, I have expanded those already implemented
methods to act on arbitrary states, as they had only previously been defined in
how they act on JzKet's. This was done by defining a basis, such that, with the
now improved rewrite logic, any state can be rewritten into an appropriate
basis for the state and the state in then acted upon by the operator. I have
begun to implement the tests that ensure the implemented logic is valid in all
cases, both numerical and symbolic, tho this is still a work in progress.

The focus for this next week will be continuing the development of the spin
operators, hopefully getting to working with uncoupled spin operators, i.e.
operators given in a tensor product to only act on one of the uncoulped states,
and developing the tests necessary to the implementation of these states. If I
can complete this, I will be closing in on the completion of the coupling of
two spin spaces.
