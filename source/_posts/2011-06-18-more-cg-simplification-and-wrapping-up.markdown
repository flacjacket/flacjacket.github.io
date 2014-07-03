---
layout: post
title: "More CG simplification and wrapping up x/y/z spin bases"
date: 2011-06-18T08:17:00-07:00
categories:
 - sympy
 - GSoC
---

For the first part of this last week, I continued on my work to get sums of
Clebsch-Gordan coefficients to simplify. Using the same general logic that I
outlined in the last blog entry, besides general cleaning up of the code, most
of the work at the beginning of the week was spent on trying to develop a
function that could check an expression for CG coefficients matching a set of
conditions.

The rationale behind trying to write such a method is that it would make it
much easier to identify the times where symmetries could be utilized. With
such a method, the process of checking for CG coefficients could be done in a
single function and the logic for implementing CG symmetries could be handled
in this one function. The current method uses lists of tuples to specify the
conditions on CG coefficients. For example, if the j1 value of a CG coefficient
needed to be =0, you could pass the tuple ("j1",0), or if the m1 and m3 values
match ("m1","m3"). All the conditions for each CG coefficient are combined into
a single tuple. The current snag with simplifications of sums of products of CG
coefficients. For example:
$$ \sum\_{\alpha,\beta} C\_{\alpha\beta}^{c\gamma} C\_{\alpha\beta}^{c'\gamma'}
= \delta\_{cc'} \delta\_{\gamma\gamma'} $$

While the current method would be able to check for specific values on the CG
coefficients, I have yet to come up with a good way to check that the m1 and m2
values are the same when they can take any value, as in this example. As it
stands, this code still seems like quite a hack and will need some work before
it is good to go.

What is left with this part of the project is:

- Getting simplification to work with sums of products of terms (as in the example above)
- Applying CG symmetries to perform simplifications
- Simplification of symbolic CG sums
- Fixing up the printing of CG terms
- Final testing/documentation

This part of the project has unfortunately fallen behind the preliminary
schedule by a bit, as it was due to be finished up last week. I'll outline what
I'm currently working on finish up next, but hopefully I can finish the CG
stuff ASAP so I can move on to working on the spin stuff which is the true meat
of the project and try to get back on schedule.

After meeting with my project mentor, Ondrej, on Wednesday, it was decided that
the focus would shift to finishing up the work I'd started on x/y/z spin bases
and representation of spin states that I'd started before GSoC had officially
started.

The first order of business was identifying an error in the Wigner small-d
function, which is used extensively in the changing of spin bases. With Ondrej
noting that the small-d function was defined only on a small interval and then
me discovering the bug in the Rotation.d method, we were able to address this.
However, no sooner had this been done than Ondrej is able to work out a better
equation for the small-d function, which will likely replace the current
implementation.

Other than this, most of the work this week on the x/y/z basis representation
was in documentation, testing and generally cleaning up the code to be pulled.
The current pull request (my first work to be submitted since the start of
GSoC) is still open [here](https://github.com/sympy/sympy/pull/431).  While
this pull integrates the current work on basis representation, after this pull
there is still some work that will need to be done testing both the Wigner
small-d and the D functions, for both symbolic and numerical values, and
ensuring they return the correct results. Because the representation code
relies so heavily on these functions, it is imperative that these functions
evaluate properly. Once these are fully tested, there will also likely need to
be more tests to ensure all the representation code returns the right values
for as many odd cases as would be necessary to test. Hopefully I can finish
this up soon and move on to other work that still needs to be done.
