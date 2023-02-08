# Divide and Conquer

## Learning Goals

You may recall learning about divide and conquer algorithms such as Quick Sort, and Merge Sort, Binary Search. This lesson is intended to serve as a refresher for the divide and conquer approach.

This lesson requires prior knowledge about the divide and conquer technique and you are encouraged to re-read the Divide and Conquer lesson under the Algorithmic Strategies topic provided during classroom if you require more details about any of the review topics mentioned here. Any new topics covered in this lesson will be clearly indicated.

## Overview

As a reminder, **Divide and Conquer** is an approach to problem solving that breaks down a large problem into multiple, smaller subproblems. We combine the results of those subproblems to solve the original problem.

When we write a divide-and-conquer solution we can follow these steps:

1. Break the problem into subproblems of the same type
1. Recursively solve the subproblems
1. Combine the solved subproblems to solve the larger problem

## Algorithms Previously Covered

### Example: QuickSort

QuickSort is an algorithm which takes a divide-and-conquer approach to sorting an array by using the following steps:

1. If the array is only one element or empty, we are done, the array is sorted.
1. Pick an element from the array as the _pivot_.
1. Move all elements smaller than the pivot to the left and all elements larger than the pivot to the right. Note that the pivot is now in the correct index. Picking a pivot and rearranging the elements is referred to as _partitioning_.
1. Perform QuickSort on the left and right sides of the pivot.

### Example: Merge Sort

Merge sort is another divide-and-conquer algorithm. It involves the following three stages:

1. _Divide_ the array into two subarrays at each step until each subarray is of size one.
2. _Sort_ each subarray with the merge sort algorithm. (An array of size one is trivially sorted.)
3. _Merge_ the subarrays into one array by combining two subarrays into one at each step.

### Example: Binary Search (Decrease-and-Conquer)

Binary search can be considered a decrease-and-conquer algorithm because it decreases the size of the array by half with each step. No matter how large the original array was, at each step we'll be able to discard half the remaining data from consideration! The half-sized array will then be analyzed with the same step as the full-sized array.

Binary search is technically not considered a divide-and-conquer algorithm but instead a decrease-and-conquer algorithm because divide-and-conquer algorithms typically have *two or more* subproblems which are generated from the main problem. In contrast, the binary search algorithm decreases to one sub-problem.

Here's a description of the binary search algorithm:

1. Starting with a sorted array, we check whether it contains a particular value by comparing the search value with the element in the middle of the array.
1. If we find the value we return the position where it was found.
1. If we don't find the value, we determine whether it would be in the left or right half of the array by seeing whether it is smaller or larger than the middle element. Remember, we can make this decision because _we assume the array is sorted!_ Then we perform a binary search on the selected half.
1. If at any point, we end up with an empty range, we know the value was not in the array, and we can return a result indicating the value was not found, such as `None`. Other variations of binary search may return the index of where the value _should_ have been, but as a negative value to indicate that it was missing.
1. Each recursion divides the array in half and performs the binary search on a smaller subproblem.

## Binary Search in the Wild

### Binary Search: A modified approach

The following material serves as an addendum to the Divide and Conquer lesson reviewed during class. 

Binary search can be used to solve many problems related to searching through sorted data. The following problem offers an opportunity to use the binary search algorithm using a modified approach.

```
Suppose you are given a sorted array of non-negative distinct integers. 
You are tasked with finding the smallest missing non-negative element inside of the array.

If present, the array should start with the integer 0.

For example:
If the array is [0, 1, 2, 6, 9, 11, 15], the smallest missing element is 3.

If the array is [1, 2, 3, 4, 5], the smallest missing element is 0.
```

This problem can be solved in O(n) time using a linear search to find the first index containing an element that does not match its value. However, this approach does not take advantage of the fact the input is sorted.

We can instead use a modified binary search algorithm to solve the problem in O(log(n)) time.

Spend *no more than 15 minutes* writing a modified binary search solution to the problem detailed above.

<details style="max-width: 700px; margin: auto;">
  <summary>Click here to see a sample solution</summary>
    ```py
    def findSmallestMissingNum(nums, left = None, right = None):
        # initialize right and left
        if left is None and right is None:
            (left, right) = (0, len(nums) - 1)
        
        # base case
        if left > right:
            return left

        # calculate the middle index
        mid = (left + right) // 2

        # if the mid index matches with its value, then the mismatch must lie on the right half
        if nums[mid] == mid:
            return findSmallestMissingNum(nums, mid + 1, right)
        # otherwise, the mismatch must lie on the right half
        else:
            return findSmallestMissingNum(nums, left, mid - 1)
    ```
</details>

## Check for Understanding

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 645bad5d-af5f-42a9-a7e4-c70412972ab1
* title: Quicksort Weakness

##### !question

Which step in the Quicksort algorithm may cause the algorithm to run in O(N<sup>2</sup>) time?

##### !end-question

##### !options

a| If the array is only one element or empty, we are done, the array is sorted.
b| Pick an element from the array as the pivot.
c| Move all elements smaller than the pivot to the left and all elements larger than the pivot to the right.
d| Perform QuickSort on the left and right sides of the pivot.

##### !end-options

##### !answer

b|

##### !end-answer


##### !explanation

The worst-case time complexity for Quicksort is O(N<sup>2</sup>) because picking the worst pivot (e.g. the smallest or biggest remaining element) for each step will result in one array of size n-1 as opposed to two arrays that are approximately n/2 in length. Therefore, step 2: Pick an element from the array as the pivot, is the step, if incorrectly chosen, that may cause Quicksort to have an O(N<sup>2</sup>) runtime.

##### !end-explanation 

### !end-challenge

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 25522151-56d9-4495-9691-da53700f896e
* title: Binary Search Implementation Detail

##### !question

Which of the following lines in Python can be used to calculate the middle index used in step 1 of Binary Search? Assume the variable `high` stores the upper bound of where we want to search in the array and `low` stores the lower bound for where we want to search in the array.

##### !end-question

##### !options

a| mid = (low - high) * 2
b| mid = (high - low) // 2
c| mid = (high + low) * 2
d| mid = (low + high) // 2

##### !end-options

##### !answer

d|

##### !end-answer

#### !explanation

The answer is (low + high) // 2 because the index calculated using that expression is the index of the middle element. For example, if the lower bound is 2 and the upper bound is 16, the middle element between indices 2 and 16 is the element in index 8. 

#### !end-explanation 

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## Summary

Divide and conquer is an algorithmic strategy which involves breaking down a large problem into easier-to-solve subproblems.

In a divide and conquer solution we break a large problem into one or more smaller subproblems and then use the solution to the subproblems to solve the larger problem.

## Resources

- [Wikipedia: Divide & Conquer](https://en.wikipedia.org/wiki/Divide-and-conquer_algorithm)
- [Daniel Liang's Binary Search Animation](https://yongdanielliang.github.io/animation/web/BinarySearchNew.html)
- [Geeks for Geeks: Python Program for QuickSort](https://www.geeksforgeeks.org/python-program-for-quicksort/)
- [hackerearth: QuickSort Animation](https://www.hackerearth.com/practice/algorithms/sorting/quick-sort/visualize/)
- [Find the smallest missing element from a sorted array](https://www.techiedelight.com/find-smallest-missing-element-sorted-array/)
