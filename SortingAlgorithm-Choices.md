Sorting Algorithms - Choices
============================

We all know about the standard comparison based sorting algorithms and their time/space complexity. 
Algorithms like bubble sort, insertion sort, selection sort, quick sort, merge sort, Heap sort operate with a asymptotic lower bound of O(n log n).
Also, other unconventional sorting algorithms like Bucket Sort, Counting Sort, Radix Sort run in O(n)

We will not talk about implementation details and complexities of these algorithms. 
Here we will discuss about various situation and choosing best algorithm for them.

- Array/List is nearly sorted - Insertion sort
- Arrays with mostly duplicated elements - Counting sort, Bucket sort
- Sorting with less write operation (flash devices) - Selection sort
- Data is really huge (Cannot fit in memory) - External Merge sort
- Need top K sorted - Modified Heap sort
- Sorting Linked list (of big structures) - Merge sort
- In general - Quick sort


## Other Sources:

- http://cs.stackexchange.com/questions/3/why-is-quicksort-better-than-other-sorting-algorithms-in-practice
- http://www.sorting-algorithms.com/
- http://en.wikipedia.org/wiki/Sorting_algorithm
- http://www.cprogramming.com/tutorial/computersciencetheory/sortcomp.html
