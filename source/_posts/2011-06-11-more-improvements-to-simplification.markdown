---
layout: post
title: "More improvements to the simplification method"
date: 2011-06-11T03:59:00-07:00
categories:
 - sympy
 - GSoC
---

I was out of town for the beginning of this week, so I don't have as much to
report, nevertheless in the last few days, I have made some good improvements
to the cg_simp method, allowing it to simplify cases other than just the simple
sums, tho it still only handles the same case as before involving the sum of .
While it is entirely possible I'm doing something stupid in performing all the
checks, as far as I can tell, it works for the given case. Because the code
itself is not yet very clear and it is not always straightforward what is
happening, I'll explain what I have implemented.

First note that for the simplifications that will be made, it is required to
have a sum of terms. The first for loop in the method constructs two lists
`cg_part` and `other_part`, the former consisting of all terms of the sum
containing a CG coefficient and the latter the other terms.

Next, we iterate over the list `cg_part`. The number of CG coefficients is
computed, which determines which simplifications can be made (currently, the
only implemented simplification uses terms with 1 CG coefficient in each sum
term).  Those terms with the proper number of CG coefficients are then
considered for the simplification. The way this will work is: based on the
properties of the CG coefficient in the term, it will search the rest of the
list for other terms that can be used in the simplification, and if all the
terms exist, will simplify the terms.

Turning to the implementation, when iterating through the list, the first thing
to do is determine the properties of the CG coefficient terms, that is to
extract from the term in the sum the CG coefficient itself and the numerical
leading terms. Here it is also noted the sign of these numerical terms.

Next, the rest of the list is checked to see if a simplification can be made
using the determined term. To keep track of this, a list, `cg_index`, is
initialized with `False` as the element of the list. In checking the later
terms, we preform a similar decomposition as with the first term, that is
splitting up the CG coefficient from the other components of the term,
determining the CG coefficient, the leading terms and the sign of the terms. If
the properties of these are correct, then the corresponding element of
`cg_index` is updated with a tuple `(term, cg, coeff)` where term is the term
in `cg_part` (so this element can be removed later), the CG coefficient and the
leading numerical coefficient of the coefficient.

Now, if all the elements of `cg_index` are changed, the simplification is
preformed. When this happens, first we find the minimum coefficient of the
chosen CG coefficients, which determines the number of times we can apply the
simplification. Then the replacing happens; for each element in `cg_index`
(which is a tuple) the first element of the tuple is popped off `cg_part`,
then, if the term is not eliminated by the simplification, a new term is
created and added to `cg_part`, and finally a constant is added to
`other_part`, completing the simplification.

Looking at the code, this method is very straightforward, but should be robust
and scalable for treating cases of sums with numerical leading coefficients,
and now that the i's have been dotted and the t's have been crossed on testing
this method, implementing new cases should come rapidly in the next couple
days.  However, one place where this will still need some work is in
implementing symbolic simplification, both in dealing with symbolic leading
terms on the CG coefficients and symbolic CG coefficients themselves. This will
take a bit of thought and likely a bit of help to complete, but this is one
thing I hope to work on in the next week. In addition, as the simplification
comes into place, I'll work on polishing out the last of the details to get the
classes for the Wigner3j/CG coefficients working properly.
