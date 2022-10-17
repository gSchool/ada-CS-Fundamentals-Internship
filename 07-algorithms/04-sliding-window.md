# Sliding Window Technique

## Overview

Within the broader category of dynamic programming, there are further techniques that can help us solve specific types of dynamic programming problems.

One useful strategy is called the **sliding window technique**. The sliding window technique is a strategy used to simplify time and space complexity when solving a problem that asks us to find some subsequence that satisifies a given set of conditions inside of a larger sequence.

## Understanding the Sliding Window Technique

Say we have some sequence of data that we want to examine. We can create a 'window' that allows us to look at some contiguous subsection of the data. Then, we then shift our window repeatedly in one direction so that we can look at every contiguous subsection one at a time. 

![Sliding Window](images/sliding-window.png)

This is called the sliding window technique because it mimics sliding a window open or shut. The section of data we are currently viewing shifts as we slide our window along the sequence.

![Sliding Window with an Array](images/sliding-window.png)

We can make our window as small or large as we , but we must be interested in looking at contiguous - meaning adjacent - subsections of the array. Observe that if we try to make the array to large. 


### What Kinds of D
Why is this usual?

Contiguous, meaning adjacent
- window must be of **fixed size** - this is why it won't work for max contiguous sum subarray


### Static Sliding Window

### Dynamic Sliding Window
### Why can't Kadane's algorithm be solved with the sliding window technique?
- With a dynamically sized array, it isn't possible 

### Example - 