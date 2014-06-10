---
layout: default
title: "Assignment 6: Big-O"
---

**Due: Tuesday, July 29th by 11:59 PM**

Your Task
=========

Do exercise 5.20 on page 220, *part (a) only*. You just need to analyze each code fragment to find a big-O upper bound on its running time. You do not need to implement or benchmark the code fragments.

Please see me if you have the third edition of the textbook.

For each code fragment, *explain* how you arrived at the big-O upper bound.

For example, for the first code fragment: "the body of the loop executes in constant time, and the loop executes exactly *n* iterations, so the overall running time is O(*n*)".

Hints
=====

Don't forget to drop low order terms and constant factors from your big-O bound.

<div class="callout"> **Important Reminder**: If the problem involves nested loops in which the inner loop is dependent on the outer loop, then you will need to analyze the loops together. Use a series to count the total number of iterations of the body of the inner loop. </div>

Submitting
==========

Save your answers in a **plain text file** or a **PDF file**. Submit to marmoset as **assign06**:

> <https://cs.ycp.edu/marmoset/>

<b><span style="color:red;">Important</span></b>: Do **not** submit a file in any format other than plain text or PDF.

<b><span style="color:red;">Important</span></b>: After you submit your file, download it and check to make sure it is what you intended to submit.

I may assign a grade of 0 for incorrectly submitted assignments.
