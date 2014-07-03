---
layout: post
title: "Transitioning to spin states"
date: 2011-06-25T02:18:00-07:00
categories:
 - sympy
 - GSoC
---

This last week, the first thing that was taken care of was finishing the x/y/z
spin basis representation. Having fixed the Wigner small d-function in the
Rotation class, the tests for this were put into the pull request and the pull
was merged into the sympy master, making this my first pull request since
starting GSoC. There is still some changes that will come for the Rotation
class, namely the creation of a symbolic WignerD class which is returned by the
current Rotation.D and Rotation.d functions, but that will be dealt with in a
later pull request.

With the x/y/z basis stuff finally out of the way, I moved back to getting the
Glebsch-Gordan coefficient/Wigner-3j symbols to a state where they can be
pulled. Having fallen behind in getting the CG coefficient simplification to a
suitable state and with the work on the x/y/z spin basis pushing the timeline
back even further, the current goal is to merge what I have so far and move on
to the coupled spin states. What I have so far is the classes for the Wigner-3j
symbols and the Clebsch-Gordan coefficients which can be manipulated
symbolically and evaluated, and a very rough version of the cg_simp method.
Currently, this method can handle 3 numerical simplification, however the code
is still messy and having more cases would be ideal. That said, in an effort to
make sure the key parts of this GSoC project are covered, I'll be moving into
writing the coupled spin states.

For the spin states portion of this project, I will develop a means of writing
coupled and uncoupled spin states. The uncoupled product basis states will be
written using the TensorProduct, which is in the current quantum module; each
of the states in the tensor product will be states as they are currently
implemented. To represent coupled basis spin states, the current spin states
will be modified to included a coupled parameter. This value stores the J_i's
of the spin spaces which are being coupled. In addition to the spin states
being implemented, methods will be written to utilize the CG coefficients
mentioned earlier to go between coupled and uncoupled basis representation.
Look for more next week as this code is fleshed out.
