---
layout: default
title: "Lecture 13: Big-O"
---

You may also refer to the [course notes](../notes/analysisOfAlgorithms.html).

Big-O example problems
======================

First problem
-------------

In the following method, let the problem size *N* be **rowsCols**, which is the number of rows and columns in the square two-dimensional array **matrix**.

{% highlight java %}
public static boolean isUpperTriangular(double[][] matrix, int rowsCols) {
    for (int j = 1; j < rowsCols; j++) {
        for (int i = 0; i < j; i++) {
            if (matrix[j][i] != 0.0) {
                return false;
            }
        }
    }
    return true;
}
{% endhighlight %}

As a function of the problem size *N*, what is the big-O upper bound on the worst-case running time of this method?

Also: would our answer be different if *N* was the number of *elements* in **matrix**?

Second problem
--------------

Assume that, in the following problem, **a** and **b** are both square two-dimensional arrays (same number of rows and columns). Let the problem size *N* be the number of rows and columns.

{% highlight java %}
public static double[][] matrixMult(double[][] a, double[][] b) {
    if (a[0].length != b.length) {
        throw new IllegalArgumentException();
    }

    int resultRows = a.length;
    int resultCols = b[0].length;

    double[][] result = new double[resultRows][resultCols];
    for (int j = 0; j < resultRows; j++) {
        for (int i = 0; i < resultCols; i++) {
            // compute dot product of row j in a and col i in b
            double sum = 0;
            for (int k = 0; k < b.length; k++) {
                sum += a[j][k] * b[k][i];
            }
            result[j][i] = sum;
        }
    }

    return result;
}
{% endhighlight %}

As a function of the problem size *N*, what is the big-O upper bound on the worst-case running time of this method?

Again: would the answer be different if *N* was the number of elements in the two arrays?

Third problem
-------------

Assume that, in the following algorithm, the problem size *N* is the number of elements in the array.

{% highlight java %}
// Return the index of the element of the array which is equal to
// searchVal.  Returns -1 if the array does not contain
// any element equal to searchVal.
// Important: the array must be in sorted order for
// this algorithm to work.
public static<E extends Comparable<E>>
int binarySearch(E[] arr, E searchVal) {
    int min = 0, max = arr.length;

    while (min < max) {
        int mid = min + (max-min)/2;

        int cmp = arr[mid].compareTo(searchVal);

        if (cmp == 0) {
            return mid;
        } else if (cmp < 0) {
            max = mid;
        } else {
            min = mid + 1;
        }
    }

    return -1;
}
{% endhighlight %}

As a function of the problem size *N*, what is the big-O upper bound on the worst-case running time of this method?
