---
layout: post
title: "Finishing GSoC"
date: 2011-08-19T21:37:00-07:00
categories:
 - sympy
 - GSoC
---

So this is the last week of the GSoC program. I'll be writing up a full report
on what I've done over the summer
[here](https://github.com/sympy/sympy/wiki/GSoC-2011-Report-Sean-Vig) and it
will be updated over this next week. This blog post will be recapping this last
week of progress and looking forward past the GSoC.

The main thing to report with this last week was the finishing the work on the
spin coupling work that was laid out last week and the writing of the code for
Coupled spin states, the last pull request I'll get in during the GSoC project
is currently open and should only need a last bit of code review to get pulled.

The main thing now is moving beyond the work that will be done during the GSoC
project. While I'll be starting classes this next week and I have my qual the
next week, so work will definitely slow down. However, this last week, I worked
on the multi_coupling branch, which takes the coupling work that is in the
current pull and expands it to allow for an arbitrary number of spin bases. The
first thing to implement with this was a means of representing the coupling
between the spin bases, since the order in which spaces are coupled matters. To
do this, I added a jcoupling option to the functions that deal with coupled
states. It currently seems pretty messy, but I'm not sure of a better way to do
it, as coupling multiple spaces will just pick up a bunch of additional quantum
numbers that need to be represented somehow. Basically, this parameter is
passed as a list of lists, where each element of the outermost list represents
a coupling between two spin spaces. These inner lists have 3 elements, 2 giving
the number of the space that is being coupled and the third being the j value
of these spaces coupled together.  For example, if we wanted to represent a
state $|j,m,j_1,j_2,(j_{12}),j_3\rangle$, the jcoupling would be `( (1,2,j12),
)`. If this option is not set, then the methods default to coupling the spaces
in numerical order, i.e. 1 and 2, then 1,2 and 3, etc.  Using this, I have been
able to rewrite the uncouple code. The results do not yet have tests, and I'll
definitely need to do some calculations by hand to make sure this is working
properly, but looking at it, I am pretty confident in the results, tho the code
could use some cleaning up.

Moving forward from this would be to get the couple method working with
arbitrary spin spaces and run through all of the functions that deal with spin
coupling and make sure nothing is still hard coded to use two spin bases. Other
than that, the project that I'd set out to work on has been basically
completed. I'll continue to work with and develop sympy when I have some spare
and hopefully continue to add features and functionality to the quantum module.
