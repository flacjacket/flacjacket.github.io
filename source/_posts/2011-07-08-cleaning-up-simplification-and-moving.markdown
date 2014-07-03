---
layout: post
title: "Cleaning up simplification and moving into coupled states"
date: 2011-07-08T19:40:00-07:00
categories:
 - sympy
 - GSoC
---

So, as I stated in my last post, the first thing I dealt with was fixing up the
`_cg_simp_add` method by implementing pattern matching and move the logic for
determining if the simplification can be performed and performing the
simplification out of the `_cg_simp_add` method and developing a system that
can easily be expanded to include additional simplifications. To do this, I
created another method, `_check_cg_simp`, which takes various expression to
determine if the sum can be simplified. Using Wild variables, the method takes
an expression which is matched to the terms of the sum. The method uses a list
to store the terms in the sum which can be simplified, so additional
expressions are used to determine the length of the list and the index of the
items that are matched.  There are also additional parameters to handle the
leading terms and the sign of the terms. There are still some issues with this
method, as when there is more than 1 Clebsch-Gordan coefficient in the sum,
then the leading term cannot be matched on the term.

In addition to the finishing of this component of the Clebsch-Gordan
coefficient simplification, I have started into working on the coupled spin
states and the methods to rewrite them in coupled and uncoupled bases. Coupled
spin states are set by passing j1 and j2 parameters when creating the state,
for example:
``` python
>>>  JzKet(1,0,j1=1,j2=1)
|1,0,j1=1,j2=1>
```

These states can be given in the uncoupled basis using the rewrite method and
passing coupled=False, so:
``` python
>>> JzKet(1,0,j1=1,j2=1).rewrite(Jz, coupled=False)
2**(1/2)*|1,1>x|1,-1>/2-2**(1/2)*|1,-1>x|1,1>/2
```
This can also be done with a normal state and passing j1 and j2
parameters to the rewrite method, as:
``` python
>>> JzKet(1,0).rewrite(Jz, j1=1, j2=1)
2**(1/2)*|1,1>x|1,-1>/2-2**(1/2)*|1,-1>x|1,1>/2
```
How the coupled states will be handled by rewrite still needs to be addressed,
but that will need some thinking and with another GSoC project doing a lot of
changes to the represent function, it may take some coordination to get this
and the TensorProducts of states and operators working.

Note that in the python expressions above, the states are given as uncoupled
states written as tensor products. Uncoupled states will be written as
TensorProduct's of states, which will be extended later to spin operators,
being written in the uncoupled basis as a TensorProduct. I've just started
playing with the uncoupled states and the various methods that will be used to
go from uncoupled to coupled states and I've been putting them in a separate
TensorProductState class, which subclasses TensorProduct, which keeps all the
spin logic separate from the main TensorProduct class, tho this will have to be
expanded to include operators. Developing the logic for these uncoupled spin
states will be the primary focus of this next week of
coding.
