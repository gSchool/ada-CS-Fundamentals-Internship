# Sliding Window Technique

## Overview

Within the broader category of dynamic programming, there are further techniques that can help us solve specific types of dynamic programming problems.

One useful strategy is called the **sliding window technique**. The sliding window technique is a strategy used to simplify time and space complexity when solving a problem that asks us to find some subsequence that satisifies a given set of conditions inside of a larger sequence.

## Understanding the Sliding Window Technique

Say we have some sequence of data that we want to examine. We can create a 'window' that allows us to look at some contiguous subsection of the data. Then we iterate through the remainder of the data by adjusting the start and end indices of the subsequence or window.  Each iteration either the start index, end index, or both indices move forward so that we have a  "sliding" subsequences that progresses through the original sequence until we have looked at every part of the original sequence.

![Sliding Window](images/sliding-window.png)

This is called the sliding window technique because it mimics sliding a window open or shut. The section of data we are currently viewing shifts as we slide our window along the sequence.

![Sliding Window with an Array](images/sliding-window-array.png)

We can make our window as small or large as we would like to solve a problem, but we must be interested in looking at contiguous - meaning adjacent and maintaining order - subsections of the sequence. If we are interested in combining non-adjacent sections of the larger sequence into a subsequence, we need to use a different strategy. To accommodate noncontiguous subsequences, we would need to split our window and in most cases it would be difficult to know when we had examined all the subsequences we were interested in.

![Comparing Contiguous and NonContiguous Subsequences](images/contiguous-v-noncontiguous.png)

### When to Apply the Sliding Window Technique
What types of data can the sliding window technique be applied to? When deciding.

#### Contiguous Stream of Data
When determining whether the sliding window technique is an appropriate approach for a given problem, the first thing we want to consider is what type of data we will be looking at. Our input should be a contiguous, linear, and iterable set of data stored such that we can create a window over it.

For example, we could perform the sliding window technique on an array, because we can create a `window` variable that holds some subset of the data using list slicing.

In the example below, the input array is `arr = [4, 3, 12, 4, -1]`

Our window is initally `window = [4, 3, 12]` or `window = [0:2]`. If we use variables to store where the array slice should start and stop, each time we want to slide our window, all we need to do is increment each our start and stop variables by 1. 

![Sliding Window with an Integer Array](images/sliding-window-integer-array.png)

We could do the same thing with a string using string slicing. In fact, most problems that can be will involve either a string or an array. 

It is also possible with some slight adjustments to perform the sliding window technique on a data structure such as a hashmap or a linked list, but accessing and storing values within the window may not be as straightforward because (at least in Python) we cannot slice a dictionary or linked list in the same way that we can a string or an array.

A data structure like a graph would be difficult to using the sliding window technique on, because it is not a linear data structure. How would we place and slide our window? 

#### Contiguous Subset
In order for the sliding window technique to be applicable, the problem must also ask us to find a contiguous subset of the problem.

For example, say you are given an array of integers and asked to find all adjacent pairs of integers in the list that add up to a given sum. This could be solved using the sliding window technique. Our window would be of size two and we can check each adjacent pair by starting the left end of the window at index 0 and shifting our window by one each iteration until the right end of the window is at the last index in the array.

![Sliding Window on Adjacent Pair Sum Problem Animation](./images/sliding-integer-adjacent-pair-sum.gif)


However, if the problem were changed slightly and we were asked to instead find all  pairs of numbers in an array that add up to a given sum, adjacent or not, we could not use the sliding window technique. The elements we want to look at together wouldn't necessarily fit inside of a window.

![Sliding Window on Non-Adjacent Pair Sum Problem Animation](./images/sliding-integer-nonadjacent-pair-sum.gif)

#### Dynamic Programming Problem
Recall that the sliding window technique is used to solve a subset of dynamic programming problems. This means that problems solved with the sliding window technique should be optimization problems that maintain the optimal substructure property **and** have overlapping subproblems. 

The overlapping subproblems can be seen simply by observing the way we slide the window. Observe that when we shift the window in the array below, element 3 from the previous window is also in the new window. 

![Element 3 Shared Between Windows](./images/overlapping-subproblem.png)

To determine whether the problem is composed of optimal substructures, consider whether the optimal overall solution is comprised of the optimal solution for its smallest subproblems for some sample inputs.

Some example questions we could solve with the sliding window technique include:
- [Given an array of integers, find the maximum sum subarray of a given size](https://www.geeksforgeeks.org/find-maximum-minimum-sum-subarray-size-k/)
- [Given an array of 0s and 1s, find the maximum sequence of continuous 1s that can be made by flipping at most k 0s to 1s](https://www.geeksforgeeks.org/find-zeroes-to-be-flipped-so-that-number-of-consecutive-1s-is-maximized/)
- [Given two strings, find the shortest substring in the first string that contains all the characters in the second string](https://leetcode.com/problems/minimum-window-substring/)

As always, there are some edge cases that may seem like sliding window problems but have other, more optimal solutions. However, in general, this is a good place to start. We will discuss at least one edge case in further detail later on in the lesson.

### Static Sliding Window

Now that we understand what the sliding window technique is, let's apply the technique to an example problem. 

#### Maximum Subarray of Size K
Consider the following problem:

*Given an array of integers `numbers` and an integer `k`, return the sum of the minimum sum subarray of size `k`.*

In other words, given the array of integers `numbers`, calculate the minimum sum of `k` consecutive elements in the array.

#### Brute Force Solution
Before we jump into solving this problem with the sliding window technique, let's look at how we could solve the problem without this new technique. We might develop the following solution: 
```py
def min_sum(numbers, k):

    # initially overestimate what the minimum sum of any k consecutive elements in the array is 
    min_sum = float('inf')

    nums_len = len(numbers)

    for i in range(nums_len - k + 1):
        current_sum = 0
        for j in range(k):
            current_sum = current_sum + numbers[i + j]
        
        min_sum = min(current_sum, min_sum)

    return min_sum


```
### Dynamic Sliding Window

We can modify the sliding window technique by shifting the left and right edges of our windows at different rates. 

#### Minimum Sublist
Say we are asked to solve the following problem:

*Write a function called `minimum_sub_list_length` that takes in a list of positive 
numbers and a positive integer.*  

*It should return the minimum length of a contiguous sublist of the given input 
list which adds up to the given integer.*

#### Brute Force Solution

Before we jump into solving this problem with the sliding window technique, let's look at how we could solve the problem without this new technique. We might develop the following solution: 

  ```py
  def minimum_sub_list_length(numbers, target):
    '''
    INPUT: list of positive numbers, and target a positive integer
    OUTPUT: the minimal length of a contiguous sublist of the given input list which adds up to the given integer.
    Return the length of the smallest contiguous sublist which adds up to the given integer or 
    return None if there is no such sublist.
    '''
    # if the target sum is 0, we can reach the sum simply by not adding any elements to the sublist
    if target == 0:
        # so we return that the length of the minimum sublist is 0 (an empty list)
        return 0
    
    # initialize the minimum length to be the length of the initial length plus one
    min_length = len(numbers) + 1
  
    for index in range(0, len(numbers)):
        current_sum = numbers[index]
        current_index = index + 1
        while current_index < len(numbers) and \
                current_sum + numbers[current_index] <= target:
            current_sum += numbers[current_index]
            current_index += 1
        
        if current_sum == target and current_index - index < min_length:
            min_length = current_index - index
    
    if min_length == len(numbers) + 1:
        return None
    
    return min_length
  ```

This solution works and is a relatively direct straight forward approach. This is often called a brute force solution. Notice the nested for loops. In the worst case, this solution would have time complexity of O(n^2). 

## Simplify/Refactor

The first big challenge in software development is to **produce working code**. After code is working however the time comes to simplify or refactor (improve) the solution.

In the sample solution above we are using a nested loop and the loop repeatably traverses the list. Our code is not time efficient because we examine the same elements of the list repeatedly.

We are only interested in contiguous sublists, elements have to be next to one another. This means we can apply a technique called a [sliding window](https://www.geeksforgeeks.org/window-sliding-technique/).   

In this technique we slide a "window" across the list and track the sum of the elements within the window.  If the sum of the elements in the window is equal to the target, we have found a contiguous sublist.  

The image below illustrates the sliding window technique.

![Sliding Window Example](images/problem-solving__sliding-window.gif)

*Fig. Sliding Window*

### Implementing Our Refactor

In our refactor we can start by creating a window of size 1 from index 0 to index 1.  So our window's `start_index` is `0` and `end_index` is `1`. Our current sum then is the value of the 1st element of the list.

We track the following values:

* `start_index` - Where our window starts
* `end_index` - Where our window ends
* `current_sum` - The sum of the elements in the current window
* `min_length` - The length of the smallest contiguous sublist found thus far.

Then we can repeat this algorithm:

1.  If the current sum is equal to the target, we have found a contiguous sublist which adds up to target, and if it is the smallest contiguous sublist we have found so far, we update the minimum length.
      * We can also advance the window by incrementing the `start_index` by one.
1.  If the current sum is greater than or equal to the target we can decrease the window size by adding one to the start index of the window.
1.  If the current sum is less than the target we can increase the window size by adding one to the end index of the window.
1.  We will repeat this algorithm until the end index has passed the end of the list.

**Practice**:  Go back to the exercise above and try to implement the refactor.  Spend no more than 15 minutes on it.

<details style="max-width: 700px; margin: auto;">
  <summary>Click here to see a sample solution</summary>

  ```py
  def minimum_sub_list_length(numbers, target):
    '''
    INPUT: list of positive numbers, and target a positive integer
    OUTPUT: the minimal length of a contiguous sublist of the given input list which adds up to the given integer.
    Return the length of the smallest contiguous sublist which adds up to the given integer or 
    return None if there is no such sublist.
    '''
    if len(numbers) == 0:
        return None
          
    start_index = 0
    end_index = 1
    current_sum = numbers[0]
    min_length_sublist = len(numbers) + 1
  
    while end_index < len(numbers) + 1:

        if current_sum == target:
            min_length_sublist = min(min_length_sublist, end_index - start_index)

            current_sum -= numbers[start_index]
            start_index += 1

        elif current_sum < target:
            if end_index < len(numbers):
                current_sum += numbers[end_index]
            end_index += 1
            
        elif current_sum > target:
            current_sum -= numbers[start_index]
            start_index += 1

    if min_length_sublist == len(numbers) + 1:
        return None
    return min_length_sublist
  ```
</details>

This solution now makes only one pass through the list, meaning as the input array grows, the solution will perform better compared to our original solution.



### Why can't Kadane's algorithm be solved with the sliding window technique?
- With a dynamically sized array, it isn't possible 

### Example - 