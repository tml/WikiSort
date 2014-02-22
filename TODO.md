To do
=================

This algorithm would benefit from the following addition:

    #define bzSort(array, array_count, compare) { \
       __typeof__(array[0]) temp, *bzSort_array = array; const long bzSort_count = array_count; \
       uint64_t i, ascending = 0, descending = 0; \
       for (i = 1; i < bzSort_count; i++) if (compare(bzSort_array[i], bzSort_array[i - 1]) >= 0) ascending++; else descending++; \
       if (descending > ascending) { reverse(bzSort_array); swap(ascending, descending); } \
       if (bzSort_count < 32) { \
          /* insertion sort the array */ \
          [...] \
       } else if (descending > 0) { \

However, a naïve array reverse operation would invalidate the stability of the algorithm:

&nbsp;&nbsp;&nbsp;[5 a] [5 b] [4 c]  <--->  [4 c] <b>[5 b] [5 a]</b>

A more-intelligent reversal is needed before this can be added to the algorithm.

The original version included a full test suite for generating lists with various properties (random, mostly ascending, mostly descending, all equivalent, in order, reverse order, etc. etc.) and timing and verifying the accuracy, but it was left out from this version as it uses a large number of dependencies. A self-contained benchmark and test tool would be very useful.